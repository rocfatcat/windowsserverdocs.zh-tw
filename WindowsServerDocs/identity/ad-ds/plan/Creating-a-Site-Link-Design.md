---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: 建立站台連結設計
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: 881ca5f2d932a8e13aaa7467179360ca8bb4af66
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941138"
---
# <a name="creating-a-site-link-design"></a>建立站台連結設計

> 適用於：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

建立站台連結設計，以使用站台連結來連接您的網站。 站台連結會反映用來傳送複寫流量的站上連接和方法。 您必須以網站連結連接網站，讓每個網站上的網域控制站可以複寫 Active Directory 變更。

## <a name="connecting-sites-with-site-links"></a>使用站台連結連線站台

若要使用站台連結來連接網站，請找出您想要與站台連結連線的成員網站，在個別的網站間傳輸容器中建立站台連結物件，然後為網站連結命名。 建立站台連結之後，您可以繼續設定站台連結屬性。

建立站台連結時，請確定每個網站都包含在站台連結中。 此外，請確定所有網站都透過其他站台連結彼此連接，以便將變更從任何網站中的網域控制站複寫到所有其他網站。 如果您無法這麼做，則目錄服務記錄檔中會產生一則錯誤訊息，事件檢視器指出網站拓撲未連線。

當您將網站新增至新建立的站台連結時，請判斷要加入的網站是否為其他站台連結的成員，並視需要變更網站的站台連結成員資格。 例如，如果您在一開始建立網站時，將網站設為預設的第一個網站連結，請務必在您將網站新增至新的網站連結之後，從預設的網站連結移除網站。 如果您未從預設的第一個網站連結中移除網站，則知識一致性檢查程式 (KCC) 將會根據兩個站台連結的成員資格來做出路由決策，而這可能會導致不正確的路由。

若要識別您想要與站台連結連線的成員網站，請使用您在 [地理位置和通訊連結] 中記錄的位置和連結位置清單 ( # A0) 工作表。 如果多個網站具有相同的連線能力和可用性，您可以使用相同的站台連結來連接它們。

網站間傳輸容器會提供方法，將站台連結對應至連結所使用的傳輸。 當您建立站台連結物件時，您會在 IP 容器中建立它，此容器會將站台連結與遠端程序呼叫產生關聯， (RPC) over IP 傳輸，或使用 Simple Mail Transfer Protocol (SMTP) 容器，這會將站台連結與 SMTP 傳輸產生關聯。

> [!NOTE]
> 未來版本的 Active Directory Domain Services (AD DS) ，將不支援 SMTP 複寫。因此，不建議在 SMTP 容器中建立站台連結物件。

當您在個別的網站間傳輸容器中建立站台連結物件時，AD DS 會使用 RPC over IP 來傳送網域控制站之間的站對站和網站間複寫。 為了讓資料在傳輸期間保持安全，RPC over IP 複寫會使用 Kerberos 驗證通訊協定和資料加密。

當直接 IP 連線無法使用時，您可以在網站之間設定複寫以使用 SMTP。 不過，SMTP 複寫功能有限，而且需要 (CA) 的企業憑證授權單位單位。 SMTP 只能複寫設定、架構和應用程式目錄分割，而且不支援複寫網域目錄分割。

若要命名站台連結，請使用一致的命名配置，例如 name_of_site1 name_of_site2。 記錄網站的清單、連結的網站，以及在工作表中連接這些網站之站台連結的名稱。 如需協助您記錄網站名稱和相關網站連結名稱的工作表，請參閱 [適用于 Windows Server 2003 部署套件的工作輔助工具](https://microsoft.com/download/details.aspx?id=9608)、下載 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip，以及開啟 [網站和相關網站連結] ( # A1) 。

## <a name="in-this-guide"></a>本指南內容

[設定站台連結屬性](Setting-Site-Link-Properties.md)
