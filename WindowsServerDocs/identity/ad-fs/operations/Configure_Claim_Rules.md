---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: 在 AD FS 中設定宣告規則
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8f01e78689e687f4ed44653dd3213ab62011359d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967505"
---
# <a name="configure-claim-rules"></a>設定宣告規則

在宣告式身分 \- 識別模型中，Active Directory 同盟服務 (AD FS) 為同盟服務的功能，就是發出包含一組宣告的權杖。 宣告規則負責管理 AD FS 問題之宣告的相關決策。 宣告規則和所有伺服器設定資料都會儲存在 AD FS 設定資料庫中。

AD FS 會根據以宣告形式提供的身分識別資訊和其他內容資訊，做出發行決策。 概括而言，AD FS 會藉由採用一組宣告做為輸入、執行一些轉換，然後傳回一組不同的宣告做為輸出，以作為規則處理器來運作。

下列主題可協助您建立 AD FS 將會處理的規則：

-   [建立規則以傳遞或篩選傳入宣告](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)

-   [建立規則允許所有使用者](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)

-   [建立規則依據傳入宣告允許或拒絕使用者](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)

-   [建立規則來以宣告方式傳送 LDAP 屬性](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)

-   [建立規則以宣告方式傳送群組成員資格](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)

-   [建立規則轉換傳入宣告](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)

-   [建立規則傳送驗證方法相容宣告](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)

-   [建立規則使用自訂規則傳送宣告](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)

## <a name="see-also"></a>另請參閱
[AD FS 操作](../ad-fs-operations.md)
