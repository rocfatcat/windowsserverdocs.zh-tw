---
ms.assetid: d8adcb68-18e0-41bf-a817-d57344bf2e7d
title: Windows Server 2016 中的 Web 應用程式 Proxy
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: 2f24e1b8605503d338b15f385017bbeacce682fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872209"
---
# <a name="web-application-proxy-in-windows-server-2016"></a>Windows Server 2016 中的 Web 應用程式 Proxy

>適用於：Windows Server 2016

**此內容是關於 Web 應用程式 Proxy 的內部部署版本的項目。若要在雲端上啟用安全存取內部部署應用程式，請參閱[Azure AD Application Proxy 內容](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)。**  
  
本章節內容說明的新功能和 Web 應用程式 Proxy 的 Windows Server 2016 中已變更。 變更此處所列的新功能是最有可能有重大影響，當您使用預覽。  
  
## <a name="web-application-proxy-new-features-in-windows-server-2016"></a>Web 應用程式 Proxy 中的新功能 Windows Server 2016
  
-   HTTP 基本應用程式發佈的預先驗證  
  
    HTTP 基本驗證是許多通訊協定，包括 ActiveSync，用來連接豐富型用戶端，包括智慧型手機，使用您的 Exchange 信箱的授權通訊協定。 傳統上會與 AD FS 使用重新導向 ActiveSync 用戶端不支援 web 應用程式 Proxy 互動。 這個新版本的 Web 應用程式 Proxy 提供的支援發行使用 HTTP 基本藉由啟用 HTTP 應用程式接收非宣告的應用程式信賴憑證者信任 Federation Service 應用程式。  
  
    如需有關 HTTP 基本發佈的詳細資訊，請參閱[使用 AD FS 預先驗證發行應用程式](Publishing-Applications-using-AD-FS-Preauthentication.md#publish-an-application-that-uses-http-basic)  
  
-   萬用字元網域發佈應用程式  
  
    若要支援的案例，例如 SharePoint 2013，應用程式的外部 URL 現在可以包含萬用字元，以讓您將發行從多個應用程式特定的網域，例如 https://*.sp-apps.contoso.com 內。 這會簡化 SharePoint 應用程式的發行。  
  
-   HTTP 至 HTTPS 重新導向  
  
    若要確定您的使用者可以存取您的應用程式，即使他們沒有在 URL 中輸入 HTTPS，Web 應用程式 Proxy 現在支援 HTTP 至 HTTPS 重新導向。  
  
-   HTTP 發佈  
  
    您現在可發行使用傳遞預先驗證的 HTTP 應用程式  
  
-   遠端桌面閘道應用程式發佈  
  
    如需有關 Web 應用程式 Proxy 中的 RDG 的詳細資訊，請參閱[與 SharePoint、 Exchange 及 RDG 發佈應用程式](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)  
  
-   新的偵錯記錄檔，以協助疑難排解和服務記錄檔以取得完整的稽核記錄和改善的錯誤處理  
  
    如需有關疑難排解的詳細資訊，請參閱[疑難排解 Web 應用程式 Proxy](https://technet.microsoft.com/library/dn770156.aspx)  
  
-   系統管理員主控台 UI 增強功能  
  
-   後端應用程式的用戶端 IP 位址的傳播  
  
## <a name="see-also"></a>另請參閱  
  
-   [什麼是 Windows Server 2016 新功能](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [使用 AD FS 預先驗證發佈應用程式](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [疑難排解 Web 應用程式 Proxy](https://technet.microsoft.com/library/dn770156.aspx)  
  

