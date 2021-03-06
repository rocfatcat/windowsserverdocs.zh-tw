---
title: 安裝 RDS 用戶端存取使用權
description: 了解如何為 RD 用戶端安裝 CAL。
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 848ca4ae9edd414173bbfd5822011b93d044e394
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961662"
---
# <a name="install-rds-client-access-licenses-on-the-remote-desktop-license-server"></a>在遠端桌面授權伺服器上安裝 RDS 用戶端存取使用權

>適用於：Windows Server (半年通道)、Windows Server 2019、Windows Server 2016

請使用下列資訊，將遠端桌面服務用戶端存取使用權 (CAL) 安裝在授權伺服器上。 安裝 CAL 之後，授權伺服器即會適時地將其核發給使用者。

請注意，您執行遠端桌面授權管理員的電腦 (而不是執行授權伺服器的電腦) 上必須要有網際網路連線。

1. 在授權伺服器 (通常是第一個 RD 連線代理人) 上，開啟 [遠端桌面授權管理員]。
2. 以滑鼠右鍵按一下授權伺服器，然後按一下 [安裝授權]  。
3. 在 [歡迎頁面] 上按 [下一步]  。
4. 選取您用來購買 RDS CAL 的方案，然後按 [下一步]  。 如果您是服務提供者，請選取 [服務提供者授權合約]  。
5. 輸入您的授權方案資訊。 在大部分情況下，這項資訊會是授權碼或合約號碼，但會隨著您所使用的授權方案而不同。
6. 按 [下一步]  。
7. 選取您的環境的產品版本、授權類型和授權數目，然後按 [下一步]  。 授權管理員會連絡 Microsoft Clearinghouse，以驗證及擷取您的授權。
8.  按一下 [完成]  完成訂購程序。