---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: 當地語系化的自訂
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 41a540b43fde264718ca7aa81ba0e48184cf1265
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956385"
---
# <a name="customization-for-localization"></a>當地語系化的自訂

可以將網頁內容當地語系化成英文以外的語言。 進行當地語系化時，請注意下列考量。

在自訂內容之後，自訂會有較高的優先順序；因此，您應該自訂您想要支援的所有語言。 所有的自訂內容皆接受地區設定參數。 當您設定當地語系化的內容時，請先使用較少的地區設定（例如 "en"）來設定它， \- 然後再設定國家/地區特定的地區設定， \- 例如 "en \- us"。

以下顯示某些額外的程式碼範例。

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}
Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}
```

以下顯示某些額外的程式碼範例。

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"

Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"
```

如果您想要將 web 內容自訂為需要 Unicode 輸入的英文以外的語言，建議您使用 Windows PowerShell ISE。 如需其他資訊，請參閱[Windows PowerShell ISE 簡介](/previous-versions/mt707506(v=msdn.10))。

## <a name="additional-references"></a>其他參考資料

[AD FS 使用者登入自訂](AD-FS-user-sign-in-customization.md)
