---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: 設定宣告規則
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7a85044010c95f64fe1167d7bf186f265fe4beb9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964765"
---
# <a name="configure-claim-rules-in-ad-fs-for-windows-server"></a>在 Windows Server 的 AD FS 中設定宣告規則

在宣告式身分 \- 識別模型中， \( 做為同盟服務之 Active Directory 同盟服務 AD FS 的功能 \) 是發行包含一組宣告的權杖。 宣告規則負責管理 AD FS 問題之宣告的相關決策。 宣告規則和所有伺服器設定資料都會儲存在 AD FS 設定資料庫中。

AD FS 會根據以宣告形式提供的身分識別資訊和其他內容資訊，做出發行決策。 概括而言，AD FS 會藉由採用一組宣告做為輸入、執行一些轉換，然後傳回一組不同的宣告做為輸出，以作為規則處理器來運作。

下列主題可協助您建立 AD FS 將會處理的規則：

-   [建立規則以傳遞或篩選傳入宣告](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)

-   [建立規則允許所有使用者](Create-a-Rule-to-Permit-All-Users.md)

-   [建立規則依據傳入宣告允許或拒絕使用者](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)

-   [建立規則來以宣告方式傳送 LDAP 屬性](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)

-   [建立規則以宣告方式傳送群組成員資格](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)

-   [建立規則轉換傳入宣告](Create-a-Rule-to-Transform-an-Incoming-Claim.md)

-   [建立規則傳送驗證方法相容宣告](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)
-   [建立規則以傳送 AD FS 1.x 相容的宣告](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)

-   [建立規則使用自訂規則傳送宣告](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)

## <a name="see-also"></a>另請參閱
[AD FS 操作](../ad-fs-operations.md)
