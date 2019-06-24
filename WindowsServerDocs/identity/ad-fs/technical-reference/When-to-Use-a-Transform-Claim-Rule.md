---
ms.assetid: 77aa61bf-9c04-4889-a5d2-6f45bc1b8bd2
title: 使用轉換宣告規則的時機
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5ed8ee500582e0e687a2b52e83d99fc3cb8f147f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188339"
---
# <a name="when-to-use-a-transform-claim-rule"></a>使用轉換宣告規則的時機
您可以使用這項規則中 Active Directory Federation Services \(AD FS\)當您需要將傳入宣告類型對應至傳出宣告類型，然後再套用動作，以決定應該發生何種輸出，以值為基礎，在連入宣告產生。 當您使用此規則時，您會根據您在規則中設定的選項之一傳遞或轉換符合下列規則邏輯的宣告，如下表中所述。  
  
|規則選項|規則邏輯|  
|---------------|--------------|  
|傳遞所有傳入宣告|如果傳入宣告類型等於*指定的宣告類型*，且值等於*任何值*，則會以宣告類型等於*指定宣告類型*的傳出宣告傳遞該宣告。|  
|以不同的傳出宣告值取代傳入宣告值|如果傳入宣告類型等於*指定的宣告類型*，且值等於*指定的宣告值*，則會以新的傳出宣告值*指定的宣告值*和傳出宣告類型*指定的宣告類型*轉換該宣告|  
|取代內送電子\-郵件後置詞宣告新的電子\-郵件尾碼|如果傳入宣告類型等於*指定的宣告類型*，且值等於*任何尾碼值*，則會以新的傳出宣告值*指定的尾碼值*和傳出宣告類型*指定的宣告類型*轉換該宣告|  
  
下列章節提供宣告規則的基本介紹，並進一步提供如何使用此規則的詳細資訊。  
  
## <a name="about-claim-rules"></a>關於宣告規則  
宣告規則表示商務邏輯，會收取傳入宣告，對其套用條件的執行個體\(若 x 則 y\)和產生根據條件參數傳出宣告。 在您進一步閱讀本主題之前，請先閱讀下列清單，其中會概述關於宣告規則您應該知道的重要秘訣：  
  
-   在 AD FS 管理嵌入式管理單元\-，宣告規則只能建立使用宣告規則範本  
  
-   宣告規則處理程序內送宣告直接從宣告提供者\(Active Directory 或其他同盟服務等\)或宣告提供者信任上從輸出的接受轉換規則。  
  
-   宣告規則的處理方式，是由宣告發行引擎依時間先後順序按照指定的規則集處理。 藉由設定規則優先順序，您可以進一步精簡或篩選由特定規則集內的上一個規則所產生的宣告。  
  
-   宣告規則範本一律會要求您指定傳入宣告類型。 不過，您可以使用單一規則和同一宣告類型處理多個宣告值。  
  
如需詳細的宣告規則和宣告規則集的相關資訊，請參閱[規則的角色宣告](The-Role-of-Claim-Rules.md)。 如需有關規則的處理方式的詳細資訊，請參閱 < [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)。 宣告規則集的處理方式的詳細資訊，請參閱[The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md)。  
  
## <a name="pass-through-all-claim-values"></a>傳遞所有宣告值  
使用這個動作時，所有做為指定的傳入宣告類型之索引的傳入宣告值，會先對應至指定的傳出宣告類型，然後以傳出宣告傳送至您的同盟服務簽署的權杖。  
  
例如，當規則設定為**傳遞所有宣告值**選項邏輯，並且指定「群組」傳入宣告類型和「角色」傳出宣告類型，則所有從簽發者傳來的傳入宣告值會個別複製到個別的新傳出宣告，且新宣告為「角色」宣告類型。  
  
## <a name="transforming-a-claim"></a>轉換宣告  
在 AD FS 的詞彙*宣告轉換*方法來取代一個傳入宣告以不同的傳出宣告值的值。 「轉換傳入宣告」規則讓這個功能得以執行。 在此規則的屬性中，您可以設定條件，根據指定的傳入宣告類型將傳入值轉換為不同的傳出宣告值。  
  
例如在下圖中，規則的條件設定為以不同的傳出宣告值取代傳入的值，所有「群組」傳入宣告類型會對應到新的「角色」傳出宣告類型。 在這個案例中，傳入宣告值 Purchaser 會被新的傳出宣告值 Admin 取代。  
  
![使用轉型的時機](media/adfs2_transform.gif)  
  
您也可以使用此規則来套用的條件，將會取代所有的連入宣告與指定的電子\-郵件尾碼值的新值。 例如，您可以在此規則設定一個條件，將所有尾碼為 sales.corp.fabrikam.com 的宣告值都變更為 fabrikam.com。  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>在宣告提供者信任上設定此規則  
當您使用宣告提供者信任時，可將此規則設定為將傳入宣告從宣告提供者轉換成可信任的同等項目。 宣告類型或宣告值在您的組織中的意義可以和在宣告提供者組織中不同。 您可以使用此規則將來自宣告提供者的宣告類型和值正規化，使信賴憑證者可以理解提供者傳出宣告的同等項目。  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>在信賴憑證者信任上設定此規則  
當您使用信賴憑證者信任時，可將此規則設定為轉換特定信賴憑證者的宣告。 針對特定信賴憑證者，宣告類型或宣告值可能有不同的意義，此規則可讓您變更單一信賴憑證者的傳出宣告類型和值。  
  
## <a name="how-to-create-this-rule"></a>如何建立此規則  
建立此規則使用宣告規則語言，或使用**轉換傳入宣告**規則範本，在 AD FS 管理嵌入式管理單元中的\-中。 這個規則範本提供下列設定選項：  
  
-   指定宣告規則名稱  
  
-   將特定傳入宣告類型轉換為指定傳出宣告類型  
  
-   傳遞所有宣告值  
  
-   以不同的傳出宣告值取代傳入宣告值  
  
-   將內送電子\-郵件後置詞宣告新的電子\-郵件尾碼  
  
如需有關如何建立此範本的詳細資訊，請參閱[建立規則來轉換傳入宣告](https://technet.microsoft.com/library/dd807068.aspx)AD FS 部署指南中。  
  
## <a name="using-the-claim-rule-language"></a>使用宣告規則語言  
如果必須從一個以上的傳入宣告的內容建構傳出宣告，則必須改用自訂規則。 如果傳出宣告的宣告值必須根據傳入宣告值 — 但還有其他內容 — 您也必須在該內容中使用自訂規則。 如需詳細資訊，請參閱 [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)。  
  
### <a name="examples-of-how-to-construct-a-transform-rule-syntax"></a>如何建構轉換規則語法的範例  
使用宣告規則語言語法來轉換宣告時，可以設定轉換後宣告的屬性為新的常值。 例如，下列規則將角色宣告的值從 "Administrators" 變更為 "root"，並同時保留相同的宣告類型：  
  
```  
c:[type == “https://schemas.microsoft.com/ws/2008/06/identity/claims/role”, value == “Administrators”]  => issue(type = c.type, value = “root”);  
```  
  
規則運算式也可以用於宣告轉換。 例如，下列規則將會設定網域 windows 使用者名稱宣告中網域中\\給 FABRIKAM 的使用者格式：  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => issue(type = c.type, value = regexreplace(c.value, "(?<domain>[^\\]+)\\(?<user>.+)", "FABRIKAM\${user}"));  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>建立自訂規則的最佳做法  
可以將宣告轉換選擇性地套用到使用基本篩選功能所選取的宣告。 您可以為篩選所使用的每個宣告屬性指派值，與下列注意事項：  
  
|宣告屬性|描述|  
|------------------|---------------|  
|Type, Value, ValueType|指派最常使用這些屬性。 為了產生轉換後的宣告，至少必須指派類型和值。|  
|簽發者|宣告規則語言允許設定宣告的簽發者 (Issuer)，但通常不建議您這麼做。 宣告的簽發者在權杖中不會序列化。 收到權杖時，系統會將所有宣告的 Issuer 屬性設為簽署該權杖之同盟伺服器的識別碼。 因此，在規則中設定宣告的簽發者並不會影響權杖的內容，且一旦宣告封裝在權杖中，設定就會遺失。 設定簽發者唯一有意義的案例，是將簽發者設為宣告提供者規則集中的特定值，並且以參考這個特定值的規則撰寫信賴憑證者規則集。 如果沒有明確將 Issuer 屬性設為宣告規則中的值，宣告發行引擎會將其設為 “LOCAL AUTHORITY”。|  
|OriginalIssuer|和 Issuer 類似，通常不應該為 OriginalIssuer 明確指派值。 不同於 Issuer 的是，OriginalIssuer 屬性會在權杖中序列化，但是權杖取用者期望的是，如果有設定 OriginalIssuer，它會包含原始簽發宣告之同盟伺服器的識別碼。|  
|屬性|如上一節所述，在權杖之中不會保留宣告的屬性包，因此，只有當後續的本機原則會參考儲存在屬性內的資訊時，才應該指派屬性。|  
  
如需如何使用宣告規則語言的詳細資訊，請參閱[The Role of 宣告規則語言](The-Role-of-the-Claim-Rule-Language.md)。  
  
