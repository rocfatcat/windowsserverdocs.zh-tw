---
title: 設定條件式存取原則
description: 建立根憑證之後，VPN 連線就會觸發 「 VPN 伺服器 」 的雲端應用程式，在客戶的租用戶中建立。
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 466e76d01ca99a1e1ed72fa955ccd287ae63c5df
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749502"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>步驟 7.3. 設定條件式存取原則

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows 10

- [**前一個：** 步驟 7.2.使用 Azure AD 建立 VPN 驗證的根憑證](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**下一步:** 步驟 7.4.將條件式存取的根憑證部署至內部部署 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

在此步驟中，您可以設定 VPN 連線能力的條件式存取原則。 「 VPN 連線能力 」 刀鋒視窗中建立第一個根憑證時，它會自動建立 「 VPN 伺服器 」 的雲端應用程式的租用戶中。

建立條件式存取原則指派給 VPN 使用者群組和範圍**雲端應用程式**要**VPN 伺服器**:

- **Users**：VPN 使用者
- **雲端應用程式**:VPN 伺服器
- **授與 （存取控制）** :[需要多重要素驗證]。 如有需要，可以使用其他控制項。

**程序：** 此步驟涵蓋建立最基本的條件式存取原則。  如有需要，可以使用其他條件及控制項。


1. 在 **條件式存取**頁面上，在頂端工具列中的選取**新增**。

    ![在條件式存取 頁面上選取 新增](../../media/Always-On-Vpn/07.png)

2. 在 **的新**頁面上，於**名稱**方塊中，輸入您的原則的名稱。 例如，輸入**VPN 原則**。

    ![在條件式存取 頁面上新增的原則名稱](../../media/Always-On-Vpn/08.png)

3. 在 **指派**區段中，選取**使用者和群組**。

    ![選取使用者和群組](../../media/Always-On-Vpn/09.png)

4. 在 **使用者和群組**頁面上，執行下列步驟：

    ![選取的測試使用者](../../media/Always-On-Vpn/10.png)

    a. 選取 **選取 使用者和群組**。

    b. 選取 **選取**。

    c. 在上**選取** 頁面上，選取**VPN 使用者**分組，然後按**選取**。

    d. 在 **使用者和群組**頁面上，選取**完成**。

5. 在 **新增**頁面上，執行下列步驟：

    ![選取雲端應用程式](../../media/Always-On-Vpn/11.png)

    a. 在 **指派**區段中，選取**雲端應用程式**。

    b. 在 **雲端應用程式**頁面上，選取**選取 應用程式**。

    d. 選取  **VPN 伺服器**。

6.  上**的新**頁面上，若要開啟**Grant**頁面上，於**控制項**區段中，選取**授與**。

    ![選取 [同意]](../../media/Always-On-Vpn/13.png)

7.  在 **授與**頁面上，執行下列步驟：

    ![選取需要多重要素驗證](../../media/Always-On-Vpn/14.png)

    a. 選取 **需要多重要素驗證**。

    b. 選取 **選取**。

8.  在 **的新**頁面的 **啟用原則**，選取**上**。

    ![啟用原則](../../media/Always-On-Vpn/15.png)

9.  在 **的新**頁面上，選取**建立**。


## <a name="next-steps"></a>後續步驟
[步驟 7.4.將條件式存取的根憑證部署至內部部署 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md):在此步驟中，您將部署條件式存取的根憑證做為 VPN 驗證的受信任的根憑證到您內部部署 AD。