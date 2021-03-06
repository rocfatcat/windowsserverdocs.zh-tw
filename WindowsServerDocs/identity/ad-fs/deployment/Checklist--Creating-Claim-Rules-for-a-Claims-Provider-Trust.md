---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: 檢查清單-建立宣告提供者信任的宣告規則
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 02cfddbe018b470000eca5331d53b3f0e38197ae
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945629"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>檢查清單：為宣告提供者信任建立宣告規則


此檢查清單包含用來規劃、設計和部署與 Active Directory 同盟服務 AD FS 中的宣告提供者信任相關聯的宣告規則的工作 \( \) 。

> [!NOTE]
> 請依序完成此檢查清單中的工作。 當某個參考連結帶您進入某個程序時，請在完成該程序中的步驟之後返回本主題，讓您可以繼續進行此檢查清單中其餘的工作。

![建立宣告規則](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**檢查清單：建立宣告提供者信任的宣告規則集**

|Task|參考|
|--------|-------------|
|請參閱有關宣告、宣告規則、宣告規則集和宣告規則範本的概念，以及它們如何與同盟信任產生關聯。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[角色](../../ad-fs/technical-reference/The-Role-of-Claims.md)<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[角色的宣告規則](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|
|請參閱有關宣告如何流經宣告發布管線中的所有階段，以及宣告發行引擎如何處理規則的概念。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[角色的宣告管線](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[角色](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|
|若要有效地規劃並執行將透過此宣告提供者信任發出的輸出宣告，請判斷是否需要一或多個宣告規則，以及您應該搭配此宣告提供者信任使用的宣告規則。|![建立宣告規則會](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[決定要使用的宣告規則範本類型](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|
|請參閱有關何時建立一個宣告規則的概念，以及如何使用宣告規則語言來提供比標準規則更複雜的邏輯，以在理想的輸出宣告集內提供所需的結果。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用通過或篩選宣告規則的](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)時機<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用轉換宣告規則的](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)時機<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[，以使用傳送 LDAP 屬性做為宣告規則](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[，以使用傳送群組成員資格做為宣告規則](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<p>![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用自訂宣告規則的](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)時機<p>![建立宣告規則具有宣告](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[規則語言的角色](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|
|如果尚未存在可滿足貴組織需求的宣告描述，則必須加以建立。 AD FS 隨附一組預設的宣告描述，會在 AD FS 管理嵌入式管理單元 \- 中公開。|![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[新增宣告描述](../../ad-fs/operations/Add-a-Claim-Description.md)|
|視組織的需求而定，針對與此宣告提供者信任相關聯的接受轉換規則集建立一或多個宣告規則，以便適當地發行宣告。|![建立宣告規則會](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來通過或篩選傳入](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)宣告<p>![建立宣告規則會](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送 LDAP 屬性作為宣告](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<p>![建立宣告規則會](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則，以宣告方式傳送群組成員資格](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<p>![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則以轉換傳入](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)宣告<p>![建立宣告規則會](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送驗證方法](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)宣告<p>![建立宣告規則會](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送 AD FS 1.X 相容的](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)宣告<p>![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則，以使用自訂規則傳送宣告](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|


