---
title: IOS 上的安全区域布局指南
description: 平台特定信息，可使用的功能仅适用于特定的平台，而无需实现自定义呈现器或效果。 本文介绍如何使用特定于 iOS 平台的, 确保页面内容定位在屏幕上, 此区域对于使用 iOS 11 及更高版本的所有设备是安全的。
ms.prod: xamarin
ms.assetid: 2B6789C1-39B4-4C16-ADE1-3ED3378EAC63
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
ms.openlocfilehash: c6a2ec5a4d1466b7118e6cc7b03cc5518b27e2fb
ms.sourcegitcommit: 3ea9ee034af9790d2b0dc0893435e997bd06e587
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68644532"
---
# <a name="safe-area-layout-guide-on-ios"></a>IOS 上的安全区域布局指南

[![下载示例](~/media/shared/download.png) 下载示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

此 iOS 平台特定用于确保页面内容定位在屏幕上, 此区域对于使用 iOS 11 及更高版本的所有设备是安全的。 具体而言，这将有助于确保该内容未剪辑的舍入的设备角部、 家庭的指示符或在 iPhone X 上的传感器底座。设置使用在 XAML`Page.UseSafeArea`附加属性设置为`boolean`值：

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
             Title="Safe Area"
             ios:Page.UseSafeArea="true">
    <StackLayout>
        ...
    </StackLayout>
</ContentPage>
```

或者，可以使用它从 C# 使用 fluent API:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

On<iOS>().SetUseSafeArea(true);
```

`Page.On<iOS>`方法指定仅将在 iOS 上运行此特定于平台的。 `Page.SetUseSafeArea`方法，请在[ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)命名空间中，控制是否启用安全区域布局指南。

结果是屏幕的页面内容可置于是屏幕的安全的所有 Iphone 区域：

[![](page-safe-area-images/safe-area-layout.png "安全区域布局指南")](page-safe-area-images/safe-area-layout-large.png#lightbox "安全区域布局指南")

> [!NOTE]
> 定义由 Apple 的安全区域在 Xamarin.Forms 中用来设置[ `Page.Padding` ](xref:Xamarin.Forms.Page.Padding)属性，并且将重写此属性的任何以前已设置的值。

可以通过检索自定义安全区域及其[ `Thickness` ](xref:Xamarin.Forms.Thickness)值替换`Page.SafeAreaInsets`方法从[ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)命名空间。 它然后可修改为所需和重新分配给`Padding`该页的构造函数中的属性或[ `OnAppearing` ](xref:Xamarin.Forms.Page.OnAppearing)重写：

```csharp
protected override void OnAppearing()
{
    base.OnAppearing();

    var safeInsets = On<iOS>().SafeAreaInsets();
    safeInsets.Left = 20;
    Padding = safeInsets;
}
```

## <a name="related-links"></a>相关链接

- [PlatformSpecifics （示例）](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [创建平台特定信息](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
