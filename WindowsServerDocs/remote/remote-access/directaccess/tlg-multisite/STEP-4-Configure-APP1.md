---
title: 步驟4設定 APP1
description: 本主題屬於測試實驗室指南-示範適用于 Windows Server 2016 的 DirectAccess 多網站部署
manager: brianlic
ms.topic: article
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 32f781293e4e4406d38c867f5461559101e8f398
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953694"
---
# <a name="step-4-configure-app1"></a>步驟4設定 APP1

>適用於：Windows Server (半年度管道)、Windows Server 2016

設定靜態 IPv6 位址和閘道設定，以啟用對2公司網路子網的 APP1 存取。

- 設定預設閘道和 DNS 伺服器。 多網站設定會使用 ROUTER1 電腦做為預設閘道。 在 APP1 上設定預設閘道。

## <a name="to-configure-the-default-gateway-and-dns-server"></a>設定預設閘道和 DNS 伺服器

1.  在伺服器管理員主控台中，按一下 [**本機伺服器**]，然後在 [**屬性**] 區域中的 [**有線乙太**網路連線] 旁，按一下連結。

2.  在 [**網路**連線] 視窗中，以滑鼠**按右鍵 [****有線 Ethernet 連接**]，然後按一下 [內容]。

3.  在 [**有線乙太**網路線上內容] 對話方塊中 **，按一下 [****網際網路通訊協定第4版] ([TCP/IPv4) **]，然後按一下 [內容]。

4.  在 [**預設閘道**] 中，輸入**10.0.0.254**，並在 [**其他 DNS 伺服器**] 中輸入**10.2.0.1**，然後按一下 **[確定]**。

5.  在 [**有線乙太**網路線上內容] 對話方塊中，按一下 [**網際網路通訊協定第6版] ([TCP/IPv6) **]，然後按一下 [內容 **]。**

6.  在 [**預設閘道**] 中，輸入**2001： db8：1：： fe**。 在 [**其他 DNS 伺服器**] 中，輸入**2001： db8：2：： 1**，然後按一下 **[確定]**。

7.  在 [**有線乙太**網路線上內容] 對話方塊中，按一下 [**關閉**]，然後關閉 [**網路**連線] 視窗。



