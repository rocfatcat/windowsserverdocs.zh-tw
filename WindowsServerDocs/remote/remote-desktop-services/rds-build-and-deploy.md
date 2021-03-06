---
title: RDS - 建置和部署
description: 建置遠端桌面部署的步驟
ms.author: elizapo
ms.date: 04/18/2017
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: be58880108f84aa6141157dbe730e18fcff4c6c2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961802"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>建置和部署您的遠端桌面服務部署

遠端桌面服務部署是用來與使用者共用應用程式和資源的基礎結構。 根據您想要提供的體驗，您可以視需要讓它變得更小或更複雜。 輕鬆地調整遠端桌面部署。 您可以隨意地增加和減少遠端桌面 Web 存取、閘道、連線代理人和工作階段主機伺服器。 您可以使用遠端桌面連線代理人來散發工作負載。 Active Directory 型驗證可提供高度安全的環境。

[遠端桌面用戶端](clients/remote-desktop-clients.md)能夠從任何 Windows、Apple 或 Android 電腦、平板電腦或手機存取。

如需一起運作來組成遠端桌面服務部署之各個部分的詳細討論，請參閱[遠端桌面服務架構](desktop-hosting-logical-architecture.md)。

現有的遠端桌面部署是否已建置於舊版 Windows Server 上？ 請檢查您可用來移至 Windows Server 2016 的選項，您可以在其中利用關於效能與延展性的新功能和更好的功能：

- [將您的 RDS 部署移轉至 Windows Server 2016](migrate-rds-role-services.md)
- [將您的 RDS 部署升級至 Windows Server 2016](./upgrade-to-rds.md)

想要建立新的遠端桌面部署嗎？ 請使用下列資訊來部署 Windows Server 2016 中的遠端桌面：

- [部署遠端桌面服務基礎結構](rds-deploy-infrastructure.md)
- [建立工作階段集合來保存您想要共用的應用程式和資源](rds-create-collection.md)
- [授權您的 RDS 部署](rds-client-access-license.md)
- 讓使用者安裝[遠端桌面用戶端](clients/remote-desktop-clients.md)，如此一來，他們就能夠存取應用程式和資源。
- 藉由新增其他連線代理人和工作階段主機來啟用高可用性：
   - [使用 RD 工作階段主機伺服器陣列向外延展現有的 RDS 集合](rds-scale-rdsh-farm.md)
   - [新增高可用性到 RD 連線代理人基礎結構](rds-connection-broker-cluster.md)
   - [新增高可用性到 RD Web 和 RD 閘道 Web 前端](rds-rdweb-gateway-ha.md)
   - [部署雙節點儲存空間直接存取檔案系統以儲存 UPD](rds-storage-spaces-direct-deployment.md)


如果您是有興趣使用遠端桌面來提供應用程式和資源給客戶的代管合作夥伴，或是尋找某人來代管您應用程式的客戶，請參閱[遠端桌面服務代管合作夥伴](rds-hosting-partners.md)，以了解下列相關資訊：您可以針對在 Azure 中使用 RDS 作為代管環境所採取的評估，以及已通過該評估的合作夥伴清單。
