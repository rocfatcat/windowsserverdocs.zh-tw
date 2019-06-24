---
title: 遠端桌面用戶端
description: 深入了解適用於您所有裝置的不同遠端桌面戶端
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d8158c-aee1-4c60-8a46-40ce5595b8e8
author: HeidiLohr
manager: dougkim
ms.author: helohr
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 341262243b5bbe8ed046382d7490a6e5c39b8965
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188130"
---
# <a name="remote-desktop-clients"></a>遠端桌面用戶端

>適用於：Windows 10，Windows 8.1、 Windows Server 2019、 Windows Server 2016、windows Server 2012 R2

您可以使用 Microsoft 遠端桌面用戶端，從幾乎任何使用幾乎任何裝置的地方連線至遠端電腦及工作資源。 您可以連線到您的工作電腦並且存取所有應用程式、檔案和網路資源，就像您是坐在您的辦公桌前面一樣。 您可以讓應用程式在工作時保持開啟，然後在家查看相同的應用程式 - 只需要使用 RD 用戶端。

在您開始前，請務必先查看[支援的設定](remote-desktop-supported-config.md)文章，其中會討論您可以使用遠端桌面戶端連線到的電腦。 此外，也請看一下[用戶端常見問題](remote-desktop-client-faq.md)。

可用的用戶端應用程式如下：

| 裝置   | 取得應用程式                                                                                                     | 設定指示                                                                |
|----------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Windows  | [在 Microsoft Store 中的 Windows 10 用戶端](https://go.microsoft.com/fwlink/?LinkID=616709)                      | [開始使用 Windows 上的遠端桌面用戶端](windows.md)                |
| Android  | [在 Google Play 的 android 用戶端](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)        | [開始使用在 Android 上的遠端桌面用戶端](remote-desktop-android.md) |
| iOS      | [在 iTunes store 中的 iOS 用戶端](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)     | [開始使用在 iOS 上的遠端桌面用戶端](remote-desktop-ios.md)         |
| macOS    | [在 iTunes store 中的 macOS 用戶端](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12) | [開始使用在 Mac 上的遠端桌面用戶端](remote-desktop-mac.md)         |

## <a name="configuring-the-remote-pc"></a>設定遠端電腦

若要先設定您的遠端電腦，再從遠端存取它，請[允許存取您的電腦](remote-desktop-allow-access.md)。

## <a name="remote-desktop-client-uri-scheme"></a>遠端桌面用戶端 URI 配置

您可以啟用統一資源識別項 (URI) 配置，跨平台整合遠端桌面用戶端的功能。 請查看您可搭配 iOS、Mac 及 Android 用戶端使用的[支援的 URI 屬性](remote-desktop-uri.md)。