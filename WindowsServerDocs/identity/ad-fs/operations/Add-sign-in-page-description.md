---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: 新增登入頁面描述
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 033663720750ee2990cbc6eb4dd0c6d9abe1a002
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962632"
---
# <a name="add-sign-in-page-description"></a>新增登 \- 入頁面描述

## <a name="to-add-sign-in-page-description"></a>新增登 \- 入頁面描述
若要將登 \- 入頁面描述新增至登 \- 入頁面，請使用下列 Windows PowerShell Cmdlet 和語法。

![新增登入描述](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

```powershell
Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"
```

> [!IMPORTANT]
> `SignInPageDescriptionText` 參數的字串支援包含標記與不包含標記的純 HTML。 因此，您也可以在不使用 p 標記的情況下執行下列 Cmdlet &lt; &gt; 。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." `

\-自訂登入頁面之後，自訂會有較高的優先順序; 因此，您應該自訂您想要支援的所有語言。 所有的自訂內容皆接受地區設定參數。 當您設定當地語系化的內容時，應該先使用較少的地區設定 \- （例如 "en"）來設定，然後再設定國家和地區特定的地區設定， \- 例如 "en-us \- "。

## <a name="additional-references"></a>其他參考資料

[AD FS 使用者登入自訂](AD-FS-user-sign-in-customization.md)
