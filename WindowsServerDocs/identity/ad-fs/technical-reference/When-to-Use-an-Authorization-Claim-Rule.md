---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: 使用授權宣告規則的時機
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 690ae558f625ca3a4c5878be229d950902f7f5e2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958696"
---
# <a name="when-to-use-an-authorization-claim-rule"></a>使用授權宣告規則的時機
\( \) 當您需要取得傳入宣告類型，然後套用動作來根據您在規則中指定的值來決定是否允許或拒絕使用者存取時，您可以在 Active Directory 同盟服務 AD FS 中使用此規則。 當您使用此規則時，您會根據您在規則中設定的選項之一，傳遞或轉換符合下列規則邏輯的宣告。

|規則選項|規則邏輯|
|---------------|--------------|
|允許所有使用者|如果傳入宣告類型等於「任何宣告類型」** 且值等於「任何值」**，則會發行值等於「允許」** 的宣告|
|允許具有這個傳入宣告的使用者存取|如果傳入宣告類型等於「指定的宣告類型」** 且值等於「指定的宣告值」**，則會發行值等於「允許」** 的宣告|
|拒絕具有這個傳入宣告的使用者的存取|如果傳入宣告類型等於「指定的宣告類型」** 且值等於「指定的宣告值」**，則會發行值等於「拒絕」** 的宣告|

下列章節提供宣告規則的基本介紹，並進一步提供如何使用此規則的詳細資訊。

## <a name="about-claim-rules"></a>關於宣告規則
宣告規則代表會接受傳入宣告的商務邏輯實例， \( 如果 x then y 則套用條件， \) 並根據條件參數產生傳出宣告。 在您進一步閱讀本主題之前，請先閱讀下列清單，其中會概述關於宣告規則您應該知道的重要秘訣：

-   在 [AD FS 管理] 嵌入式管理單元中 \- ，只能使用宣告規則範本建立宣告規則

-   宣告規則會直接從宣告提供者 \( （例如 Active Directory 或另一個同盟服務， \) 或從宣告提供者信任的接受轉換規則輸出）處理傳入宣告。

-   宣告規則的處理方式，是由宣告發行引擎依時間先後順序按照指定的規則集處理。 藉由設定規則優先順序，您可以進一步精簡或篩選由特定規則集內的上一個規則所產生的宣告。

-   宣告規則範本一律會要求您指定傳入宣告類型。 不過，您可以使用單一規則和同一宣告類型處理多個宣告值。

如需宣告規則和宣告規則集的詳細資訊，請參閱宣告[規則的角色](The-Role-of-Claim-Rules.md)。 如需如何處理規則的詳細資訊，請參閱[宣告引擎的角色](The-Role-of-the-Claims-Engine.md)。 如需宣告規則集處理方式的詳細資訊，請參閱[宣告管線的角色](The-Role-of-the-Claims-Pipeline.md)。

## <a name="permit-all-users"></a>允許所有使用者
當您使用「允許所有使用者」規則範本時，所有的使用者都將可存取信賴憑證者。 不過，您可以使用其他授權規則進一步限制存取權。 如果一項規則允許使用者存取信賴憑證者，而另一個規則拒絕使用者存取信賴憑證者，拒絕結果將會覆寫允許結果，而拒絕使用者的存取。

從同盟服務獲准存取信賴憑證者的使用者，仍可能遭信賴憑證者拒絕服務。

## <a name="permit-access-to-users-with-this-incoming-claim"></a>允許具有這個傳入宣告的使用者存取
當您使用 [根據傳入宣告允許或拒絕使用者] 規則範本來建立規則，並將條件設定為 [允許] 時，您可以根據傳入宣告的類型和值，允許特定使用者對信賴憑證者的存取權。 例如，您可以使用此規則範本建立下列規則：僅允許群組宣告值為 Domain Admins 的使用者。 如果一項規則允許使用者存取信賴憑證者，而另一個規則拒絕使用者存取信賴憑證者，拒絕結果將會覆寫允許結果，而拒絕使用者的存取。

從同盟服務獲准存取信賴憑證者的使用者，仍可能遭信賴憑證者拒絕服務。 如果您想要允許所有使用者存取信賴憑證者，請使用「允許所有使用者」規則範本。

## <a name="deny-access-to-users-with-this-incoming-claim"></a>拒絕具有這個傳入宣告的使用者的存取
當您使用 [根據傳入宣告允許或拒絕使用者] 規則範本來建立規則，並將條件設定為 [拒絕] 時，您可以根據傳入宣告的類型和值，拒絕使用者對信賴憑證者的存取權。 例如，您可以使用此規則範本建立下列規則：拒絕群組宣告值為 Domain Users 的所有使用者。

如果您想要使用拒絕條件，但同時允許特定使用者存取信賴憑證者，您後續必須明確地新增授權規則，以及讓這些使用者存取信賴憑證者的允許條件。

當宣告發行引擎處理規則集時，如果使用者遭到拒絕存取，則會關閉進一步的規則處理，而 AD FS 會對使用者的要求傳回「拒絕存取」錯誤。

## <a name="authorizing-users"></a>授權使用者
在 AD FS 中，授權規則會用來發出允許或拒絕宣告，以根據所使用的宣告類型來判斷使用者或使用者群組是否 \( \) 可存取指定信賴憑證者中的 Web \- 資源。 只可以在信賴憑證者信任上設定授權規則。

### <a name="authorization-rule-sets"></a>授權規則集
視您需要設定的允許或拒絕作業類型之不同，會有不同的授權規則集。 這些規則集包括：

-   **發佈授權規則**：這些規則會決定使用者是否可接收信賴憑證者的宣告，因而能夠存取該信賴憑證者。

-   **委派授權規則**：這些規則會決定使用者是否可做為信賴憑證者的另一個使用者。 當使用者做為另一位使用者時，要求端使用者的相關宣告仍會放置在權杖中。

-   **模擬授權規則**：這些規則會決定使用者是否可做為信賴憑證者的另一個使用者。 模擬另一個使用者是非常強大的功能，因為信賴憑證者並不知道使用者正被模擬。

如需有關如何將授權規則程序融入宣告發行管線中的詳細資訊，請參閱「宣告發行引擎的角色」。

### <a name="supported-claim-types"></a>支援的宣告類型
AD FS 會定義兩個宣告類型，用來判斷是否允許或拒絕使用者。 這些宣告類型的統一資源識別項 uri 如下所示 \( \) ：

1.  **允許**： HTTP： \/ \/ schemas.microsoft.com \/ 授權 \/ 宣告 \/ 允許

2.  **拒絕**： HTTP： \/ \/ schemas.microsoft.com \/ 授權 \/ 宣告 \/ 拒絕

## <a name="how-to-create-this-rule"></a>如何建立此規則
您可以使用宣告規則語言，或使用 [AD FS 管理] 嵌入式管理單元中的 [**允許所有使用者**] 規則範本或 [**根據傳入宣告允許或拒絕使用者**] 規則範本來建立這兩個授權規則 \- 。 「允許所有使用者」規則範本未提供任何設定選項。 但「根據傳入宣告允許或拒絕使用者」規則範本則提供下列設定選項：

-   指定宣告規則名稱

-   指定傳入宣告類型

-   輸入傳入宣告值

-   允許具有這個傳入宣告的使用者存取

-   拒絕具有這個傳入宣告的使用者的存取

如需有關如何建立此範本的詳細指示，請參閱 AD FS 部署指南中的[建立規則以允許所有使用者](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913577(v=ws.11))或[建立規則以根據傳入宣告來允許或拒絕使用者](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913594(v=ws.11))。

## <a name="using-the-claim-rule-language"></a>使用宣告規則語言
如果只有在宣告值符合自訂模式時才應傳送宣告，您必須使用自訂規則。 如需詳細資訊，請參閱 [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)。

### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>說明如何根據多個宣告建立授權規則的範例
當使用宣告規則語言語法來授權宣告時，也可以根據使用者的原始宣告中是否有多個宣告來發行宣告。 只有在使用者屬於「編輯者」群組的成員，並且已使用 Windows 驗證通過驗證後，下列規則才會發出授權宣告：

```
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",
value == "urn:federation:authentication:windows" ]
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == "editors"]
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");
```

### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>說明如何建立授權規則以委派可建立或移除同盟伺服器 Proxy 信任之人員的範例
必須先建立同盟服務與同盟伺服器 Proxy 電腦之間的信任，同盟服務才可以使用同盟伺服器 Proxy 重新導向用戶端要求。 根據預設，順利在 AD FS 同盟伺服器 Proxy 設定精靈中提供下列其中一個認證時，將會建立 Proxy 信任：

-   Proxy 所將保護的服務帳戶 (由同盟服務使用)

-   在同盟伺服器陣列中的所有同盟伺服器上，屬於本機系統管理員群組成員的 Active Directory 網域帳戶

當您想要指定哪些使用者可以建立給定同盟服務的 Proxy 信任時，您可以使用下列任何委派方法。 這份方法清單的優先順序是根據 AD FS 產品小組對於最安全且最不有問題的委派方法的建議。 您只需要根據組織的需求使用其中一個方法即可：

1.  在 Active Directory 中建立網域安全性群組（ \( 例如 FSProxyTrustCreators \) ），將此群組新增至伺服器陣列中每部同盟伺服器上的本機系統管理員群組，然後只將您要委派此許可權的使用者帳戶新增至新群組。 這是慣用的方法。

2.  將使用者的網域帳戶新增至伺服器陣列中每部同盟伺服器上的系統管理員群組。

3.  如果您因故無法使用其中一種方法，您也可以建立符合此用途的授權規則。 您可以使用自訂授權規則，指定哪些 Active Directory 網域使用者帳戶也可以建立、甚至移除與指定的同盟服務相關聯的所有同盟伺服器 Proxy 之間的信任。但我們不建議此做法，因為此規則若未正確撰寫，可能會導致複雜的狀況。

    如果您選擇 [方法 3]，您可以使用下列規則語法來發出授權宣告，以便 \( 在此情況下允許指定的使用者，contoso \\ frankm \) 為同盟服務的一個或多個同盟伺服器 proxy 建立信任。 您必須使用 Windows PowerShell 命令**集 \- set-adfsproperties addproxyauthorizationrules 來**來套用此規則。

    ```
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")

    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");

    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );

    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );
    ```

    如果您後續想要移除使用者，讓該使用者無法再建立 Proxy 信任，您可以還原至預設 Proxy 信任授權規則，以移除使用者建立 Proxy 對同盟服務之信任的權限。 您也必須使用 Windows PowerShell 命令**集 \- set-adfsproperties addproxyauthorizationrules 來**來套用此規則。

    ```
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");

    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );

    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );
    ```

如需如何使用宣告規則語言的詳細資訊，請參閱宣告[規則語言的角色](The-Role-of-the-Claim-Rule-Language.md)。

