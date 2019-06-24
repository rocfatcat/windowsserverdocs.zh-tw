---
title: 使用群組原則來設定網域成員用戶端電腦
description: 本主題是 BranchCache 部署指南的 Windows Server 2016 中，示範如何以最佳化 WAN 頻寬使用量，在分公司的分散式和裝載式快取模式部署 BranchCache 的一部分
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: pashort
author: shortpatti
ms.date: 06/02/2018
ms.openlocfilehash: 8e82d3e0ee7a84fbd6e2916d0f22472a8c117688
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855079"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>使用群組原則來設定網域成員用戶端電腦

>適用於：Windows Server （半年通道），Windows Server 2016

在本節中，您組織中建立群組原則物件的所有電腦、 網域成員用戶端電腦設定為使用分散式快取模式或託管快取模式和設定具有進階安全性，以允許 BranchCache 的 Windows 防火牆流量。  
  
本章節包含下列程序。  
  
1.  [若要建立群組原則物件和設定 BranchCache 模式](#bkmk_gp)  
  
2.  [若要使用進階安全性的輸入流量規則設定 Windows 防火牆](#bkmk_inbound)  
  
3.  [若要使用進階安全性輸出流量規則設定 Windows 防火牆](#bkmk_outbound)  
  
> [!TIP]  
> 在下列程序中，系統指示您在 預設網域原則中建立群組原則物件，不過，您可以建立物件，在組織單位 (OU) 或其他適用於您部署的容器中。  
  
您必須是隸屬**Domain Admins**，或同等權限才能執行這些程序。  
  
## <a name="bkmk_gp"></a>若要建立群組原則物件和設定 BranchCache 模式  
  
1.  安裝的電腦上的 Active Directory 網域服務伺服器角色，在 [伺服器管理員] 中，按一下**工具**，然後按一下**群組原則管理**。 群組原則管理主控台隨即開啟。  
  
2.  在 [群組原則管理] 主控台中，展開下列路徑：**樹系：** *example.com*，**網域**， *example.com*，**群組原則物件**，其中*example.com*是您想要設定 BranchCache 用戶端電腦帳戶所在網域的名稱。  
  
3.  以滑鼠右鍵按一下**群組原則物件**，然後按一下**新增**。 **新的 GPO**對話方塊隨即開啟。 在 **名稱**，輸入名稱 「 新群組原則物件 (GPO)。 例如，如果您想要命名的物件 BranchCache 用戶端電腦，輸入**BranchCache 用戶端電腦**。 按一下 [確定] 。  
  
4.  在 [群組原則管理] 主控台中，確定**群組原則物件**已選取，然後在 [詳細資料] 窗格中以滑鼠右鍵按一下您剛才建立的 GPO。 例如，如果您名為 GPO BranchCache 用戶端電腦，以滑鼠右鍵按一下**BranchCache 用戶端電腦**。 按一下 **\[編輯\]**。 群組原則管理編輯器主控台隨即開啟。  
  
5.  在 [群組原則管理編輯器] 主控台中，展開下列路徑：**電腦設定**，**原則**，**系統管理範本：從本機電腦的原則定義 （ADMX 檔案） 擷取**，**網路**， **BranchCache**。  
  
6.  按一下  **BranchCache**，然後在 詳細資料 窗格中，按兩下**開啟 BranchCache**。 原則的 [設定] 對話方塊隨即開啟。  
  
7.  在 [**開啟 BranchCache** ] 對話方塊中，按一下**已啟用**，然後按一下 **[確定]**。  
  
8.  若要啟用 BranchCache 分散式快取模式，在 [詳細資料] 窗格中，按兩下**設定 BranchCache 分散式快取模式**。 原則的 [設定] 對話方塊隨即開啟。  
  
9. 在 [**設定 BranchCache 分散式快取模式**] 對話方塊中，按一下**已啟用**，然後按一下 **[確定]**。  
  
10. 如果您有一或多個分公司其中您要部署 BranchCache 託管快取模式，而您已部署裝載在辦公室中的快取伺服器中，按兩下**啟用自動託管快取探索的服務連接點**. 原則的 [設定] 對話方塊隨即開啟。  
  
11. 在 **啟用自動託管快取探索服務連接點所** 對話方塊中，按一下**已啟用**，然後按一下  **確定**。  
  
    > [!NOTE]  
    > 當您啟用這兩**設定 BranchCache 分散式快取模式**並**啟用自動託管快取探索透過服務連線點**中 BranchCache 的原則設定，用戶端電腦運作分散式快取模式，除非它們在分公司辦公室，屆時它們運作託管快取模式中尋找託管快取伺服器。  
  
12. 使用下列程序使用群組原則設定用戶端電腦上的防火牆設定。  
  
## <a name="bkmk_inbound"></a>若要使用進階安全性的輸入流量規則設定 Windows 防火牆  
  
1.  在 [群組原則管理] 主控台中，展開下列路徑：**樹系：** *example.com*，**網域**， *example.com*，**群組原則物件**，其中*example.com*是您想要設定 BranchCache 用戶端電腦帳戶所在網域的名稱。  
  
2.  在 [群組原則管理] 主控台中，確定**群組原則物件**已選取，然後在 [詳細資料] 窗格中以滑鼠右鍵按一下您先前建立的 GPO 的 BranchCache 用戶端電腦。 例如，如果您名為 GPO BranchCache 用戶端電腦，以滑鼠右鍵按一下**BranchCache 用戶端電腦**。 按一下 **\[編輯\]**。 群組原則管理編輯器主控台隨即開啟。  
  
3.  在 [群組原則管理編輯器] 主控台中，展開下列路徑：**電腦設定**，**原則**， **Windows 設定**，**安全性設定**，**具有進階安全性的Windows防火牆**，**具有進階安全性-LDAP 的 Windows 防火牆**，**輸入規則**。  
  
4.  以滑鼠右鍵按一下 [**輸入規則**]，然後按一下 [**新增規則**]。 新增輸入規則精靈 隨即開啟。  
  
5.  在 **規則類型**，按一下**預先定義**展開選項清單，然後按一下  **BranchCache-內容擷取 (使用 HTTP)**。 按一下 [下一步] 。  
  
6.  在 [**預先定義的規則**，按一下**下一步]**。  
  
7.  在 **動作**，請確認**允許連線**已選取，然後按一下**完成**。  
  
    > [!IMPORTANT]  
    > 您必須選取**允許連線**BranchCache 用戶端能夠在此連接埠上接收流量。  
  
8.  若要建立 Ws-discovery 防火牆例外狀況，再次以滑鼠右鍵按一下**輸入規則**，然後按一下**新規則**。 新增輸入規則精靈 隨即開啟。  
  
9. 在 **規則類型**，按一下**預先定義**展開選項清單，然後按一下  **BranchCache-同儕節點探索 (使用 WSD)**。 按一下 [下一步] 。  
  
10. 在 [**預先定義的規則**，按一下**下一步]**。  
  
11. 在 **動作**，請確認**允許連線**已選取，然後按一下**完成**。  
  
    > [!IMPORTANT]  
    > 您必須選取**允許連線**BranchCache 用戶端能夠在此連接埠上接收流量。  
  
## <a name="bkmk_outbound"></a>若要使用進階安全性輸出流量規則設定 Windows 防火牆  
  
1.  在 [群組原則管理編輯器] 主控台中，以滑鼠右鍵按一下**輸出規則**，然後按一下**新規則**。 新的輸出規則精靈 隨即開啟。  
  
2.  在 **規則類型**，按一下**預先定義**展開選項清單，然後按一下  **BranchCache-內容擷取 (使用 HTTP)**。 按一下 [下一步] 。  
  
3.  在 [**預先定義的規則**，按一下**下一步]**。  
  
4.  在 **動作**，請確認**允許連線**已選取，然後按一下**完成**。  
  
    > [!IMPORTANT]  
    > 您必須選取**允許連線**BranchCache 用戶端可以在此連接埠傳送流量。  
  
5.  若要建立 Ws-discovery 防火牆例外狀況，再次以滑鼠右鍵按一下**輸出規則**，然後按一下**新規則**。 新的輸出規則精靈 隨即開啟。  
  
6.  在 **規則類型**，按一下**預先定義**展開選項清單，然後按一下  **BranchCache-同儕節點探索 (使用 WSD)**。 按一下 [下一步] 。  
  
7.  在 [**預先定義的規則**，按一下**下一步]**。  
  
8.  在 **動作**，請確認**允許連線**已選取，然後按一下**完成**。  
  
    > [!IMPORTANT]  
    > 您必須選取**允許連線**BranchCache 用戶端可以在此連接埠傳送流量。  
  

