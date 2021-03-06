---
title: 將 Active Directory Federation Services 角色服務移轉到 Windows Server 2012
description: 提供將 AD FS 服務遷移至 Windows Server 2012 的指示。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: abbd51daea374eb4684f5416bed45fb0aaf315d4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938208"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>將 Active Directory Federation Services 角色服務移轉到 Windows Server 2012

以下提供將下列角色服務遷移至 Windows Server 2012 上的 Active Directory 同盟服務 (AD FS) 的指示：

-   與 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 Windows 權杖型代理程式和 AD FS 1.1 宣告感知代理程式

-   在 Windows Server 2008 或 Windows Server 2008 R2 上安裝的 AD FS 2.0 同盟伺服器和 AD FS 2.0 同盟伺服器 Proxy

## <a name="supported-migration-scenarios"></a>支援的移轉案例
 遷移指示包含下列工作：

- 從執行 Windows Server 2008 或 Windows Server 2008 R2 的伺服器匯出 AD FS 2.0 設定資料

- 將此伺服器的作業系統從 Windows Server 2008 或 Windows Server 2008 R2 就地升級到 Windows Server 2012。

- 重新建立原始的 AD FS 設定，並還原此伺服器上剩餘的 AD FS 服務設定，這現在正在執行與 Windows Server 2012 一起安裝的 AD FS 伺服器角色。

  本指南不包含移轉正在執行多個角色之伺服器的指示。 如果您的伺服器正在執行多個角色，則建議您根據其他角色移轉指南中提供的資訊，設計伺服器環境特有的自訂移轉程序。 您可以在 [Windows Server 移轉入口網站](https://go.microsoft.com/fwlink/?LinkId=247608)上取得其他角色的移轉指南。

## <a name="supported-operating-systems"></a>支援的作業系統
 **目的地伺服器作業系統：**


- Windows Server 2012 或 Windows Server 2008 R2 (Server Core 和完整安裝選項) 

  **目的地伺服器處理器：**


- x64 型

|來源伺服器處理器|來源伺服器作業系統|
|-----|-----|
|x86 或 x64 型|Windows Server 2003 Service Pack 2|
|x86 或 x64 型|Windows Server 2003 R2|
|x86 或 x64 型|Windows Server 2008，包括完整和 Server Core 安裝選項|
|x64 型|Windows Server 2008 R2|
|x64 型|Windows Server 2008 R2 的 Server Core 安裝選項|
|x64 型|Windows Server 2012 的 Server Core 和完整安裝選項|

> [!NOTE]
> - 上表中所列的作業系統版本是支援的最舊作業系統與 Service Pack 組合。
>   -   無論做為來源或目的地伺服器，都支援 Windows Server 作業系統的 Foundation、Standard、Enterprise 和 Datacenter 版。
>   -   支援在實體作業系統和虛擬作業系統之間移轉。

### <a name="supported-ad-fs-role-services-and-features"></a>支援 AD FS 角色服務和功能
 下表說明本指南所述的 AD FS 角色服務和其各自設定的移轉案例。

|寄件者|若要使用 Windows Server 2012 安裝 AD FS|
|----------|-----|
|隨 Windows Server 2003 R2 一起安裝的 AD FS 1.0 同盟伺服器|不支援移轉|
|隨 Windows Server 2003 R2 一起安裝的 AD FS 1.0 同盟伺服器 Proxy|不支援移轉|
|隨 Windows Server 2003 R2 一起安裝的 AD FS 1.0 Windows 權杖型代理程式|不支援移轉|
|隨 Windows Server 2003 R2 一起安裝的 AD FS 1.0 宣告感知代理程式|不支援移轉|
|隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 同盟伺服器|不支援移轉|
|隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 同盟伺服器 Proxy|不支援移轉|
|隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 Windows 權杖型代理程式|支援在相同伺服器上的移轉，但移轉的 AD FS Windows 權杖型代理程式將只能與隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 Federation Service 搭配運作。 如需詳細資訊，請參閱<p> [移轉 AD FS 1.1 網路代理程式](migrate-the-ad-fs-web-agent.md)<p> [與 AD FS 1.x 互通](Interoperating-with-AD-FS-1.x.md)|
|隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 宣告感知代理程式|支援相同伺服器的移轉。 移轉的 AD FS 1.1 宣告感知網路代理程式可與下列項目搭配運作：<p> 隨 Windows Server 2008 或 Windows Server 2008 R2 一起安裝的 AD FS 1.1 Federation Service<p> 安裝在 Windows Server 2008 或 Windows Server 2008 R2 的 AD FS 2.0 Federation Service<p> 與 Windows Server 2012 一起安裝 AD FS federation service<p> 如需詳細資訊，請參閱<p> [移轉 AD FS 1.1 網路代理程式](migrate-the-ad-fs-web-agent.md)<p> [與 AD FS 1.x 互通](Interoperating-with-AD-FS-1.x.md)|
|安裝在 Windows Server 2008 或 Windows Server 2008 R2 的 AD FS 2.0 同盟伺服器|支援相同伺服器的移轉。 如需詳細資訊，請參閱<p> [準備移轉 AD FS 2.0 同盟伺服器](prepare-to-migrate-ad-fs-fed-server.md)<p> [移轉 AD FS 2.0 同盟伺服器](migrate-the-ad-fs-fed-server.md)|
|安裝在 Windows Server 2008 或 Windows Server 2008 R2 的 AD FS 2.0 同盟伺服器 Proxy|支援相同伺服器的移轉。  如需詳細資訊，請參閱：<p> [準備移轉 AD FS 2.0 同盟伺服器 Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)<p> [移轉 AD FS 2.0 同盟伺服器 Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)|

## <a name="see-also"></a>另請參閱
 [準備遷移 AD FS 2.0 同盟伺服器](prepare-to-migrate-ad-fs-fed-server.md)[準備遷移 AD FS 2.0 同盟伺服器 proxy](prepare-to-migrate-ad-fs-fed-proxy.md) [遷移 AD FS 2.0 同盟](migrate-the-ad-fs-fed-server.md)伺服器遷移[AD FS 2.0 同盟伺服器 proxy](migrate-the-ad-fs-2-fed-server-proxy.md) [遷移 AD FS 1.1 Web 代理](migrate-the-ad-fs-web-agent.md)程式