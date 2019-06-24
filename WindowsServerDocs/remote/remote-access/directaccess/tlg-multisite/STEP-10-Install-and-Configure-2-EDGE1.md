---
title: 步驟 10 安裝及設定 2 EDGE1
description: 本主題是一部分的 「 測試實驗室指南： 示範 DirectAccess 多站台部署的 Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d98d6f7a-a2e6-45b1-9c63-08e2986a5c03
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9810d7294a2651d4811bc5969eaf6a118db8ed56
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283271"
---
# <a name="step-10-install-and-configure-2-edge1"></a>步驟 10 安裝及設定 2 EDGE1

>適用於：Windows Server （半年通道），Windows Server 2016

2-EDGE1 組態是由下列項目所組成：  
  
- 2-EDGE1 上安裝作業系統。 安裝 Windows Server 2016 中，Windows Server 2012 R2 或 Windows Server 2012 上 2 EDGE1。  
  
- 設定 TCP/IP 內容。 設定這兩個網路介面上的靜態位址 2 EDGE1。  
  
- 設定子網路之間的路由。 若要啟用的公司網路和 2 Corpnet 子網路之間的通訊，您必須設定路由。  
  
- 加入 CORP2 網域 2 EDGE1。 加入 corp2.corp.contoso.com 網域 2 EDGE1。  
  
- 取得 2 EDGE1 上的憑證。 需要 IPsec 連線，DirectAccess 用戶端與遠端存取伺服器之間，並透過 HTTPS 的用戶端連線時驗證為 IP-HTTPS 接聽程式的憑證。  
  
- 以 CORP\User1 提供存取。 使用者 CORP\User1 是遠端存取系統管理員。 若要讓此使用者將從 EDGE1 2 EDGE1 進行變更，您必須對使用者授與存取。  
  
- 安裝遠端存取角色上 2 EDGE1。 若要啟用多站台部署，您必須安裝 「 遠端存取 」 角色上 2 EDGE1。  
  
2-EDGE1 必須安裝兩張網路介面卡。  
  
## <a name="installOS"></a>2-EDGE1 上安裝作業系統  
  
1.  啟動 Windows Server 2016、 Windows Server 2012 R2 或 Windows Server 2012 的安裝。  
  
2.  請依照下列指示完成安裝，指定 Windows Server 2016、 Windows Server 2012 R2 或 Windows Server 2012 （完整安裝） 和本機系統管理員帳戶的強式密碼。 使用本機 Administrator 帳戶登入。  
  
3.  連線 2 EDGE1 至具有網際網路存取的網路，並執行 Windows Update，以針對 Windows Server 2016、 Windows Server 2012 R2 或 Windows Server 2012，安裝最新的更新，並再中斷網際網路連線。  
  
4.  以 2 Corpnet 子網路，另一個用於模擬的網際網路連線一張網路介面卡。  
  
## <a name="tcpip"></a>設定 TCP/IP 內容  
  
1.  在 伺服器管理員 主控台中，按一下**本機伺服器**，然後在**屬性**區域中下, 一步**有線乙太網路連線**，按一下連結。  
  
2.  在**網路連線**，以滑鼠右鍵按一下 連線到 2 Corpnet 子網路的網路連線後，按**重新命名**，型別**2 Corpnet**，然後按 ENTER 鍵。  
  
3.  以滑鼠右鍵按一下**2 Corpnet**，然後按一下**屬性**。  
  
4.  按一下 [網際網路通訊協定第 4 版 (TCP/IPv4)]  ，然後按一下 [內容]  。  
  
5.  按一下 [使用下列的 IP 位址]  。 在  **IP 位址**，型別**10.2.0.20**，請在**子網路遮罩**，型別**255.255.255.0**。  
  
6.  按一下 [使用下列的 DNS 伺服器位址]  。 在 **慣用 DNS 伺服器**，型別**10.2.0.1**，然後在**備用 DNS 伺服器**，類型**10.0.0.1**。  
  
7.  按一下 [進階]  ，然後按一下 [DNS]  索引標籤。  
  
8.  在 **此連線的 DNS 尾碼**，型別**corp2.corp.contoso.com**，然後按一下**確定**兩次。  
  
9. 選取 **[網際網路通訊協定第 6 版 (TCP/IPv6)]** ，然後按一下 **[屬性]** 。  
  
10. 按一下 **使用下列 IPv6 位址**。 在  **IPv6 位址**，型別**2001:db8:2::20**，請在**子網路首碼長度**，型別**64**。 按一下 **使用下列的 DNS 伺服器位址**，然後在**慣用 DNS 伺服器**，型別**2001:db8:2::1**中**備用 DNS 伺服器**，型別**2001:db8:1::1**。  
  
11. 按一下 [進階]  ，然後按一下 [DNS]  索引標籤。  
  
12. 在 **此連線的 DNS 尾碼**，型別**corp2.corp.contoso.com**，然後按一下**確定**兩次。  
  
13. 在 [ **2 公司網路內容**] 對話方塊中，按一下**關閉**。  
  
14. 在 **網路連線**視窗中，以滑鼠右鍵按一下 連線到網際網路子網路的網路連線，按一下 **重新命名**，型別**網際網路**，然後按 ENTER 鍵.  
  
15. 在 [網際網路]  按滑鼠右鍵，然後按一下 [內容]  。  
  
16. 按一下 [網際網路通訊協定第 4 版 (TCP/IPv4)]  ，然後按一下 [內容]  。  
  
17. 按一下 [使用下列的 IP 位址]  。 在  **IP 位址**，型別**131.107.0.20**。 在 [子網路遮罩]  中，輸入 **255.255.255.0**。  
  
18. 按一下 [進階]  。 在 [IP 設定]  索引標籤的 [IP 位址]  區域，按一下 [新增]  。 在上**TCP/IP 位址**對話方塊中，於**IP 位址**類型**131.107.0.21**中**子網路遮罩**類型**255.255.255.0**，然後按一下**新增**。  
  
19. 按一下 [DNS]  索引標籤。  
  
20. 在 **此連線的 DNS 尾碼**，型別**isp.example.com**，按一下**確定**兩次，然後按一下 **關閉**。  
  
21. 關閉 [網路連線]  視窗。  
  
## <a name="routing"></a>設定子網路之間的路由  
  
1.  在 **開始**畫面上，輸入**cmd.exe**，然後按 ENTER 鍵。  
  
2.  在 [命令提示字元] 視窗中，輸入下列命令。 輸入每個命令之後, 按 ENTER 鍵。  
  
    ```  
    netsh interface IPv4 add route 10.0.0.0/24 2-Corpnet 10.2.0.254  
    netsh interface IPv6 add route 2001:db8:1::/64 2-Corpnet 2001:db8:2::fe  
    ```  
  
3.  若要檢查 2 EDGE1 與 DC1 之間的網路通訊，請輸入**ping dc1.corp.contoso.com**。  
  
4.  請確認有四個回應從 IPv4 位址 10.0.0.1、 或的 IPv6 位址，2001:db8:1::1。  
  
5.  關閉 [命令提示字元] 視窗。  
  
## <a name="Join"></a>2-EDGE1 加入 CORP2 網域  
  
1.  在 伺服器管理員 主控台中，在**本機伺服器**，請在**屬性**區域中下, 一步**電腦名稱**，按一下連結。  
  
2.  在 [系統內容]  的 [電腦名稱]  索引標籤上，按一下 [變更]  。  
  
3.  在上**電腦名稱/網域變更**對話方塊中，於**電腦名稱**，型別**2 EDGE1**。 中**隸屬**，按一下**網域**，型別**corp2.corp.contoso.com**，然後按一下 **確定**。  
  
4.  如果系統提示您輸入使用者名稱和密碼，輸入**系統管理員**、 其密碼，以及然後按一下**確定**。  
  
5.  當您看見歡迎您加入 corp2.corp.contoso.com 網域 對話方塊中時，按一下**確定**。  
  
6.  當提示您必須重新啟動電腦時，按一下 [確定]  。  
  
7.  按一下 [系統內容]  對話方塊中的 [關閉]  。  
  
8.  當提示您重新啟動電腦時，請按一下 [立即重新啟動]  。  
  
9. 重新啟動電腦之後，請按一下**切換使用者**，然後按一下**其他使用者**和登入 CORP2 網域的系統管理員帳戶。  
  
## <a name="certs"></a>取得 2 EDGE1 上的憑證  
  
1.  在 **開始**畫面上，輸入**mmc.exe**，然後按 ENTER 鍵。  
  
2.  在 MMC 主控台中，按一下 [檔案]  功能表上的 [新增/移除嵌入式管理單元]  。  
  
3.  在 [新增或移除嵌入式管理單元]  對話方塊中，依序按一下 [憑證]  、[新增]  、[電腦帳戶]  、[下一步]  、[本機電腦]  、[完成]  ，然後按一下 [確定]  。  
  
4.  在 [憑證] 嵌入式管理單元的主控台樹狀目錄中，開啟**Certificates (Local Computer) \Personal**。  
  
5.  以滑鼠右鍵按一下**個人**，指向**所有工作**，然後按一下**要求新憑證**。  
  
6.  按兩次 [下一步]  。  
  
7.  上**要求憑證**頁面上，選取**Client-server Authentication**並**網頁伺服器**核取方塊，然後**的詳細資訊若要註冊此憑證需要**。  
  
8.  在上**憑證內容**對話方塊的 **主旨**索引標籤**主體名稱**區域中**類型**，選取**一般名稱**。  
  
9. 在 **值**，型別**2 edge1.contoso.com**，然後按一下**新增**。  
  
10. 在 [別名]  區域的 [類型]  中，選取 [DNS]  。  
  
11. 在 **值**，輸入**2 edge1.contoso.com**，然後按一下**新增**。  
  
12. 在上**一般**索引標籤中，於**易記名稱**，型別**IP-HTTPS 憑證**。  
  
13. 依序按一下 [確定]  、[註冊]  ，然後按一下 [完成]  。  
  
14. 在 [憑證] 嵌入式管理單元的詳細資料窗格，確認名稱 2 edge1.contoso.com 的新憑證已註冊 「 使用目的伺服器 」 驗證，新的憑證名稱 2 edge1.corp2.corp.contoso.com 與已註冊使用適用的用戶端驗證和伺服器驗證目的。  
  
15. 關閉主控台視窗。 如果提示您儲存設定時，請按一下**No**。  
  
## <a name="Access"></a>提供存取權給 CORP\User1  
  
1.  在 **開始**畫面上，輸入**compmgmt.msc**，然後按 ENTER 鍵。  
  
2.  在左窗格中，按一下**本機使用者和群組**。  
  
3.  按兩下**群組**，然後按兩下**系統管理員**。  
  
4.  在上**系統管理員屬性** 對話方塊中，按一下**新增**，然後在**選取使用者、 電腦、 服務帳戶或群組** 對話方塊中，按一下  **位置**。  
  
5.  上**位置**對話方塊中，於**位置**樹狀結構中，按一下  **corp.contoso.com**，然後按一下 **確定**。  
  
6.  在 **輸入要選取的物件名稱**型別**User1**，然後按一下  **確定**。  
  
7.  在上**系統管理員屬性** 對話方塊中，按一下**確定**。  
  
8.  關閉 [電腦管理] 視窗。  
  
## <a name="InstallDA"></a>2-EDGE1 上安裝遠端存取角色  
  
1.  在 [伺服器管理員] 主控台中，在**儀表板**，按一下**新增角色及功能**。  
  
2.  按 [下一步]  3 次，進入伺服器角色選擇畫面。  
  
3.  在 [選取伺服器角色]  對話方塊上，選取 [遠端存取]  ，按一下 [新增功能]  ，然後按 [下一步]  。  
  
4.  按 [下一步]  五次。  
  
5.  在 [確認安裝選項]  對話方塊中，按一下 [安裝]  。  
  
6.  在 [安裝進度]  對話方塊中，確認安裝成功，然後按一下 [關閉]  。  
  

