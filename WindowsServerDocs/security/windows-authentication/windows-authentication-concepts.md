---
title: Windows 驗證概念
description: Windows Server 安全性
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29d1db15-cae0-4e3d-9d8e-241ac206bb8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ee3fa19efa8c5098008749a467e649edcb5bb716
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876499"
---
# <a name="windows-authentication-concepts"></a>Windows 驗證概念

>適用於：Windows Server （半年通道），Windows Server 2016

這個參考概觀主題將說明 Windows 驗證所依據的概念。

驗證是確認物件或個人身分識別的程序。 驗證物件時，目標是要確認該物件為正版。 當您驗證個人時，目標就是確認的人不冒充者。

在網路內容中，驗證就是針對網路應用程式或資源提供身分識別的操作。 一般而言，證明身分識別密碼編譯作業所使用這兩個金鑰只有使用者知道 （如同公開金鑰密碼編譯） 或是共用的金鑰。 驗證交換的伺服器端會使用已知的密碼編譯金鑰比較簽署的資料，來驗證該驗證嘗試。

在安全的集中位置儲存密碼編譯金鑰，可以擴充和管理驗證程序。 Active Directory 是建議和預設的技術，來儲存身分識別資訊，包括密碼編譯金鑰是使用者的認證。 預設的 NTLM 與 Kerberos 實作需要 Active Directory。

驗證技術範圍從簡單的登入作業系統或在登入服務或應用程式，來識別使用者只有使用者知道，例如密碼，以使用類似的功能更強大的安全性機制的項目，權杖、 公開金鑰憑證、 圖片或生物屬性為使用者 has'such。 在商業環境中，使用者可能會在位於單一位置或跨多個位置的多種類型的伺服器上存取多個應用程式。 基於上述原因，驗證必須支援其他平台與其他 Windows 作業系統的環境。

## <a name="authentication-and-authorization-a-travel-analogy"></a>驗證和授權：旅遊比喻
旅遊比喻有助於解釋如何進行驗證。 一些準備工作會開始通常會需要。 旅行者必須證明他們，則為 true 的身分識別給其主應用程式授權單位。 這個概念可以證明的公民身分、 生日位置、 個人的憑券、 照片或任何所需的主機國家/地區的法律的形式。 旅行者的身分識別驗證的 passport，相當於發出，並且是由組織-的安全性原則管理的系統帳戶發佈。 Passport 和預定的目的根據一組規則與規定政府的授權單位所核發。

**旅程圖**

當旅行者抵達國際框線時，框線成立條件要求您提供認證，並旅行者提供他或她的 passport。 此程序是兩個方面：

-   成立條件會驗證 passport 驗證它已發行的安全性授權單位當地政府信任 （信任，並且至少發出護照），然後藉由驗證的 passport 未修改。

-   成立條件來驗證旅行者驗證所面臨的比對上 passport 如圖所示的人臉和其他必要的認證是很好的順序。

如果 passport 證明有效旅行者證實是其擁有者，驗證會成功，並旅行者可以存取整個框線。

安全性授權單位之間的可轉移信任是驗證的基礎;發生在國際的驗證類型為基礎的信任。 地方政府不知道旅行者，但信任主機 government 沒有。 當主機政府發出 passport 時，它不知道旅行者是。 它的信任發行出生證明或其他文件的單位。 發行出生證明，單位會信任醫生簽署憑證。 當醫生目睹旅行者的出生，並加上直接證明身分，使用憑證在此情況下新生的使用量。 如此一來，透過受信任的媒介，以傳輸的信任為可轉移的。

網路安全性的 Windows 用戶端/伺服器架構的基礎為可轉移的信任。 信任關係流經整個網域，例如網域樹狀目錄中，一組，並形成網域及信任該網域的所有網域之間的關聯性。 比方說，如果網域 A 有可轉移的信任關係，與網域 B，而網域 B 信任網域 C，則網域 A 信任網域 c。

沒有驗證與授權之間的差異。 使用驗證時，系統會證明您是您所表明的人員。 使用授權，系統會驗證您擁有您要執行的權限。 若要充分框線比喻下, 一個步驟，只驗證 旅行者有效的 passport 的適當的擁有者不一定授權旅行者輸入國家/地區。 特定國家/地區的居民可直接呈現只在其中輸入的國家/地區無限制權限授與所有公民的該特定國家/地區的輸入的情況下的 passport 輸入另一個國家/地區。

同樣地，您可以授與所有使用者存取資源的特定網域權限。 任何屬於該網域的使用者具有存取資源，，如同在加拿大，可讓輸入加拿大的美國公民。 不過，嘗試輸入巴西或印度的美國公民發現他們無法只藉由出示 passport，因為這些國家/地區的兩者都需要瀏覽美國公民能夠有效 visa 輸入這些國家/地區。 因此，驗證並不保證資源或授權使用資源的存取權。

## <a name="credentials"></a>認證
Passport，可能是相關聯的 visas 是 旅行者接受的認證。 不過，這些認證可能不會讓旅行者輸入，或存取國家/地區內的所有資源。 比方說，額外的認證，才能參加會議。 在 Windows 中，您能夠管理認證，以讓您可透過網路存取資源，無須重複提供認證的帳戶持有者。 這種類型的存取可讓使用者能夠一次經過系統來存取所有應用程式和資料來源，他們獲授權使用，而不輸入另一個帳戶識別碼或密碼。 能夠透過網路使用單一使用者身分識別 （Active Directory 所維護），藉由在本機快取使用者認證在作業系統的本機安全性授權 (LSA) 會利用 Windows 平台。 當使用者登入網域時，Windows 驗證封裝，以透明的方式使用的認證來驗證網路資源的認證時，提供單一登入。 如需有關認證的詳細資訊，請參閱 <<c0> [ 在 Windows 驗證的認證程序](credentials-processes-in-windows-authentication.md)。

旅行的多重要素驗證的一種可能的需求來執行，並呈現多份文件，來驗證他的身分識別，例如 passport 和會議的註冊資訊。 Windows 會實作這個表單或透過智慧卡、 虛擬智慧卡和生物識別技術驗證。 

## <a name="security-principals-and-accounts"></a>安全性主體和帳戶
在 Windows 中，任何使用者、 服務、 群組或電腦可以起始動作是安全性主體。 安全性主體擁有帳戶，可以是本機電腦，或以網域為基礎。 比方說，Windows 用戶端加入網域的電腦可以參與網路網域的網域控制站進行通訊，即使沒有任何人的使用者登入。 若要起始通訊，電腦必須具有有效的帳戶網域中。 之前接受從電腦的通訊，網域控制站上的本機安全性授權單位驗證電腦的識別，並接著定義電腦的安全性內容，就像人類的安全性主體一樣。 此安全性內容會定義在特定電腦或使用者、 服務、 群組或在網路上的電腦上的身分識別和能力的使用者或服務。 比方說，它會定義的資源，例如檔案共用或印表機，可以存取和的動作，例如讀取、 寫入或修改，可以執行的使用者、 服務或該資源上的電腦。 如需詳細資訊，請參閱 <<c0> [ 安全性主體](https://technet.microsoft.com/itpro/windows/keep-secure/security-principals)。

識別 claimant 送-服務--要求存取或資源的人類使用者帳戶。 會保留真確的 passport 旅行者擁有具有主機的國家/地區的帳戶。 使用者群組的使用者、 物件和服務都可以有個別的帳戶或共用的帳戶。 帳戶可以是群組的成員，而且可以指派特定權限與權限。 帳戶會受限於本機電腦、 群組、 網路、 或被指派給網域的成員資格。

內建的帳戶和安全性群組，它們的成員，被定義在每個 Windows 版本上。 使用安全性群組，您可以指派相同的安全性權限給許多使用者對於成功經過驗證，以簡化存取管理。 發出護照規則可能需要將旅行者指派給特定群組，例如商務或旅遊或政府。 此程序可確保一致的安全性權限，在群組的所有成員。 使用安全性群組來指派權限存取控制資源的表示會保持固定且易於管理和稽核。 藉由加入及移除使用者視需要從適當的安全性群組的存取，您可以減少至存取控制清單 (Acl) 進行變更的頻率。

獨立受管理的服務帳戶和虛擬帳戶已導入 Windows Server 2008 R2 和 Windows 7 提供必要的應用程式，例如 Microsoft Exchange Server 和 Internet Information Services (IIS)，並與自己的網域隔離「 帳戶 」，同時不需要系統管理員手動管理的服務主體名稱 (SPN) 和這些帳戶的認證。 群組受管理的服務帳戶所導入 Windows Server 2012 中和提供相同的功能，在網域內，但也將該功能延伸到多部伺服器。 當連線到伺服器陣列上託管的服務時，例如「網路負載平衡」，支援相互驗證的驗證通訊協定會要求服務的所有執行個體都使用相同的主體。

如需帳戶的詳細資訊，請參閱：

-   [Active Directory 帳戶](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-accounts)

-   [Active Directory 安全性群組](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-security-groups)

-   [本機帳戶](https://technet.microsoft.com/itpro/windows/keep-bastion.local-accounts)

-   [Microsoft Accounts](https://technet.microsoft.com/itpro/windows/keep-secure/microsoft-accounts)

-   [服務帳戶](https://technet.microsoft.com/itpro/windows/keep-secure/service-accounts)

-   [特殊身分](https://technet.microsoft.com/itpro/windows/keep-secure/special-identities)

## <a name="delegated-authentication"></a>委派的驗證
若要使用旅遊比喻，國家/地區可能會發出相同的存取權的官方的政府委派，所有成員只要委派為已知。 此委派可讓其他成員的授權單位上所做的一個成員。 在 Windows、 網路服務可接受來自使用者的驗證要求，並假設該使用者的身分識別，才能起始第二個網路服務的新連接時，就會發生委派的驗證。 若要支援委派的驗證，您必須建立前端或第一層的伺服器，例如負責處理用戶端驗證要求的網頁伺服器和後端 」 或 「 多層式架構的伺服器，例如大型資料庫，負責儲存資訊。 您可以委派的權限設定委派給組織中使用者的驗證，以減少您的系統管理員的系統管理負荷。

藉由建立服務或電腦為受信任可以委派，您可以讓該服務 」 或 「 完成電腦委派的驗證、 接收票證之使用者提出要求，然後存取該使用者的資訊。 此模型會限制存取後端伺服器上的資料只是為了這些使用者或服務具有正確的存取控制權杖該出現的認證。 此外，它可讓這些後端資源的存取稽核。 藉由要求透過委派來代表用戶端使用的伺服器的認證來存取所有的資料，您必須確定伺服器不會遭到洩漏，和其他伺服器上，您才能存取機密資訊的儲存。 委派的驗證是適用於多層式應用程式，專為使用多部電腦之間的單一登入功能。

### <a name="authentication-in-trust-relationships-between-domains"></a>在網域間信任關係中的驗證
有一個以上的網域有合理的大部分組織需要讓使用者能夠存取共用的資源位於不同的網域，就像旅行者允許在國家/地區的不同區域的移動。 控制這項存取需要也可以驗證並使用另一個網域中的資源授權一個網域中的使用者。 若要提供用戶端和不同網域中的伺服器之間的驗證和授權功能，必須有信任的兩個網域之間。 信任是安全的 Active Directory 通訊發生和是不可或缺的安全性元件的 Windows Server 網路架構的基礎技術。

存在信任時兩個網域之間，針對每個網域的驗證機制會信任來自其他網域驗證。 信任協助提供對資源網域-信任的網域-中共用資源的控制存取，藉由驗證連入驗證要求是來自受信任的授權單位-信任的網域。 如此一來，信任會做為橋接器，只讓已驗證的網域之間的驗證要求移動。

特定的信任的驗證要求的傳遞方式，端視其設定方式而定。 藉由提供每個網域中其他網域資源的存取可以藉由提供受信任的網域中信任的網域中，資源的存取，單向或雙向、 信任關係。 信任也是其中一個非轉移，只有兩個信任的夥伴網域之間，或可轉移，存在案例的信任，在此情況下信任會自動延伸至任何其他網域的其中一個夥伴所信任。

如需信任的運作方式的資訊，請參閱 < [< 網域與樹系信任的運作](https://technet.microsoft.com/library/cc773178(v=ws.10).aspx)。

### <a name="protocol-transition"></a>通訊協定轉換
通訊協定轉換可協助應用程式的設計工具，讓應用程式支援不同的驗證機制，在使用者驗證層，而只要切換到安全性功能，例如相互驗證的 Kerberos 通訊協定和限制的委派，在後續的應用程式層中。

如需有關通訊協定轉換的詳細資訊，請參閱 < [Kerberos 通訊協定轉換與限制委派](https://technet.microsoft.com/library/cc758097(v=ws.10).aspx)。

### <a name="constrained-delegation"></a>限制委派
限制的委派讓系統管理員指定與強制執行限制的範圍，應用程式服務可以代表使用者的應用程式信任界限的能力。 您可以指定受信任可以委派的電腦可以從中要求資源的特定服務。 限制服務的授權權限的彈性可協助降低不受信任的服務遭到入侵的機會來改善應用程式安全性設計。

如需有關限制委派的詳細資訊，請參閱[Kerberos 限制委派概觀](../kerberos/kerberos-constrained-delegation-overview.md)。

## <a name="see-also"></a>另請參閱
[Windows 登入及驗證技術概觀](https://technet.microsoft.com/library/dn269029.aspx)

