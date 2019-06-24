---
title: 在 Windows Server Essentials 中設定 DirectAccess
description: 描述如何使用 Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2081473500a08776a1dc81a4fa443696b6fde0d6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433461"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>在 Windows Server Essentials 中設定 DirectAccess

>適用於：Windows Server 2016 Essentials、 Windows Server 2012 R2 Essentials 中，Windows Server 2012 Essentials

本主題提供讓您順暢地連線到您的組織網路從任何具備網際網路的遠端位置不須建立的行動工作人員的 Windows Server Essentials 中設定 DirectAccess 的逐步指示虛擬私人網路 (VPN) 連線。 DirectAccess 可以讓行動工作者無論在辦公室內外的相同連線體驗從他們的 Windows 8.1，Windows 8 和 Windows 7 電腦。  
  
 在 Windows Server Essentials 中，如果網域包含一部以上的 Windows Server Essentials 伺服器，DirectAccess 必須設定網域控制站上。  
  
> [!NOTE]
>  本主題提供您的 Windows Server Essentials 伺服器時的網域控制站設定 DirectAccess 的指示。 如果 Windows Server Essentials 的伺服器是網域成員，請依照下列指示中的網域成員上設定 DirectAccess[將 DirectAccess 加入現有的遠端存取 (VPN) 部署](https://technet.microsoft.com/library/jj574220.aspx)改。  
  
## <a name="process-overview"></a>程序概觀  
 若要在 Windows Server Essentials 中設定 DirectAccess，請完成下列步驟。  
  
> [!IMPORTANT]
>  本指南中使用的程序在 Windows Server Essentials 中設定 DirectAccess 之前，您必須在伺服器上啟用 VPN。 如需相關指示，請參閱 <<c0> [ 管理 VPN](Manage-VPN-in-Windows-Server-Essentials.md)。  
  
-   [步驟 1：將遠端存取管理工具新增至您的伺服器](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [步驟 2：將伺服器的網路介面卡位址變更為靜態 IP 位址](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [步驟 3：準備網路位置伺服器憑證和 DNS 記錄](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [步驟 3a:完整權限授予給 Authenticated Users，Web 伺服器的憑證範本](#BKMK_GrantFullPermissions)  
  
    -   [步驟 3b：註冊網路位置伺服器，無法從外部網路解析的一般名稱的憑證](#BKMK_EnrollaCertificate)  
  
    -   [步驟 3c：加入新的主機上的 DNS 伺服器，並將它對應到 Windows Server Essentials 伺服器位址](#BKMK_MapNewHosttoServerAddress)  
  
-   [步驟 4：建立 DirectAccess 用戶端電腦的安全性群組](#BKMK_AddSecurityGroup)  
  
-   [步驟 5：啟用和設定 DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [步驟 5a:使用 「 遠端存取管理主控台啟用 DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [步驟 5b:移除 RRAS GPO (只有 Windows Server Essentials) 中的 無效的 IPv6Prefix](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [步驟 5c:讓執行 Windows 7 企業版使用 DirectAccess 的用戶端電腦](#BKMK_Step4cWindows7Setup)  
  
    -   [步驟 5d:設定網路位置伺服器](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [步驟 5e:新增登錄機碼，在建立 IPsec 通道時略過 CA 憑證](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [步驟 6：設定 DirectAccess 伺服器的名稱解析原則表格設定](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [步驟 7：設定 DirectAccess 伺服器 Gpo 的 TCP 和 UDP 防火牆規則](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [步驟 8：為接聽 IP-HTTPS 介面將 DNS64 設定變更](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [步驟 9:保留 WinNat 服務的連接埠](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [步驟 10:重新啟動 WinNat 服務](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [附錄：使用 Windows PowerShell 設定 DirectAccess](#BKMK_AppendixBPowerShellScript)提供可供您執行 DirectAccess 設定的 Windows PowerShell 指令碼。  
  
##  <a name="BKMK_AddRAM"></a> 步驟 1:將遠端存取管理工具新增到您的伺服器  
  
#### <a name="to-add-remote-access-management-tools"></a>新增遠端存取管理工具  
  
1.  在 伺服器 [開始] 頁面的左下角，按一下 [伺服器管理員]  圖示。  
  
     在 Windows Server Essentials 中，您必須搜尋伺服器管理員加以開啟。 在 [開始] 頁面中，輸入 **Server Manager**，然後在搜尋結果中按一下 [伺服器管理員]  。 如果要將伺服器管理員固定至 開始 頁面，在搜尋結果中以滑鼠右鍵按一下 伺服器管理員，然後按一下 釘選到 開始 畫面  。  
  
2.  如果顯示 [使用者帳戶控制]  警告訊息，按一下 [是]  。  
  
3.  在 [伺服器管理員] 儀表板中按一下 [管理]  ，然後按一下 [新增角色及功能]  。  
  
4.  在 [新增角色及功能精靈] 中，執行下列動作：  
  
    1.  在 [安裝類型]  頁面上，按一下 [角色型或功能型安裝]  。  
  
    2.  在上**伺服器選取項目頁面**(或**選取目的地伺服器**Windows Server Essentials 中的頁面)，按一下 **從伺服器集區選取伺服器**。  
  
    3.  在 [功能]  頁面上，展開 [遠端伺服器管理工具 (已安裝)]  ，展開 [遠端存取管理工具 (已安裝)]  ，展開 [角色管理工具 (已安裝)]  ，展開 [遠端存取管理工具]  ，然後選取 [遠端存取 GUI 和命令列工具]  。  
  
    4.  遵循指示以完成精靈。  
  
##  <a name="BKMK_AddStaticIP"></a> 步驟 2:將伺服器的網路介面卡位址變更為靜態 IP 位址  
 DirectAccess 需要使用靜態 IP 位址的介面卡。 您需要變更伺服器上區域網路介面卡的 IP 位址。  
  
#### <a name="to-add-a-static-ip-address"></a>新增靜態 IP 位址  
  
1.  在 [開始] 頁面中，開啟 [控制台]  。  
  
2.  按一下 [網路和網際網路]  ，然後按一下 [檢視網路狀態及工作]  。  
  
3.  在 [網路和共用中心]  的工作窗格中，按一下 [變更介面卡設定]  。  
  
4.  在區域網路介面卡上按一下滑鼠右鍵，然後按一下 [內容]  。  
  
5.  在 [網路功能]  索引標籤中，按一下 [網際網路通訊協定第 4 版 (TCP/IPv4)]  ，然後按一下 [內容]  。  
  
6.  在 [一般]  索引標籤上，按一下 [使用下列 IP 位址]  ，然後輸入您要使用的 IP 位址。  
  
     [子網路遮罩]  方塊中會自動顯示子網路遮罩的預設值。 接受預設值，或輸入您要使用的子網路遮罩。  
  
7.  在 [預設閘道]  方塊中，輸入預設閘道的 IP 位址。  
  
8.  在 [慣用 DNS 伺服器]  方塊中，輸入 DNS 伺服器的 IP 位址。  
  
    > [!NOTE]
    >  使用 DHCP 指派給您的網路介面卡的 IP 位址 (例如，192.168.X.X)，不要使用回送網路 (例如，127.0.0.1)。 如果要查詢指派的 IP 位址，請在命令提示字元執行 **ipconfig** 。  
  
9. 在 [其他 DNS 伺服器]  方塊中，輸入其他 DNS 伺服器的 IP 位址 (如果有的話)。  
  
10. 按一下 [確定]  ，然後按一下 [關閉]  。  
  
> [!IMPORTANT]
>  務必設定路由器將連接埠 80 和 443 轉送到伺服器的新靜態 IP 位址。  
  
##  <a name="BKMK_DNS"></a> 步驟 3:準備網路位置伺服器的憑證和 DNS 記錄  
 如果要準備網路位置伺服器的憑證和 DNS 記錄，請執行下列工作：  
  
-   [步驟 3a:完整權限授予給 Authenticated Users，Web 伺服器的憑證範本](#BKMK_GrantFullPermissions)  
  
-   [步驟 3b：註冊網路位置伺服器，無法從外部網路解析的一般名稱的憑證](#BKMK_EnrollaCertificate)  
  
-   [步驟 3c：加入新的主機上的 DNS 伺服器，並將它對應到 Windows Server Essentials 伺服器位址。](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a> 步驟 3a:完整權限授予給 Authenticated Users，Web 伺服器的憑證範本  
 您第一項工作是授與來驗證使用者的憑證授權單位中的 Web 伺服器的憑證範本完整權限。  
  
####  <a name="BKMK_ToGrantFullPermissions"></a> 若要完整權限授予給 Authenticated Users，Web 伺服器的憑證範本  
  
1.  在 [開始]  頁面上，開啟 [憑證授權單位]  。  
  
2.  在主控台樹狀目錄中下,**憑證授權單位 （本機）** ，展開 **< 伺服器名稱\>-CA**，以滑鼠右鍵按一下**憑證範本**，然後按一下**管理**。  
  
3.  在 [憑證授權單位 (本機)]  中的 [網頁伺服器]  上按一下滑鼠右鍵，然後按一下 [內容]  。  
  
4.  在 [網頁伺服器] 內容的 [安全性]  索引標籤上，按一下 [已驗證使用者]  ，選取 [完全控制]  ，然後按一下 [確定]  。  
  
5.  重新啟動 [Active Directory 憑證服務]  。 在 [控制台] 中，開啟 [檢視本機服務]  。 在服務清單中，以滑鼠右鍵按一下 [Active Directory 憑證服務]  ，然後按一下 [重新啟動]  。  
  
###  <a name="BKMK_EnrollaCertificate"></a> 步驟 3b:以無法從外部網路解析的一般名稱註冊網路位置伺服器的憑證  
 接著，以無法從外部網路解析的一般名稱註冊網路位置伺服器的憑證。  
  
####  <a name="BKMK_ToEnrollaCertificate"></a> 若要註冊網路位置伺服器的憑證  
  
1.  在 [開始]  頁面上，開啟 [mmc]  (Microsoft 管理主控台)。  
  
2.  如果出現 [使用者帳戶控制]  警告訊息，按一下 [是]  。  
  
     此時會開啟 Microsoft Management Console (MMC)。  
  
3.  在 [檔案]  功能表中，按一下 [新增/移除嵌入式管理單元]  。  
  
4.  在 [新增或移除嵌入式管理單元]  方塊中，按一下 [憑證]  ，然後按一下 [新增]  。  
  
5.  在 [憑證嵌入式管理單元]  頁面上，按一下 [電腦帳戶]  ，然後按 [下一步]  。  
  
6.  在 [選取電腦]  頁面上，依序按一下 [本機電腦]  、[完成]  ，然後按一下 [確定]  。  
  
7.  在主控台樹狀目錄中，展開 [憑證 (本機電腦)]  ，展開 [個人]  ，以滑鼠右鍵按一下 [憑證]  ，然後在 [所有工作]  中按一下 [要求新憑證]  。  
  
8.  當 [憑證註冊精靈] 出現時，按一下 [下一步]  。  
  
9. 在 [選取憑證註冊原則]  頁面上，按一下 [下一步]  。  
  
10. 在 [要求憑證]  頁面上，選取 [網頁伺服器]  核取方塊，然後按一下 [需要更多資訊才能註冊此憑證]  。  
  
11. 在 [憑證內容]  方塊中，為 [主體名稱]  輸入下列設定：  
  
    1.  對於 [類型]  ，請選取 [一般名稱]  。  
  
    2.  在 [值]  輸入網路位置伺服器的名稱 (例如，DirectAccess-NLS.contoso.local)，然後按一下 [新增]  。  
  
    3.  按一下 [確定]  ，然後按一下 [註冊]  。  
  
12. 當憑證註冊完成時，按一下 [完成]  。  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a> 步驟 3c:在 DNS 伺服器新增主機，並將它對應到 Windows Server Essentials 伺服器位址  
 若要完成 DNS 設定，DNS 伺服器上加入新的主機，並將它對應到 Windows Server Essentials 伺服器位址。  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a> 新主機對應到 Windows Server Essentials 伺服器位址  
  
1.  在 [開始] 頁面中，開啟 [DNS 管理員]。 如果要開啟 [DNS 管理員]，請搜尋 **dnsmgmt.msc**，然後在結果中按一下 [dnsmgmt.msc]  。  
  
2.  在 DNS 管理員主控台樹狀目錄中，展開 本機伺服器中，展開**正向對應區域**，以滑鼠右鍵按一下含有伺服器網域尾碼，該區域，然後按一下**新增主機 （A 或 AAAA）** 。  
  
3.  輸入伺服器的名稱和 IP 位址 (例如，DirectAccess-NLS.contoso.local) 以及對應的伺服器位址 (例如，192.168.x.x)。  
  
4.  依序按一下 [新增主機]  、[確定]  ，然後按一下 [完成]  。  
  
##  <a name="BKMK_AddSecurityGroup"></a> 步驟 4:為 DirectAccess 用戶端電腦建立安全性群組  
 接下來，請建立要用於 DirectAccess 用戶端電腦的安全性群組，然後將電腦帳戶新增至該群組。  
  
#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>為使用 DirectAccess 的用戶端電腦新增安全性群組  
  
1. 在 [伺服器管理員儀表板] 中，按一下 [工具]  ，然後按一下 [Active Directory 使用者和電腦]  。  
  
   > [!NOTE]
   >  如果在 [工具]  功能表上看不到 [Active Directory 使用者和電腦]  ，則需要安裝此功能。 若要安裝 Active Directory 使用者和群組，請以系統管理員身分執行下列 Windows PowerShell Cmdlet：`Install-WindowsFeature RSAT-ADDS-Tools`。 如需詳細資訊，請參閱 [安裝或移除遠端伺服器管理工具套件](https://technet.microsoft.com/library/cc730825.aspx)。  
  
2. 在主控台樹狀目錄中，展開伺服器，以滑鼠右鍵按一下 [使用者]  ，按一下 [新增]  ，然後按一下 [群組]  。  
  
3. 輸入群組名稱、範圍群組和群組類型 (建立安全性群組)，然後按一下 [確定]  。  
  
   新的安全性群組就會新增到 [使用者]  資料夾。  
  
#### <a name="to-add-computer-accounts-to-the-security-group"></a>將電腦帳戶新增至安全性群組  
  
1.  在 [伺服器管理員儀表板] 中，按一下 [工具]  ，然後按一下 [Active Directory 使用者和電腦]  。  
  
2.  在主控台樹狀目錄中，展開伺服器，然後按一下 [使用者]  。  
  
3.  在伺服器上的使用者帳戶和安全性群組清單中，以滑鼠右鍵按一下您為 DirectAccess 建立的安全性群組，然後按一下 [內容]  。  
  
4.  在 [成員]  索引標籤上，按一下 [新增]  。  
  
5.  在對話方塊中，輸入您想要新增到群組的電腦帳戶名稱，並以分號 (;) 分隔名稱。 然後按一下 [檢查名稱]  。  
  
6.  驗證電腦帳戶後，按一下 [確定]  。 然後再按一下 [確定]  。  
  
> [!NOTE]
>  您也可以使用電腦帳戶內容中的 [隸屬於]  索引標籤，將帳戶新增到安全性群組。  
  
##  <a name="BKMK_EnableConfigureDA"></a> 步驟 5:啟用和設定 DirectAccess  
 若要啟用在 Windows Server Essentials 中設定 DirectAccess，您必須完成下列步驟：  
  
-   [步驟 5a:使用 「 遠端存取管理主控台啟用 DirectAccess](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [步驟 5b:移除 RRAS GPO (只有 Windows Server Essentials) 中的 無效的 IPv6Prefix](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [步驟 5c:讓執行 Windows 7 企業版使用 DirectAccess 的用戶端電腦](#BKMK_Step4cWindows7Setup)  
  
-   [步驟 5d:設定網路位置伺服器](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [步驟 5e:新增登錄機碼，在建立 IPsec 通道時略過 CA 憑證](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a> 步驟 5a:使用遠端存取管理主控台啟用 DirectAccess  
 本節提供逐步指示來啟用 Windows Server Essentials 中的 DirectAccess。 如果您尚未在伺服器上設定 VPN，您應在此程序開始前先行設定。 如需相關指示，請參閱 <<c0> [ 管理 VPN](Manage-VPN-in-Windows-Server-Essentials.md)。  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>使用遠端存取管理主控台啟用 DirectAccess  
  
1.  在 [開始] 頁面中，開啟 [遠端存取管理]  。  
  
2.  在 [啟用 DirectAccess 精靈] 中，執行下列動作：  
  
    1.  檢閱 [DirectAccess 先決條件]  ，按一下 [下一步]  。  
  
    2.  在 [選取群組]  索引標籤上，新增您稍早為 DirectAccess 用戶端建立的安全性群組。 (如果您尚未建立安全性群組，請參閱[步驟 4:建立安全性群組的 DirectAccess 用戶端電腦](#BKMK_AddSecurityGroup)如需相關指示。)  
  
    3.  如果您想要讓攜帶型電腦使用 DirectAccess 從遠端存取伺服器，請在 [選取群組]  索引標籤上，按一下 [僅針對攜帶型電腦啟用 DirectAccess]  ，然後按 [下一步]  。  
  
    4.  在 [網路拓撲]  中，選取伺服器的拓撲，然後按 [下一步]  。  
  
    5.  在 [DNS 尾碼搜尋清單]  中，視需要新增用戶端電腦的其他 DNS 尾碼，然後按 [下一步]  。  
  
        > [!NOTE]
        >  根據預設，啟用 DirectAccess 精靈已經新增目前網域的 DNS 尾碼。 但是，您可以視需要新增更多尾碼。  
  
    6.  檢閱要套用的群組原則物件 (GPO)，並視需要進行修改。  
  
    7.  按 [下一步]  ，然後按一下 [完成]  。  
  
    8.  以提升的權限執行下列 Windows PowerShell 命令來重新啟動遠端存取管理服務：  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a> 步驟 5b:移除 RRAS GPO (只有 Windows Server Essentials) 中的 無效的 IPv6Prefix  
  本節適用於執行 Windows Server Essentials 的伺服器。  
  
 以系統管理員身分開啟 Windows PowerShell，然後執行下列命令：  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a> 步驟 5c:讓執行 Windows 7 企業版使用 DirectAccess 的用戶端電腦  
 如果您有執行 Windows 7 企業版的用戶端電腦，請完成下列程序，以從那些電腦啟用 DirectAccess。  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>若要啟用 Windows 7 企業版電腦使用 DirectAccess  
  
1.  在伺服器的 [開始] 畫面，開啟**遠端存取管理**。  
  
2.  在 [遠端存取管理] 主控台中，按一下 [設定]  。 然後在 [設定詳細資料]  窗格的 [步驟 2]  下方，按一下 [編輯]  。  
  
     [遠端存取伺服器安裝精靈] 便會開啟。  
  
3.  在 **驗證**索引標籤上，選擇將做為受信任的根憑證 （您可以選擇 Windows Server Essentials 伺服器的 CA 憑證） 的憑證授權單位 (CA) 憑證。 按一下 [啟用 Windows 7 用戶端電腦透過 DirectAccess 進行連線]  ，然後按一下 [下一步]  。  
  
4.  遵循指示以完成精靈。  
  
> [!IMPORTANT]
>  沒有已知的問題，如果 Windows Server Essentials 伺服器未隨附預先安裝 UR1，透過 DirectAccess 連線的 Windows 7 企業版電腦。 如果要在該環境中啟用 DirectAccess 連線，您必須執行下列額外步驟：  
> 
> 1. 安裝中所述的 hotfix [Microsoft 知識庫 (KB) 文件 2796394](https://support.microsoft.com/kb/2796394) Windows Server Essentials 伺服器上。 然後重新啟動伺服器。  
>    2. 然後安裝中所述的 hotfix [Microsoft 知識庫 (KB) 文件 2615847](https://support.microsoft.com/kb/2615847)每一部 Windows 7 電腦上。  
> 
>    Windows Server Essentials 中已解決此問題。  
  
###  <a name="BKMK_NLS"></a> 步驟 5d:設定網路位置伺服器  
 本節提供設定網路位置伺服器各項設定的逐步指示。  
  
> [!NOTE]
>  在開始之前，將內容複製 < SystemDrive\>\inetpub\wwwroot 資料夾 < SystemDrive\>files\windows Server\Bin\WebApps\Site\insideoutside 資料夾。 也將 default.aspx 檔案複製 < SystemDrive\>files\windows Server\Bin\WebApps\Site 資料夾至 < 系統磁碟機\>files\windows Server\Bin\WebApps\Site\insideoutside 資料夾。  
  
##### <a name="to-configure-the-network-location-server"></a>設定網路位置伺服器  
  
1.  在 [開始] 頁面中，開啟 [遠端存取管理]  。  
  
2.  在 [遠端存取管理] 主控台中，按一下 [設定]  ，然後在 [遠端存取設定]  詳細資料窗格的 [步驟 3]  中，按一下 [編輯]  。  
  
3.  在遠端存取伺服器安裝精靈，在**網路位置伺服器**索引標籤上，選取**網路位置伺服器部署於遠端存取伺服器**，然後選取 已使用的憑證先前發行 (在[步驟 3:準備網路位置伺服器憑證和 DNS 記錄](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS))。  
  
4.  依照指示完成精靈，然後按一下 [完成]  。  
  
###  <a name="BKMK_CA"></a> 步驟 5e:新增登錄機碼，在建立 IPsec 通道時略過 CA 憑證  
 下一步是設定伺服器設在建立 IPsec 通道時略過 CA 憑證。  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>新增登錄機碼以略過 CA 憑證  
  
1.  在 [開始] 頁面中，開啟 [regedit]  (登錄編輯程式)。  
  
2.  在 [登錄編輯程式] 中，依序展開 [HKEY_LOCAL_MACHINE]  、[系統]  、[CurrentControlSet]  、[服務]  、[IKEEXT]  。  
  
3.  在 [IKEEXT]  下方，以滑鼠右鍵按一下 [參數]  ，按一下 [新增]  ，然後按一下 [DWORD (32 位元) 值]  .  
  
4.  將新增的值重新命名為 **ikeflags**。  
  
5.  連按兩下 [ikeflags]  ，將 [類型]  設為 [十六進位]  ，將值設為 **8000**，然後按一下 [確定]  。  
  
> [!NOTE]
>  您可以提升的權限使用下列 Windows PowerShell 命令來新增此登錄機碼：  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a> 步驟 6:設定 DirectAccess 伺服器的名稱解析原則表格設定  
 本節提供為 DirectAccess 用戶端 GPO 編輯內部位址 (例如，尾碼是 contoso.local 的項目) 的名稱解析原則表格 (NPRT) 項目，然後設定 IPHTTPS 介面位址的指示。  
  
#### <a name="to-configure-name-resolution-policy-table-entries"></a>設定名稱解析原則表格項目  
  
1.  在 [開始] 頁面中，開啟 [群組原則管理]  。  
  
2.  在 [群組原則管理] 主控台中，按一下預設樹系及網域，用滑鼠右鍵按一下 [DirectAccess 用戶端設定]  ，然後按一下 [編輯]  。  
  
3.  依序按一下 [電腦設定]  、[原則]  、[Windows 設定]  ，然後按一下 [名稱解析原則]  。 選擇命名空間與您的 DNS 尾碼相同的項目，然後按一下 [編輯規則]  。  
  
4.  按一下 [DirectAccess 的 DNS 設定]  索引標籤，然後選取 [啟用此規則中 DirectAccess 的 DNS 設定]  。 在 DNS 伺服器清單中新增 IP-HTTPS 介面的 IPv6 位址。  
  
    > [!NOTE]
    >  您可以使用以下 Windows PowerShell 命令取得 IPv6 位址：  
    >   
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`  
  
##  <a name="BKMK_TCPUDP"></a> 步驟 7:設定 DirectAccess 伺服器 GPO 的 TCP 和 UDP 防火牆規則  
 本節包含設定 DirectAccess 伺服器 GPO 的 TCP 和 UDP 防火牆規則的逐步指示。  
  
#### <a name="to-configure-firewall-rules"></a>設定防火牆規則  
  
1.  在 [開始] 頁面中，開啟 [群組原則管理]  。  
  
2.  在 [群組原則管理] 主控台中，按一下預設樹系及網域，用滑鼠右鍵按一下 [DirectAccess 伺服器設定]  ，然後按一下 [編輯]  。  
  
3.  依序按一下 [電腦設定]  、[原則]  、[Windows 設定]  、[安全性設定]  、[具有進階安全性的 Windows 防火牆]  、下一層的 [具有進階安全性的 Windows 防火牆]  ，然後按一下 [輸入規則]  。 在 [網域名稱伺服器 (TCP-In)]  上按一下滑鼠右鍵，然後按一下 [內容]  。  
  
4.  按一下 [領域]  索引標籤，然後在 [本機 IP 位址]  清單中，新增 IP-HTTPS 介面的 IPv6 位址。  
  
5.  在 [網域名稱伺服器 (UDP-In)]  重複相同的程序。  
  
##  <a name="BKMK_DNS64"></a> 步驟 8:將 DNS64 設定變更為接聽 IP-HTTPS 介面  
 您必須使用以下 Windows PowerShell 命令，將 DNS64 設定變更為接聽 IP-HTTPS 介面。  
  
```powershell  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a> 步驟 9:保留 WinNat 服務的連接埠  
 使用下列 Windows PowerShell 命令以保留 WinNat 服務的連接埠。 Windows Server Essentials 伺服器的實際 IPv4 位址取代"192.168.1.100"。  
  
```powershell  
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  為避免與應用程式的連接埠衝突，請確定您為 WinNat 服務保留的連接埠範圍未包含連接埠 6602。  
  
##  <a name="BKMK_WinNAT"></a> 步驟 10:重新啟動 WinNat 服務  
 執行以下 Windows PowerShell 命令以重新啟動 Windows NAT 驅動程式 (WinNat) 服務。  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a> 附錄：使用 Windows PowerShell 安裝 DirectAccess  
 本節說明如何使用 Windows PowerShell 安裝與設定 DirectAccess。  
  
### <a name="preparation"></a>準備  
 開始設定 DirectAccess 的伺服器之前，您必須完成以下各項：  
  
1.  請依照下列中的程序[步驟 3:準備網路位置伺服器憑證和 DNS 記錄](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)名為的憑證**Directaccess-nls.contoso.com** (其中**contoso.com**實際取代內部網域名稱），並將網路位置伺服器 (NLS) 的 DNS 記錄。  
  
2.  在 Active Directory 新增名為 **DirectAccessClients** 的安全性群組，然後新增您要為其提供 DirectAccess 功能的用戶端電腦。 如需詳細資訊，請參閱[步驟 4:建立安全性群組的 DirectAccess 用戶端電腦](#BKMK_AddSecurityGroup)。  
  
### <a name="commands"></a>命令  
  
> [!IMPORTANT]
>  在 Windows Server Essentials 中，您不需要移除不必要的 IPv6 首碼 GPO。 刪除含有下列標籤的程式碼區段： `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`。  
  
```powershell  
# Add Remote Access role if not installed yet  
$ra = Get-WindowsFeature RemoteAccess  
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }  
  
# Server may need to restart if you installed RemoteAccess role in the above step  
  
# Set the internet domain name to access server, replace contoso.com below with your own domain name  
$InternetDomain = "www.contoso.com"  
#Set the SG name which you create for DA clients  
$DaSecurityGroup = "DirectAccessClients"  
#Set the internal domain name  
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name  
  
# Set static IP and DNS settings  
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"  
$CurrentIP = $NetConfig.IPAddress[0]  
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}  
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)  
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)  
$NetConfig.SetDNSServerSearchOrder($CurrentIP)  
  
# Get physical adapter name and the certificate for NLS server  
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId  
$Certs = dir cert:\LocalMachine\My  
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}  
  
# Add regkey to bypass CA cert for IPsec authentication  
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000  
  
# Install DirectAccess.   
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force  
  
#Restart Remote Access Management service  
Restart-Service RaMgmtSvc  
  
# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO   
  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
  
# Enable client computers running Windows 7 to use DirectAccess  
$allcertsinroot = dir cert:\LocalMachine\root  
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}  
Set-DAServer -IPSecRootCertificate $rootcert[0]  
Set -DAClient -OnlyRemoteComputers Disabled -Downlevel Enabled  
  
#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients  
Add-DAClient -SecurityGroupNameList $DaSecurityGroup   
Remove-DAClient -SecurityGroupNameList "Domain Computers"  
  
# Gather DNS64 IP address information  
$Remoteaccess = get-remoteaccess  
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128  
$DNS64IP=$IPInterface[1].IPaddress  
$Natconfig = Get-NetNatTransitionConfiguration  
  
# Configure TCP and UDP firewall rules for the DirectAccess server GPO  
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'  
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
  
# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain  
$Suffix = '.' + $InternalDomain  
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP  
  
# Change the DNS64 configuration to listen to IP-HTTPS interface  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
  
# Copy the necessary files to NLS site folder  
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y  
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y  
  
# Reserve ports for the WinNat service  
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
  
# Restart the WinNat service  
Restart-Service winnat  
```  
  
## <a name="see-also"></a>另請參閱  
  
-   [管理隨處存取](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [管理 Windows Server Essentials](Manage-Windows-Server-Essentials.md)