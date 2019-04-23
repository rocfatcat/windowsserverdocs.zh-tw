---
title: 步驟 2 設定 APP1
description: 本主題是測試實驗室指南-使用 OTP 驗證和 RSA SecurID for Windows Server 2016 的示範 DirectAccess 的一部分
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19a7a4a6-9a04-42ea-a5d0-ecb28a34dbaa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 612d3f4e9be71f60811b4499d9bdb8ae3bd217e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847489"
---
# <a name="step-2-configure-app1"></a>步驟 2 設定 APP1

>適用於：Windows Server （半年通道），Windows Server 2016

您可以使用下列步驟來準備 OTP 支援 APP1:  
  
1. 若要建立及部署憑證範本用來登入 OTP 憑證要求。 設定用來登入 OTP 憑證要求的憑證範本。  
  
2. 若要建立並部署公司的 CA 所發行的 OTP 憑證的憑證範本。 設定公司的 CA 所發行的 OTP 憑證的憑證範本。  
  
> [!WARNING]  
> 這個測試實驗室指南的設計，包括基礎結構伺服器，例如網域控制站和執行 Windows Server 2012 R2 或 Windows Server 2012 的憑證授權單位 (CA)。 使用這個測試實驗室指南設定執行其他作業系統的基礎結構伺服器尚未經過測試，並設定其他作業系統的指示不包含在本指南中。  
  
## <a name="DAOTPRA"></a>建立及部署憑證範本用來登入 OTP 憑證要求  
  
1.  執行**certtmpl.msc**，然後按 ENTER 鍵。  
  
2.  在 [憑證範本] 主控台，在詳細資料窗格中，以滑鼠右鍵按一下**電腦**範本，然後按**複製範本**。  
  
3.  在上**新範本的內容**對話方塊的 **相容性**索引標籤**憑證授權單位**清單中，選取您想，作業系統在**產生的變更**對話方塊中，按一下**確定**。 在 **憑證收件者**清單中，選取您想，作業系統並在**產生的變更**對話方塊中，按一下**確定**。  
  
4.  在 **新範本的內容** 對話方塊中，按一下**一般** 索引標籤。  
  
5.  在 **一般**索引標籤中，於**範本顯示名稱**，型別**DAOTPRA**。 設定**有效期**為 2 天，並將**續約期限**為 1 天。 如果**憑證範本**就會顯示警告，請按一下**確定**。  
  
6.  按一下 [安全性]  索引標籤，然後按一下 [新增] 。  
  
7.  在 [**選取使用者、 電腦、 服務帳戶或群組**] 對話方塊中，按一下**物件類型**。 在上**物件類型**對話方塊中，選取**電腦**，然後按一下 **確定**。 在 **輸入物件名稱來選取**方塊中，輸入**EDGE1**，按一下**確定**，然後在**允許**欄中，選取**讀取**，**註冊**，以及**自動註冊**核取方塊。 按一下  **Authenticated Users**，選取**讀取**底下的核取方塊**允許**資料行，並清除所有其他核取方塊。 按一下  **Domain Computers**，並取消核取**註冊**之下**允許**資料行。 按一下  **Domain Admins**並**Enterprise Admins** ，按一下 **完全控制**下**允許**兩個資料行。 按一下 **[套用]**。  
  
8.  按一下 **主體名稱**索引標籤，然後再按一下**Active Directory 資訊來建立**。 在 **主體名稱格式：** 清單中，選取**DNS 名稱**，請確定**DNS 名稱** 方塊已核取，然後按一下 **套用**。  
  
9. 按一下 **延伸模組**索引標籤上，選取**應用程式原則**，然後按一下 **編輯**。 移除所有現有的應用程式原則。 按一下 **新增**，然後在**新增應用程式原則** 對話方塊中，按一下 **新增**，輸入**DA OTP RA**中**名稱：** 欄位和**1.3.6.1.4.1.311.81.1.1**中**物件識別碼：** 欄位，然後按一下 **確定**。 在 [**新增應用程式原則**] 對話方塊中，按一下**確定**。 在 **編輯應用程式原則延伸**，按一下**確定**。 在 [**新範本的內容**] 對話方塊中，按一下**確定**。  
  
## <a name="DAOTPLogon"></a>若要建立和部署公司的 CA 所發行的 OTP 憑證的憑證範本  
  
1.  在 [憑證範本] 主控台，在詳細資料窗格中，以滑鼠右鍵按一下**智慧卡登入**範本，然後按**複製範本**。  
  
2.  在上**新範本的內容**對話方塊的 [**相容性**索引標籤**憑證授權單位**清單中，按一下您要使用的作業系統和**產生的變更**] 對話方塊中，按一下**確定**。 在 **憑證收件者**清單中，選取您要使用的作業系統然後在**產生的變更**對話方塊中，按一下**確定**。  
  
3.  在 **新範本的內容** 對話方塊中，按一下**一般** 索引標籤。  
  
4.  在 **一般**索引標籤中，於**範本顯示名稱**，型別**DAOTPLogon**。 中**有效期**，在下拉式清單中，按一下 [**小時**上**憑證範本**] 對話方塊中，按一下**確定**，並確定時數是設定為 1。 在 **續約期限**，型別**0**。  
  
    > [!IMPORTANT]  
    > **Windows Server 2003 CA**。 在執行 Windows Server 2003 的電腦的憑證授權單位 (CA) 的情況下，然後設定憑證範本必須在不同電腦上。 這是必要的因為設定**有效期**在小時是不可能時執行 Windows Server 2008 和 Windows Vista 之前的 Windows 版本。 如果您用來設定範本的電腦沒有安裝 Active Directory 憑證服務伺服器角色，或者它是用戶端電腦，您可能需要安裝憑證範本 嵌入式管理單元。 如需詳細資訊，請參閱 <<c0> [ 憑證範本 嵌入式管理單元安裝](https://technet.microsoft.com/library/cc732445.aspx)。  
    >   
    > **Windows Server 2008 R2 CA**。 如果您已部署執行 Windows Server 2008 R2 的憑證授權單位 (CA)，您必須設定憑證範本**續約期限**1 或 2 個小時，而**有效期**至長度超過**續約期限**，但不是能超過 4 小時。 如果您設定憑證範本**有效期**超過 4 小時透過 CA 執行 Windows Server 2008 R2 DirectAccess 安裝精靈 無法偵測的憑證範本和 DirectAccess安裝會失敗。  
  
5.  按一下 **安全性**索引標籤上，選取**Authenticated Users**，請在**允許**資料行，然後選取**讀取**和**註冊**核取方塊。 按一下 [確定] 。 按一下**Domain Admins**並**Enterprise Admins**，然後按一下**完全控制**下**允許**兩個資料行。 按一下 **[套用]**。  
  
6.  按一下 **主體名稱**索引標籤，然後再按一下**Active Directory 資訊來建立**。 在 **主體名稱格式：** 清單中，選取**完整辨別的名稱**，請確定**使用者主體名稱 (UPN)** 方塊已核取，然後按一下 **套用**.  
  
7.  按一下 **伺服器**索引標籤上，選取**不要 CA 資料庫以儲存憑證及要求**核取方塊，清除**簽發的憑證中不包含撤銷資訊**核取方塊，然後在**新範本的內容** 對話方塊中，按一下 **套用**。  
  
8.  按一下 **發行需求**索引標籤上，選取**授權簽章的這個數字：** 核取方塊，將值設為 1。 在 **簽章中必需的原則類型：** 清單中，選取**應用程式原則**，然後在**應用程式原則**清單中，選取**DA OTP RA**. 在 [**新範本的內容**] 對話方塊中，按一下**確定**。  
  
9. 按一下 **延伸模組** 索引標籤，然後在**應用程式原則**按一下 **編輯**。 刪除**用戶端驗證**，保留**核取 SmartCardLogon**，然後按一下**確定**兩次。  
  
10. 關閉 [憑證範本主控台]。  
  
11. 在 **開始**畫面上，輸入**certsrv.msc**，然後按 ENTER 鍵。  
  
12. 在 憑證授權單位主控台樹狀目錄中，展開**corp-APP1-CA-1**，按一下**憑證範本**，以滑鼠右鍵按一下**憑證範本**，指向**的新**，然後按一下**要發出的憑證範本**。  
  
13. 在憑證範本清單中，按一下  **DAOTPRA**並**DAOTPLogon**，然後按一下**確定**。  
  
14. 在主控台的 [詳細資料] 窗格應該會看到**DAOTPRA**使用的憑證範本**目的**的**DA OTP RA**而**DAOTPLogon**憑證範本，內含**目的**的**智慧卡登入**。  
  
15. 重新啟動服務。  
  
16. 關閉 [憑證授權單位] 主控台。  
  
17. 開啟提升權限的命令提示字元。 型別**CertUtil.exe-SetReg DBFlags + DBFLAGS_ENABLEVOLATILEREQUESTS**，然後按 ENTER。  
  
18. 保留 [命令提示字元] 視窗開啟以供下一個步驟。  
  

