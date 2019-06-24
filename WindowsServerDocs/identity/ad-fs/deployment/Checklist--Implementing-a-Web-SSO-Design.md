---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: 檢查清單-實作網頁 SSO 設計
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b2e09addbdc192bc6ce93a4402e6a6e61873ad56
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192359"
---
# <a name="checklist-implementing-a-web-sso-design"></a>檢查清單：實作網頁 SSO 設計

此父檢查清單包含跨\-參照有關 Web 單一的重要概念的連結\-號\-上\(SSO\)設計 Active Directory Federation Services \(AD FS\). 它也包含次檢查清單連結，其中的資訊可協助您完成實作此設計所需執行的工作。  
  
> [!NOTE]  
> 請依序完成此檢查清單中的工作。 當參照連結將您導向概念性主題或次檢查清單時，請在檢閱概念性主題或完成次檢查清單中的工作之後返回此主題，以便您可以繼續執行此檢查清單中的其餘工作。  
  
![網頁 sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**檢查清單：實作網頁 SSO 設計**  
  
||工作|參考資料|  
|-|--------|-------------|  
|![網頁 sso](media/icon_checkboxo.gif)|檢閱有關網頁 SSO 設計的重要概念，並判斷哪一個 AD FS 部署目標，您可以使用來自訂此設計，以符合您組織的需求。 **注意：** |![網頁 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[網頁 SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![網頁 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[識別您的 AD FS 部署目標](https://technet.microsoft.com/library/dd807053.aspx)|  
|![網頁 sso](media/icon_checkboxo.gif)|檢閱硬體、 軟體、 憑證、 網域名稱系統\(DNS\)、 屬性存放區，並針對您的組織中部署 AD FS 用戶端需求。|![網頁 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[附錄 a:檢閱 AD FS 需求](https://technet.microsoft.com/library/ff678034.aspx)|  
|![網頁 sso](media/icon_checkboxo.gif)|根據您的設計計畫，請在公司網路或周邊網路中安裝一或多個同盟伺服器。 **注意：** 網頁 SSO 設計中需要能順利運作的只有一部同盟伺服器。 在單一同盟伺服器會作為宣告提供者角色與信賴憑證者的合作對象角色。|![網頁 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[檢查清單：設定同盟伺服器](Checklist--Setting-Up-a-Federation-Server.md)|  
|![網頁 sso](media/icon_checkboxo.gif)|\(選擇性\)判斷您的組織是否需要在周邊網路中的同盟伺服器 proxy。|![網頁 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[檢查清單：設定同盟伺服器 Proxy](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![網頁 sso](media/icon_checkboxo.gif)|根據您的網頁 SSO 設計計畫與您想要的使用方式而定，新增適當的屬性存放區、信賴憑證者信任與宣告規則至 Federation Service。|![網頁 sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[檢查清單：設定帳戶夥伴組織](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![網頁 sso](media/icon_checkboxo.gif)|如果您是資源夥伴組織中的系統管理員，宣告\-可讓您的 Web 瀏覽器應用程式、 Web 服務應用程式或使用 WIF 與 WIF SDK 的 Microsoft® Office SharePoint® Server 應用程式。 **注意：** |![網頁 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![網頁 sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 