---
title: 步驟2設定 APP1
description: 本主題屬於測試實驗室指南-示範使用 OTP 驗證的 DirectAccess 和適用于 Windows Server 2016 的 RSA SecurID
manager: brianlic
ms.topic: article
ms.assetid: 19a7a4a6-9a04-42ea-a5d0-ecb28a34dbaa
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a66208ba0f7523026f9169a9544be7a8f6234c02
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944218"
---
# <a name="step-2-configure-app1"></a>步驟2設定 APP1

>適用於：Windows Server (半年度管道)、Windows Server 2016

使用下列步驟來準備 APP1 以支援 OTP：

1. 建立及部署用來簽署 OTP 憑證要求的憑證範本。 設定用來簽署 OTP 憑證要求的憑證範本。

2. 為公司 CA 所簽發的 OTP 憑證建立及部署憑證範本。 為公司 CA 所簽發的 OTP 憑證設定憑證範本。

> [!WARNING]
> 此測試實驗室指南的設計包含基礎結構伺服器，例如網域控制站和憑證授權單位單位 (執行 Windows Server 2012 R2 或 Windows Server 2012 的 CA) 。 使用此測試實驗室指南來設定執行其他作業系統的基礎結構伺服器尚未經過測試，且本指南不含設定其他作業系統的指示。

## <a name="to-create-and-deploy-a-certificate-template-used-to-sign-otp-certificate-requests"></a><a name="DAOTPRA"></a>建立及部署用來簽署 OTP 憑證要求的憑證範本

1.  執行**certtmpl.msc**，然後按 enter。

2.  在 [憑證範本] 主控台的詳細資料窗格中，以滑鼠右鍵按一下**電腦**範本，然後按一下 [**複製範本**]。

3.  在 [**新範本**的內容] 對話方塊的 [**相容性**] 索引標籤的 [**憑證授權單位**單位] 清單中，選取您想要的作業系統，然後在 [**產生的變更**] 對話方塊中按一下 **[確定**]。 在 [**憑證收件**者] 清單中，選取您想要的作業系統，然後在 [**產生的變更**] 對話方塊中按一下 **[確定]**。

4.  在 [**新範本**的內容] 對話方塊中，按一下 [**一般**] 索引標籤。

5.  在 [**一般**] 索引標籤的 [**範本顯示名稱**] 中，輸入**DAOTPRA**。 將 [**有效期間**] 設為2天，並將**更新期間**設定為1天。 如果顯示 [**憑證範本**] 警告，請按一下 **[確定]**。

6.  按一下 [安全性]**** 索引標籤，然後按一下 [新增]****。

7.  在 [**選取使用者、電腦、服務帳戶或群組**] 對話方塊中，按一下 [**物件類型**]。 在 [**物件類型**] 對話方塊中，選取 [**電腦**]，然後按一下 **[確定]**。 在 [**輸入要選取的物件名稱**] 方塊中，輸入**EDGE1**，按一下 **[確定]**，然後在 [**允許**] 欄中，選取 [**讀取**]、[**註冊**] 和 [**自動註冊**] 核取方塊。 按一下 [**已驗證的使用者**]，選取 [**允許**] 資料行底下的 [**讀取**] 核取方塊，並清除所有其他核取方塊。 按一下 [**網域電腦**]，然後取消核取 [**允許**] 欄底下的 [**註冊**]。 按一下 [ **Domain admins** ] 和 [ **Enterprise Admins** ]，然後按一下 [**允許**] 資料行底下的 [**完全控制**]。 按一下 [套用]。

8.  按一下 [**主體名稱**] 索引標籤，然後**從這個 Active Directory 資訊中**按一下 [建立]。 在 [**主體名稱格式：** ] 清單中，選取 [ **dns 名稱**]，確認已核取 [ **dns 名稱**] 方塊，**然後按一下 [** 套用]。

9. 按一下 [**擴充**功能] 索引標籤，選取 [**應用程式原則**]，然後按一下 [**編輯**] 移除所有現有的應用程式原則。 按一下 [新增]，然後在 [新增**應用程式原則**] 對話方塊**中按一下 [****新增**]，在 [**名稱：** ] 欄位中輸入**DA OTP RA** ，然後在 [**物件識別碼：** ] 欄位中輸入**1.3.6.1.4.1.311.81.1.1** ，再按一下 **[確定]**。 在 [**新增應用程式原則**] 對話方塊中，按一下 **[確定]**。 在 [**編輯應用程式原則] 延伸**模組上，按一下 **[確定]**。 在 [**新範本**的內容] 對話方塊中，按一下 **[確定**]。

## <a name="to-create-and-deploy-a-certificate-template-for-otp-certificates-issued-by-the-corporate-ca"></a><a name="DAOTPLogon"></a>建立及部署公司 CA 所發行之 OTP 憑證的憑證範本

1.  在 [憑證範本] 主控台的詳細資料窗格中，以滑鼠右鍵按一下**智慧卡登**入範本，然後按一下 [**複製範本**]。

2.  在 [**新範本**的內容] 對話方塊的 [**憑證授權單位**單位] 清單中的 [**相容性**] 索引標籤上，按一下您要使用的作業系統，然後在 [**產生的變更**] 對話方塊中按一下 **[確定**]。 在 [**憑證收件**者] 清單中，選取您要使用的作業系統，然後在 [**產生的變更**] 對話方塊中按一下 **[確定**]。

3.  在 [**新範本**的內容] 對話方塊中，按一下 [**一般**] 索引標籤。

4.  在 [**一般**] 索引標籤的 [**範本顯示名稱**] 中，輸入**DAOTPLogon**。 在 [**有效期間**] 的下拉式清單中，按一下 [**小時**]，在 [**憑證範本**] 對話方塊中按一下 **[確定]**，並確定 [小時數] 設定為1。 在 [**更新期間**] 中，輸入**0**。

    > [!IMPORTANT]
    > **Windows Server 2003 CA**。 在憑證授權單位單位 (CA) 位於執行 Windows Server 2003 的電腦上時，必須在不同的電腦上設定憑證範本。 這是必要的，因為在 Windows Server 2008 和 Windows Vista 之前執行 Windows 版本時，不可能設定以小時為單位的**有效期間**。 如果您用來設定範本的電腦未安裝 Active Directory 憑證服務伺服器角色，或者它是用戶端電腦，則您可能需要安裝 [憑證範本] 嵌入式管理單元。 如需詳細資訊，請參閱[安裝憑證範本嵌入式管理](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732445(v=ws.11))單元。
    >
    > **Windows Server 2008 R2 CA**。 如果您已部署執行 Windows Server 2008 R2 (CA) 的憑證授權單位單位，您必須將憑證範本的**更新期間**設定為1或2小時，且**有效期間**應超過**更新期間**，但不超過4小時。 如果您使用執行 Windows Server 2008 R2 的 CA 來設定超過4小時的憑證範本**有效期間**，directaccess 安裝精靈將無法偵測到憑證範本，且 directaccess 安裝將會失敗。

5.  按一下 [**安全性**] 索引標籤，選取 [**已驗證的使用者**]，在 [**允許**] 欄中選取 [**讀取**] 和 [**註冊**] 核取方塊。 按一下 [確定]  。 按一下 [ **Domain admins** ] 和 [ **Enterprise Admins**]，然後按一下 [**允許**] 資料行底下的 [**完全控制**]。 按一下 [套用]。

6.  按一下 [**主體名稱**] 索引標籤，然後**從這個 Active Directory 資訊中**按一下 [建立]。 在 [**主體名稱格式：** ] 清單中，選取 [**完整辨別名稱**]，確認已核取 [**使用者主體名稱 (UPN) ** ] 方塊，**然後按一下 [** 套用]。

7.  按一下 [**伺服器**] 索引標籤，選取 [**不要在 CA 資料庫中儲存憑證和要求**] 核取方塊，清除 [不要**在已發行的憑證中包含撤銷資訊**] 核取方塊，然後在 [**新範本**的內容] 對話方塊中按一下 [套用 **]。**

8.  按一下 [**發行需求**] 索引標籤，選取 [**此授權簽章數目：** ] 核取方塊，將值設定為1。 在 [簽章**所需的原則類型：** ] 清單中選取 [**應用程式原則**]，然後在**應用程式原則**清單中選取 [ **DA OTP RA**]。 在 [**新範本**的內容] 對話方塊中，按一下 **[確定**]。

9. 按一下 [**擴充**功能] 索引標籤，然後在 [**應用程式原則**] 按一下 [**編輯**] 刪除**用戶端驗證**，保留**SmartCardLogon**，然後按兩次 **[確定]** 。

10. 關閉 [憑證範本主控台]。

11. 在 [**開始**] 畫面上，輸入**certsrv**，然後按 enter。

12. 在 [憑證授權單位單位] 主控台樹中，展開 [ **APP1-CA-1**]，按一下 [**憑證範本**]，以滑鼠右鍵按一下 [**憑證範本**]，指向 [**新增**]，然後按一下 [**要發出的憑證範本**]。

13. 在憑證範本清單中，按一下 [ **DAOTPRA**和**DAOTPLogon**]，然後按一下 **[確定]**。

14. 在主控台的詳細資料窗格中，您應該會看到 [ **DAOTPRA** ] 憑證範本具有 [適用于**DA OTP RA**的**目標**] 和 [ **DAOTPLogon**憑證範本]，並具有**預定用途**的**智慧卡登**入。

15. 重新啟動服務。

16. 關閉 [憑證授權單位] 主控台。

17. 開啟提升權限的命令提示字元。 輸入**CertUtil.exe-SetReg DBFlags + DBFLAGS_ENABLEVOLATILEREQUESTS**，然後按 enter。

18. 讓命令提示字元視窗保持開啟，以進行下一個步驟。

