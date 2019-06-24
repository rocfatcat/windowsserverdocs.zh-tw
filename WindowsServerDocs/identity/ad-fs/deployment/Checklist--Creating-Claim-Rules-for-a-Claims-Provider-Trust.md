---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: 檢查清單-Creating Claim Rules for 宣告提供者信任
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 708919691f88cc49d1f2bd74d8f4255e1a854353
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192386"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>檢查清單：建立宣告規則的宣告提供者信任


此檢查清單包含工作的規劃、 設計，以及部署與宣告提供者相關聯的宣告規則 Active Directory Federation Services \(AD FS\)。  
  
> [!NOTE]  
> 請依序完成此檢查清單中的工作。 當某個參考連結帶您進入某個程序時，請在完成該程序中的步驟之後返回本主題，讓您可以繼續進行此檢查清單中其餘的工作。  
  
![建立宣告規則](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**檢查清單：建立宣告提供者信任宣告規則集**  
  
||工作|參考資料|  
|-|--------|-------------|  
|![建立宣告規則](media/icon_checkboxo.gif)|檢閱有關宣告的概念、 宣告規則、 宣告規則集和宣告規則範本，以及它們相關聯的同盟信任。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of Claims](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[規則的角色宣告](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![建立宣告規則](media/icon_checkboxo.gif)|檢閱有關宣告透過宣告發行管線中的所有階段流動的方式，以及如何由宣告發行引擎處理規則的概念。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claims Pipeline](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![建立宣告規則](media/icon_checkboxo.gif)|若要有效規劃及實作會透過此宣告提供者信任發出輸出宣告，判斷是否需要一或多個宣告規則以及哪個宣告的規則您應該使用與此宣告提供者信任。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[判斷類型的宣告規則範本使用](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![建立宣告規則](media/icon_checkboxo.gif)|若要建立一個宣告，透過另一個規則，以及如何使用宣告規則語言，以及在以提供更複雜的邏輯比標準規則，以提供所要的結果，在理想的輸出宣告集時，請檢閱相關的概念。|![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用傳遞或篩選宣告規則的時機](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用轉換宣告規則的時機](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用 a Send LDAP Attributes as Claims Rule 的時機](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用傳送的群組成員資格宣告規則的時機](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[使用自訂宣告規則的時機](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![建立宣告規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[宣告規則語言的角色](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![建立宣告規則](media/icon_checkboxo.gif)|如果不存在，就必須建立宣告描述的因應組織的需求。 AD FS 隨附一組預設的宣告描述會公開在 AD FS 管理嵌入式管理單元中\-中。|![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[新增宣告描述](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![建立宣告規則](media/icon_checkboxo.gif)|根據您組織的需求，建立會與此宣告提供者信任相關聯，以便將適當地發出的宣告接受轉換規則集的一或多個宣告規則。|![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳遞或篩選傳入宣告](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則，以宣告方式傳送 LDAP 屬性](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則，以宣告形式傳送群組成員資格](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來轉換傳入宣告](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送驗證方法宣告](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送 AD FS 1.x 相容的宣告](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![建立宣告規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[建立規則來傳送宣告使用自訂規則](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
  
