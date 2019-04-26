---
title: Erstellen eines benutzerdefinierten Xamarin.Forms-Designs
description: In diesem Artikel wird erläutert, wie zum Erstellen eines benutzerdefinierten Xamarin.Forms-Designs, zum Verweisen auf die in einer app wird.
ms.prod: xamarin
ms.assetid: 4FE08ADC-093F-47FA-B33C-20CF08B5D7E0
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/01/2017
ms.openlocfilehash: 0897afeacffc89e30b28474e4530a83d05d33cd2
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61187282"
---
# <a name="creating-a-custom-xamarinforms-theme"></a>Erstellen eines benutzerdefinierten Xamarin.Forms-Designs

![](~/media/shared/preview.png "Diese API ist derzeit als Vorschauversion")

Zusätzlich zum Hinzufügen eines Designs aus Nuget-Paketen (z. B. die [Licht](~/xamarin-forms/user-interface/themes/light.md) und [dunkel](~/xamarin-forms/user-interface/themes/dark.md) Designs), Ihre eigenen Ressourcennamen Wörterbuch Designs erstellen, auf die verwiesen werden, können in Ihrer app.

## <a name="example"></a>Beispiel

Die drei `BoxView`s angezeigt, auf die [Designs Seite](~/xamarin-forms/user-interface/themes/index.md) gemäß drei Klassen, die in den beiden Themen definiert formatiert sind.

Um zu verstehen, wie diese funktionieren, das folgende Markup erstellt eine entsprechende Formatvorlage, die Sie direkt mit hinzufügen konnte Ihre **"App.xaml"**.

Beachten Sie die `Class` Attribut für `Style` (im Gegensatz zu den [`x:Key`](~/xamarin-forms/user-interface/styles/inheritance.md)
Attribut in früheren Versionen von Xamarin.Forms verfügbar).

```xml
<ResourceDictionary>
  <!-- DEFINE ANY CONSTANTS -->
  <Color x:Key="SeparatorLineColor">#CCCCCC</Color>
  <Color x:Key="iOSDefaultTintColor">#007aff</Color>
  <Color x:Key="AndroidDefaultAccentColorColor">#1FAECE</Color>
  <OnPlatform x:TypeArguments="Color" x:Key="AccentColor">
    <On Platform="iOS" Value="{StaticResource iOSDefaultTintColor}" />
    <On Platform="Android" Value="{StaticResource AndroidDefaultAccentColorColor}" />
  </OnPlatform>
  <!--  BOXVIEW CLASSES -->
  <Style TargetType="BoxView" Class="HorizontalRule">
    <Setter Property="BackgroundColor" Value="{ StaticResource SeparatorLineColor }" />
    <Setter Property="HeightRequest" Value="1" />
  </Style>

  <Style TargetType="BoxView" Class="Circle">
    <Setter Property="BackgroundColor" Value="{ StaticResource AccentColor }" />
    <Setter Property="WidthRequest" Value="34"/>
    <Setter Property="HeightRequest" Value="34"/>
    <Setter Property="HorizontalOptions" Value="Start" />

    <Setter Property="local:ThemeEffects.Circle" Value="True" />
  </Style>

  <Style TargetType="BoxView" Class="Rounded">
    <Setter Property="BackgroundColor" Value="{ StaticResource AccentColor }" />
    <Setter Property="HorizontalOptions" Value="Start" />
    <Setter Property="BackgroundColor" Value="{ StaticResource AccentColor }" />

    <Setter Property="local:ThemeEffects.CornerRadius" Value="4" />
  </Style>
</ResourceDictionary>
```

Sie werden feststellen, dass die `Rounded` -Klasse verweist auf einen benutzerdefinierten Effekt `CornerRadius`.
Der Code für diesen Effekt, sind nachfolgend - mit eine benutzerdefinierten richtig darauf verweisen `xmlns` muss hinzugefügt werden, um die **"App.xaml"** des "Root"-Element:

```csharp
xmlns:local="clr-namespace:ThemesDemo;assembly=ThemesDemo"
```

### <a name="c-code-in-the-net-standard-library-project-or-shared-project"></a>C#-Code in der .NET Standard Library-Projekt oder ein freigegebenes Projekt

Der Code zum Erstellen einer Round-Ecke `BoxView` verwendet [Effekte](~/xamarin-forms/app-fundamentals/effects/index.md).
Der Eckradius mithilfe der angewendet wird eine `BindableProperty` und wird von der Anwendung implementiert ein [Auswirkung](~/xamarin-forms/app-fundamentals/effects/index.md). Der Effekt ist erforderlich, plattformspezifischen Code in die [iOS](#ios) und [Android](#android) Projekte (siehe unten).

```csharp
namespace ThemesDemo
{
  public static class ThemeEffects
  {
  public static readonly BindableProperty CornerRadiusProperty =
    BindableProperty.CreateAttached("CornerRadius", typeof(double), typeof(ThemeEffects), 0.0, propertyChanged: OnChanged<CornerRadiusEffect, double>);
    private static void OnChanged<TEffect, TProp>(BindableObject bindable, object oldValue, object newValue)
              where TEffect : Effect, new()
    {
        if (!(bindable is View view))
        {
            return;
        }

        if (EqualityComparer<TProp>.Equals(newValue, default(TProp)))
        {
            var toRemove = view.Effects.FirstOrDefault(e => e is TEffect);
            if (toRemove != null)
            {
                view.Effects.Remove(toRemove);
            }
        }
        else
        {
            view.Effects.Add(new TEffect());
        }

    }
    public static void SetCornerRadius(BindableObject view, double radius)
    {
        view.SetValue(CornerRadiusProperty, radius);
    }

    public static double GetCornerRadius(BindableObject view)
    {
        return (double)view.GetValue(CornerRadiusProperty);
    }

    private class CornerRadiusEffect : RoutingEffect
    {
        public CornerRadiusEffect()
            : base("Xamarin.CornerRadiusEffect")
        {
        }
    }
  }
}
```

<a name="ios" />

### <a name="c-code-in-the-ios-project"></a>C#-Code im iOS-Projekt

```csharp
using System;
using Xamarin.Forms;
using Xamarin.Forms.Platform.iOS;
using CoreGraphics;
using Foundation;
using XFThemes;

namespace ThemesDemo.iOS
{
    public class CornerRadiusEffect : PlatformEffect
    {
        private nfloat _originalRadius;

        protected override void OnAttached()
        {
            if (Container != null)
            {
                _originalRadius = Container.Layer.CornerRadius;
                Container.ClipsToBounds = true;

                UpdateCorner();
            }
        }

        protected override void OnDetached()
        {
            if (Container != null)
            {
                Container.Layer.CornerRadius = _originalRadius;
                Container.ClipsToBounds = false;
            }
        }

        protected override void OnElementPropertyChanged(System.ComponentModel.PropertyChangedEventArgs args)
        {
            base.OnElementPropertyChanged(args);

            if (args.PropertyName == ThemeEffects.CornerRadiusProperty.PropertyName)
            {
                UpdateCorner();
            }
        }

        private void UpdateCorner()
        {
            Container.Layer.CornerRadius = (nfloat)ThemeEffects.GetCornerRadius(Element);
        }
    }
}
```

<a name="android" />

### <a name="c-code-in-the-android-project"></a>C#-Code im Android-Projekt

```csharp
using System;
using Xamarin.Forms.Platform;
using Xamarin.Forms.Platform.Android;
using Android.Views;
using Android.Graphics;

namespace ThemesDemo.Droid
{
    public class CornerRadiusEffect : BaseEffect
    {
        private ViewOutlineProvider _originalProvider;

        protected override bool CanBeApplied()
        {
            return Container != null && Android.OS.Build.VERSION.SdkInt >= Android.OS.BuildVersionCodes.Lollipop;
        }

        protected override void OnAttachedInternal()
        {
            _originalProvider = Container.OutlineProvider;
            Container.OutlineProvider = new CornerRadiusOutlineProvider(Element);
            Container.ClipToOutline = true;
        }

        protected override void OnDetachedInternal()
        {
            Container.OutlineProvider = _originalProvider;
            Container.ClipToOutline = false;
        }

        protected override void OnElementPropertyChanged(System.ComponentModel.PropertyChangedEventArgs args)
        {
            base.OnElementPropertyChanged(args);

            if (!Attached)
            {
                return;
            }

            if (args.PropertyName == ThemeEffects.CornerRadiusProperty.PropertyName)
            {
                Container.Invalidate();
            }
        }

        private class CornerRadiusOutlineProvider : ViewOutlineProvider
        {
            private Xamarin.Forms.Element _element;

            public CornerRadiusOutlineProvider(Xamarin.Forms.Element element)
            {
                _element = element;
            }

            public override void GetOutline(Android.Views.View view, Outline outline)
            {
                var pixels =
                    (float)ThemeEffects.GetCornerRadius(_element) *
                    view.Resources.DisplayMetrics.Density;

                outline.SetRoundRect(new Rect(0, 0, view.Width, view.Height), (int)pixels);
            }
        }
    }
}
```


## <a name="summary"></a>Zusammenfassung

Ein benutzerdefiniertes Design kann erstellt werden, durch die Definition der Formate für jedes Steuerelement, das benutzerdefinierten Darstellung ist erforderlich. Mehrere Formate für ein Steuerelement unterschieden werden soll, von verschiedenen `Class` Attribute im Ressourcenverzeichnis, und klicken Sie dann angewendet, indem die `StyleClass` Attribut für das Steuerelement.

Ein Format kann auch nutzen [Effekte](~/xamarin-forms/app-fundamentals/effects/index.md) Anpassen der Darstellung eines Steuerelements.

[Implizite Stile](~/xamarin-forms/user-interface/styles/implicit.md) (ohne eine `x:Key` oder `Style` Attribut) weiterhin auf alle Steuerelemente angewendet werden, die entsprechen den `TargetType`.
