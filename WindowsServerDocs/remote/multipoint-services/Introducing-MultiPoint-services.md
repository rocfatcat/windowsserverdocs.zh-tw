---
title: 簡介 MultiPoint 服務
description: 提供 MultiPoint 服務的總覽，這是一種讓多個使用者共用系統的方式。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 1cbef744-4661-4ba9-9e2b-0bbd8854fd5c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 663b3d4afade9b4fb459f34120d1e6b18984285a
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997427"
---
# <a name="introducing-multipoint-services"></a>簡介 MultiPoint 服務
Windows Server 2016 中的 MultiPoint 服務角色可讓多個使用者，各自擁有各自獨立且熟悉的 Windows 體驗，同時共用一部電腦。有數種方式可供使用者存取其會話。 其中一種方式是使用[遠端桌面應用程式](../remote-desktop-services/clients/remote-desktop-clients.md)搭配任何裝置來遠端執行伺服器。 另一種方式是透過電臺連接到 MultiPoint 伺服器的實體電臺：

-   直接前往電腦上的視訊連接埠

-   透過特製化 USB 零用戶端 (也稱為多功能 USB 集線器) ，以及透過類似的 USB 乙太網路裝置。

-   透過區域網路 (LAN) 

本檔稍後的[MultiPoint 服務站](MultiPoint-services-Stations.md)中會更詳細地說明每一種方法。

本檔說明當您打算部署 MultiPoint 服務時所要考慮的下列因素：

-   要搭配 MultiPoint 服務系統使用的桌面類型：您需要會話、虛擬機器還是 Windows 電腦？

-   [選取適用于 MultiPoint 服務系統的硬體](./select-hardware-mps.md)：您應該進行哪些硬體決策？

-   [硬體需求和效能建議](./hardware-and-performance-recommendations.md)： MultiPoint 服務需要什麼硬體？

-   [Multipoint 服務網站規劃](MultiPoint-services-Site-Planning.md)：執行 multipoint 服務及其工作站的電腦會在何處找到，以及如何設定？

-   [網路考慮和使用者帳戶](Network-Considerations-and-User-Accounts.md)：要在其中部署 MultiPoint 服務系統的網路環境，可能會影響使用者帳戶的管理方式。 您的網路環境是什麼？ 如何管理使用者帳戶？

-   [使用 MultiPoint 服務儲存](Storing-Files-with-MultiPoint-services.md)盤案：儲存使用者檔案的位置，以及這些檔案的存取方式為何？

-   [預先部署檢查清單](Predeployment-Checklist.md)