---
title: 將 Active Directory 同盟服務角色服務移轉到 Windows Server 2012 R2
description: 提供將 AD FS 服務遷移至 Windows Server 2012 R2 的指示。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: 49c75fadcbc1284f23b490eb6ee48813ef40f781
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970905"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>將 Active Directory 同盟服務角色服務移轉到 Windows Server 2012 R2
 本檔提供將下列角色服務遷移至與 Windows Server 2012 R2 一起安裝的 Active Directory 同盟服務 (AD FS) 的指示：

-   安裝在 Windows Server 2008 或 Windows Server 2008 R2 的 AD FS 2.0 同盟伺服器

-   安裝在 Windows Server 2012 的 AD FS 同盟伺服器

## <a name="supported-migration-scenarios"></a>支援的移轉案例
 本指南中的移轉指示包含下列工作：

- 從執行 Windows Server 2008、Windows Server 2008 R2 或 Windows Server 2012 的伺服器匯出 AD FS 2.0 設定資料

- 將此伺服器的作業系統從 Windows Server 2008、Windows Server 2008 R2 或 Windows Server 2012 就地升級至 Windows Server 2012 R2。

- 重新建立原始的 AD FS 設定，並還原此伺服器上剩餘的 AD FS 服務設定，這現在正在執行與 Windows Server 2012 R2 一起安裝的 AD FS 伺服器角色。

  本指南不包含移轉正在執行多個角色之伺服器的指示。 如果您的伺服器正在執行多個角色，則建議您根據其他角色移轉指南中提供的資訊，設計伺服器環境特有的自訂移轉程序。 您可以在 [Windows Server 移轉入口網站](https://go.microsoft.com/fwlink/?LinkId=247608)上取得其他角色的移轉指南。

### <a name="supported-operating-systems"></a>支援的作業系統
 目的地伺服器作業系統：

 Windows Server 2012 R2 (Server Core 和完整安裝選項) 

 目的地伺服器處理器：

 x64 型

|來源伺服器處理器|來源伺服器作業系統|
|-----------------------------|------------------------------------|
|x86 或 x64 型| Windows Server 2008，包括完整和 Server Core 安裝選項|
|x64 型|Windows Server 2008 R2|
|x64 型|Windows Server 2008 R2 的 Server Core 安裝選項|
|x64 型|Windows Server 2012 的 Server Core 和完整安裝選項|

> [!NOTE]
> - 上表中所列的作業系統版本是支援的最舊作業系統與 Service Pack 組合。
>   -   無論做為來源或目的地伺服器，都支援 Windows Server 作業系統的 Foundation、Standard、Enterprise 和 Datacenter 版。
>   -   支援在實體作業系統和虛擬作業系統之間移轉。

### <a name="supported-ad-fs-role-services-and-features"></a>支援 AD FS 角色服務和功能
 下表說明本指南所述的 AD FS 角色服務和其各自設定的移轉案例。

|寄件者|若要使用 Windows Server 2012 R2 安裝 AD FS|
|----------|----------------------------------------------------------------------------------------------|
|安裝在 Windows Server 2008 或 Windows Server 2008 R2 的 AD FS 2.0 同盟伺服器|支援相同伺服器的移轉。 如需詳細資訊，請參閱<p> [準備移轉 AD FS 同盟伺服器](prepare-migrate-ad-fs-server-r2.md)<p> [移轉 AD FS 同盟伺服器](migrate-ad-fs-fed-server-r2.md)|
|安裝在 Windows Server 2012 的 AD FS 同盟伺服器|支援相同伺服器的移轉。  如需詳細資訊，請參閱：<p> [準備移轉 AD FS 同盟伺服器](prepare-migrate-ad-fs-server-r2.md)<p> [移轉 AD FS 同盟伺服器](migrate-ad-fs-fed-server-r2.md)|

## <a name="next-steps"></a>後續步驟
 [準備遷移 AD FS 同盟伺服器](prepare-migrate-ad-fs-server-r2.md)遷移[AD FS 同盟](migrate-ad-fs-fed-server-r2.md)伺服器遷移[AD FS 同盟伺服器 Proxy](migrate-fed-server-proxy-r2.md) [驗證 AD FS 遷移至 Windows Server 2012 R2](verify-ad-fs-migration.md)