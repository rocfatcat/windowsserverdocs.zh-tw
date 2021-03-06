---
title: Windows Server SDN 的新功能
description: 本主題提供 Windows Server 1709 新軟體定義網路功能的相關資訊
manager: grcusanz
ms.topic: get-started-article
ms.assetid: efad919b-e9e7-4a0c-b373-e68a092f93b5
ms.author: anpaul
author: AnirbanPaul
ms.date: 10/02/2018
ms.openlocfilehash: bcf4923ec25aba66484ec384c8895d877aba0069
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962142"
---
# <a name="whats-new-in-sdn-for-windows-server-2019"></a>適用於 Windows Server 2019 的 SDN 的新功能

>適用於：Windows Server (半年通道)


|                         **功能**                          |                                                                                                                                                                                         **說明**                                                                                                                                                                                         | **新功能/更新功能** |
|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| [加密的網路](vnet-encryption/sdn-vnet-encryption.md) | 虛擬網路加密可讓虛擬機器之間的虛擬網路流量進行加密，這兩者會在子網內彼此通訊，並標示為「啟用加密」。 這項功能也利用虛擬子網路上的資料包傳輸層安全性 (DTLS) 來加密封包。 DTLS 提供保護以防止任何可存取實體網路的人進行竊聽、竄改和偽造。 |       新增       |
|    [防火牆審核](security/sdn-firewall-auditing.md)    |                                                                                            防火牆審核是 Windows Server 2019 中 SDN 防火牆的新功能。 當您啟用 SDN 防火牆時，SDN 防火牆規則所處理的任何流程都會記錄已啟用記錄的 (Acl) 。                                                                                            |       新增       |
| [虛擬網路對等互連](vnet-peering/sdn-vnet-peering.md)  |                                                                                                                      虛擬網路對等互連可讓您順暢地連接兩個虛擬網路。 一旦對等互連，基於連線目的，虛擬網路會顯示為一。                                                                                                                      |       新增       |
|           [輸出計量](manage/sdn-egress.md)            |                  Windows Server 2019 中的這項新功能可讓 SDN 提供輸出資料傳輸的使用量計量。 新增這項功能後，網路控制卡會針對 SDN 中使用的所有 IP 範圍，保留每個虛擬網路的白名單，並針對未包含在其中一個範圍內的目的地，考慮任何封包系結，以作為輸出資料傳輸的費用。                   |       新增       |

---



