---
title: 開始使用群組受管理的服務帳戶
description: Windows Server 安全性
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6da212185eb47d3f30f81ca6f1eb322bc232e229
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881449"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>開始使用群組受管理的服務帳戶

>適用於：Windows Server （半年通道），Windows Server 2016


本指南提供啟用及使用 Windows Server 2012 中的群組受控服務帳戶的逐步指示和背景資訊。

**在這份文件**

-   [必要條件](#BKMK_Prereqs)

-   [簡介](#BKMK_Intro)

-   [部署新的伺服器陣列](#BKMK_DeployNewFarm)

-   [新增至現有的伺服器陣列的成員主機](#BKMK_AddMemberHosts)

-   [更新群組受管理的服務帳戶屬性](#BKMK_Update_gMSA)

-   [解除委任成員主機從現有的伺服器陣列](#BKMK_DecommMemberHosts)


> [!NOTE]
> 本主題包含可讓您用來將部分所述的程序自動化的 Windows PowerShell Cmdlet 範例。 如需詳細資訊，請參閱[使用 Cmdlet](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="BKMK_Prereqs"></a>必要條件
請參閱本主題中的 [群組受管理的服務帳戶需求](#BKMK_gMSA_Req)一節。

## <a name="BKMK_Intro"></a>簡介
當用戶端電腦連線到伺服器陣列上裝載的服務，且該伺服器陣列使用網路負載平衡 (NLB) 或是某個其他讓所有伺服器在用戶端看來都是相同服務的方法時，除非所有服務執行個體都使用相同的主體，否則無法使用支援相互驗證 (例如 Kerberos) 的驗證通訊協定。 這表示每個服務都使用相同的密碼/金鑰來證明其身分識別。

> [!NOTE]
> 容錯移轉叢集不支援 gMSA。 不過，在叢集服務上執行的服務如果是 Windows 服務、應用程式集區、排定的工作或原生支援 gMSA 或 sMSA，便可使用 gMSA 或 sMSA。

服務有下列主體可供選擇，而且各有某些限制。

|主體|領域|服務支援|密碼管理|
|-------|-----|-----------|------------|
|Windows 系統的電腦帳戶|網域|僅限一部加入網域的伺服器|電腦管理|
|沒有 Windows 系統的電腦帳戶|網域|任何加入網域的伺服器|None|
|虛擬帳戶|本機|僅限一部伺服器|電腦管理|
|Windows 7 獨立受管理的服務帳戶|網域|僅限一部加入網域的伺服器|電腦管理|
|使用者帳戶|網域|任何加入網域的伺服器|None|
|群組受管理的服務帳戶|網域|任何 Windows Server 2012 已加入網域的伺服器|網域控制站管理，主機抓取|

Windows 電腦帳戶、Windows 7 獨立「受管理的服務帳戶」(sMSA) 或虛擬帳戶無法跨多個系統共用。 如果您為伺服器陣列上的服務設定一個要共用的帳戶，則除了 Windows 系統以外，您還必須選擇一個使用者帳戶或電腦帳戶。 不論哪一種方式，這些帳戶都不會擁有單一控制點密碼管理的功能。 如此會產生問題，亦即每個組織需要建立高度耗費資源的解決方案來為 Active Directory 中的服務更新金鑰，然後將金鑰傳送給這些服務的所有執行個體。

Windows Server 2012，服務或服務系統管理員不需要管理服務執行個體時使用群組受控服務帳戶 (gMSA) 之間的密碼同步處理。 您需在 AD 中佈建 gMSA，然後設定支援「受管理的服務帳戶」的服務。 您可以使用 *-ADServiceAccount Cmdlet (Active Directory 模組的一部分) 來佈建 gMSA。 下列各項支援主機上的服務身分識別設定：

-   與 sMSA 相同的 API，因此支援 sMSA 的產品也將支援 gMSA

-   使用「服務控制管理員」來設定登入身分識別的服務

-   使用應用程式集區的 IIS 管理員來設定身分識別的服務

-   使用「工作排程器」的工作

### <a name="BKMK_gMSA_Req"></a>群組受控服務帳戶需求
下表列出使用 gMSA 讓 Kerberos 驗證與服務搭配運作的作業系統需求。 Active Directory 需求列在這個表格之後。

若要執行用來管理群組「受管理的服務帳戶」的 Windows PowerShell 命令，必須有 64 位元架構。

**作業系統需求**

|項目|需求|作業系統|
|------|--------|----------|
|用戶端應用程式主機|RFC 相容的 Kerberos 用戶端|至少為 Windows XP|
|使用者帳戶的網域 Dc|RFC 相容的 KDC|至少為 Windows Server 2003|
|共用服務成員主機|| Windows Server 2012 |
|成員主機的網域 Dc|RFC 相容的 KDC|至少為 Windows Server 2003|
|gMSA 帳戶的網域 Dc| Windows Server 2012 網域控制站可供主機用來擷取密碼|它可以早於 Windows Server 2012 有某些系統的 Windows Server 2012 的網域 |
|後端服務主機|RFC 相容的 Kerberos 應用程式伺服器|至少為 Windows Server 2003|
|後端服務帳戶的網域 Dc|RFC 相容的 KDC|至少為 Windows Server 2003|
|適用於 Active Directory 的 Windows PowerShell|安裝在支援 64 位元架構的電腦本機或安裝在遠端管理電腦 (例如使用「遠端伺服器管理工具組」) 上的「適用於 Active Directory 的 Windows PowerShell」| Windows Server 2012 |

**Active Directory 網域服務需求**

-   將 gMSA 網域樹系中的 Active Directory 架構必須更新為 Windows Server 2012，才能建立 gMSA。

    您可以在安裝執行 Windows Server 2012 網域控制站，或從執行 Windows Server 2012 電腦執行版本的 adprep.exe 更新結構描述。 物件 CN=Schema,CN=Configuration,DC=Contoso,DC=Com 的 object-version 屬性值必須是 52。

-   已部署新的 gMSA 帳戶

-   如果是依群組管理要使用 gMSA 的服務主機權限，則需要新的或現有的安全性群組

-   如果是依群組管理服務存取控制，則需要新的或現有的安全性群組

-   如果未在網域中部署 Active Directory 的第一個主要根金鑰，或尚未建立該金鑰，則請建立它。 您可以在 KdsSvc 作業記錄 (事件識別碼 4004) 中確認該金鑰的建立結果。

如需相關指示如何建立金鑰，請參閱[建立金鑰發佈服務 KDS 根金鑰](create-the-key-distribution-services-kds-root-key.md)。 Microsoft 金鑰發佈服務 (kdssvc.dll) 可管理 AD 的根金鑰。

**生命週期**

使用 gMSA 功能之伺服器陣列的生命週期通常涉及下列工作：

-   部署新伺服器陣列

-   將成員主機新增到現有的伺服器陣列

-   將成員主機從現有的伺服器陣列解除委任

-   將現有的伺服器陣列解除委任

-   將已不安全的成員主機從伺服器陣列移除 (如有必要)

## <a name="BKMK_DeployNewFarm"></a>部署新的伺服器陣列
部署新伺服器陣列時，服務系統管理員將必須判斷：

-   服務是否支援使用 gMSA

-   服務需要輸入或輸出的已驗證連線

-   使用 gMSA 之服務的成員主機電腦帳戶名稱

-   服務的 NetBIOS 名稱

-   服務的 DNS 主機名稱

-   服務的服務主體名稱 (SPN)

-   密碼變更間隔 (預設值為 30 天)

### <a name="BKMK_Step1"></a>步驟 1:佈建群組受管理的服務帳戶
只有當樹系架構已更新為 Windows Server 2012 中，已部署 Active Directory 的主要根金鑰，而且將建立 gMSA 的網域中沒有至少一個 Windows Server 2012 DC，才能建立 gMSA。

若要完成下列程序，至少需要 **Domain Admins**、 **Account Operators** 的成員資格或是建立 msDS-GroupManagedServiceAccount 物件的能力。

#### <a name="BKMK_CreateGMSA"></a>若要建立群組 gMSA 使用 New-adserviceaccount cmdlet

1.  在 Windows Server 2012 網域控制站，請從工作列執行 Windows PowerShell。

2.  在 Windows PowerShell 的命令提示字元中，輸入下列命令，然後按下 ENTER。 (Active Directory 模組將會自動載入。)

    **新 ADServiceAccount [-名稱] <string> -DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < 可為 Null [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal]>]-SamAccountName <string> -ServicePrincipalNames < 字串 [] >**

    |參數|字串|範例|
    |-------|-----|------|
    |名稱|帳戶的名稱|ITFarm1|
    |DNSHostName|服務的 DNS 主機名稱|ITFarm1.contoso.com|
    |KerberosEncryptionType|主機伺服器支援的任何加密類型|RC4、AES128、AES256|
    |ManagedPasswordIntervalInDays|密碼變更間隔 (單位為天) (如果未提供，則預設值為 30 天)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|成員主機的電腦帳戶或成員主機所屬的安全性群組|ITFarmHosts|
    |SamAccountName|服務的 NetBIOS 名稱 (如果與 Name 不相同)|ITFarm1|
    |ServicePrincipalNames|服務的服務主體名稱 (SPN)|http/ITFarm1.contoso.com/contoso.com、http/ITFarm1.contoso.com/contoso、http/ITFarm1/contoso.com、http/ITFarm1/contoso|

    > [!IMPORTANT]
    > 只有在建立時，才能設定密碼變更間隔。 如果您需要變更此間隔，就必須建立新的 gMSA，然後在建立時設定它。

    **範例**

    請以單行輸入命令，即使由於格式限制，此處可能會顯示為換行成數行也一樣。

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

若要完成此程序，至少需要 **Domain Admins**、**Account Operators** 的成員資格或是建立 msDS-GroupManagedServiceAccount 物件的能力。 如需使用適當帳戶和群組成員資格的詳細資料，請參閱 [本機與網域的預設群組](https://technet.microsoft.com/library/dd728026(WS.10).aspx)。

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>使用 New-ADServiceAccount Cmdlet 來建立僅用於輸出驗證的 gMSA

1.  在 Windows Server 2012 網域控制站，請從工作列執行 Windows PowerShell。

2.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **New-ADServiceAccount [-Name] <string> -RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays <Nullable[Int32]>] [-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>]**

    |參數|字串|範例|
    |-------|-----|------|
    |名稱|帳戶的名稱|ITFarm1|
    |ManagedPasswordIntervalInDays|密碼變更間隔 (單位為天) (如果未提供，則預設值為 30 天)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|成員主機的電腦帳戶或成員主機所屬的安全性群組|ITFarmHosts|

    > [!IMPORTANT]
    > 只有在建立時，才能設定密碼變更間隔。 如果您需要變更此間隔，就必須建立新的 gMSA，然後在建立時設定它。

**範例**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>步驟 2:設定服務身分識別應用程式服務
若要設定 Windows Server 2012 中的服務，請參閱下列功能文件：

-   IIS 應用程式集區

    如需詳細資訊，請參閱 [指定應用程式集區的識別 (IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx)。

-   Windows 服務

    如需詳細資訊，請參閱 [服務](https://technet.microsoft.com/library/cc772408.aspx)。

-   工作

    如需詳細資訊，請參閱 [工作排程器概觀](https://technet.microsoft.com/library/cc721871.aspx)。

其他服務可以支援 gMSA。 如需有關如何設定這些服務的詳細資料，請參閱適當的產品文件。

## <a name="BKMK_AddMemberHosts"></a>新增至現有的伺服器陣列的成員主機
使用安全性群組來管理成員主機，如果電腦帳戶新增為新的成員主機，以安全性群組 （gMSA 成員主機的成員） 使用下列方法之一。

若要完成這些程序，至少需要 **Domain Admins**的成員資格或是將成員新增到安全性群組物件的能力。

-   方法 1：Active Directory 使用者和電腦

    如需有關如何使用這個方法的程序，請參閱使用 Windows 介面 [新增電腦帳戶到群組](https://technet.microsoft.com/library/cc733097.aspx) ，以及 [管理 Active Directory 管理中心的不同網域](manage-different-domains-in-active-directory-administrative-center.md)。

-   方法 2：dsmod

    如需有關如何使用這個方法的程序，請參閱使用命令列 [新增電腦帳戶到群組](https://technet.microsoft.com/library/cc733097.aspx) 。

-   方法 3：Windows PowerShell Active Directory Cmdlet Add-ADPrincipalGroupMembership

    如需有關如何使用這個方法的程序，請參閱 [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx)。

如果是使用電腦帳戶，請尋找現有的帳戶，然後新增電腦帳戶。

若要完成此程序，至少需要 **Domain Admins**、 **Account Operators**的成員資格或是管理 msDS-GroupManagedServiceAccount 物件的能力。 如需使用適當帳戶和群組成員資格的詳細資料，請參閱＜本機與網域的預設群組＞。

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>使用 Set-ADServiceAccount Cmdlet 來新增成員主機

1.  在 Windows Server 2012 網域控制站，請從工作列執行 Windows PowerShell。

2.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **Get-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **Set-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>**

|參數|字串|範例|
|-------|-----|------|
|名稱|帳戶的名稱|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|成員主機的電腦帳戶或成員主機所屬的安全性群組|Host1、Host2、Host3|

**範例**

例如，若要新增成員主機，請輸入下列命令，然後按下 ENTER。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1,Host2,Host3

```

## <a name="BKMK_Update_gMSA"></a>更新群組受管理的服務帳戶屬性
若要完成這些程序，至少需要 **Domain Admins**、 **Account Operators**的成員資格或是寫入 msDS-GroupManagedServiceAccount 物件的能力。

開啟「適用於 Windows PowerShell 的 Active Directory 模組」，並使用 Set-ADServiceAccount Cmdlet 設定任何屬性。

如需有關如何設定這些屬性的詳細資訊，請參閱 TechNet 文件庫中的 [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) ，或是在「適用於 Windows PowerShell 的 Active Directory 模組」的命令提示字元中輸入 **Get-Help Set-ADServiceAccount** ，然後按下 ENTER。

## <a name="BKMK_DecommMemberHosts"></a>解除委任成員主機從現有的伺服器陣列
若要完成這些程序，至少需要 **Domain Admins** 的成員資格或是將成員從安全性群組物件移除的能力。

### <a name="step-1-remove-member-host-from-gmsa"></a>步驟 1：將成員主機從 gMSA 移除
如果使用安全性群組來管理成員主機，移除的電腦帳戶已解除委任之的成員主機從 gMSA 成員主機會使用下列方法之一的成員的安全性群組。

-   方法 1：Active Directory 使用者和電腦

    如需有關如何使用這個方法的程序，請參閱使用 Windows 介面 [刪除電腦帳戶](https://technet.microsoft.com/library/cc754624.aspx) ，以及 [管理 Active Directory 管理中心的不同網域](manage-different-domains-in-active-directory-administrative-center.md)。

-   方法 2：drsm

    如需有關如何使用這個方法的程序，請參閱使用命令列 [刪除電腦帳戶](https://technet.microsoft.com/library/cc754624.aspx) 。

-   方法 3：Windows PowerShell Active Directory Cmdlet Remove-ADPrincipalGroupMembership

    如需有關如何執行這個方法的詳細資訊，請參閱 TechNet 文件庫中的  [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) ，或是在「適用於 Windows PowerShell 的 Active Directory 模組」的命令提示字元中輸入 **Get-Help Remove-ADPrincipalGroupMembership** ，然後按下 ENTER。

如果列出電腦帳戶，請抓取現有的帳戶，然後新增除了移除之電腦帳戶以外的所有帳戶。

若要完成此程序，至少需要 **Domain Admins**、 **Account Operators**的成員資格或是管理 msDS-GroupManagedServiceAccount 物件的能力。 如需使用適當帳戶和群組成員資格的詳細資料，請參閱＜本機與網域的預設群組＞。

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>使用 Set-ADServiceAccount Cmdlet 來移除成員主機

1.  在 Windows Server 2012 網域控制站，請從工作列執行 Windows PowerShell。

2.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **Get-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **Set-ADServiceAccount [-Name] <string> -PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal[]>**

|參數|字串|範例|
|-------|-----|------|
|名稱|帳戶的名稱|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|成員主機的電腦帳戶或成員主機所屬的安全性群組|Host1、Host3|

**範例**

例如，若要移除成員主機，請輸入下列命令，然後按下 ENTER。

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1,Host3

```

### <a name="BKMK_RemoveGMSA"></a>步驟 2:將群組受管理的服務帳戶從系統移除
使用 Uninstall-ADServiceAccount 或主機系統上的 NetRemoveServiceAccount API 將快取 gMSA 認證從成員主機移除。

若要完成這些程序，至少需要 **Administrators**的成員資格或同等權限。

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>使用 Uninstall-ADServiceAccount Cmdlet 來移除 gMSA

1.  在 Windows Server 2012 網域控制站，請從工作列執行 Windows PowerShell。

2.  在 Windows PowerShell Active Directory 模組的命令提示字元中，輸入下列命令，然後按 ENTER 鍵：

    **Uninstall-ADServiceAccount < ADServiceAccount>**

    **範例**

    例如，若要為名為 ITFarm1 的 gMSA 移除快取的認證，請輸入下列命令，然後按 ENTER 鍵：

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

如需有關 Uninstall-ADServiceAccount Cmdlet 的詳細資訊，請在「適用於 Windows PowerShell 的 Active Directory 模組」的命令提示字元中輸入 **Get-Help Uninstall-ADServiceAccount**，然後按 ENTER 鍵，或參閱 TechNet 網站上的 [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx)資訊。



## <a name="BKMK_Links"></a>另請參閱

-   [群組受管理的服務帳戶概觀](group-managed-service-accounts-overview.md)


