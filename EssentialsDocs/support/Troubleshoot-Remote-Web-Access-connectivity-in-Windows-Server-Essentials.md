---
title: Windows Server Essentials 的遠端 Web 存取連線問題疑難排解
description: 說明如何使用 Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: fc51555f680126cbd1b6e9fe2c672cbcbc5da7e9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625143"
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Windows Server Essentials 的遠端 Web 存取連線問題疑難排解

>適用于： Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 一般而言，如果寬頻路由器是 UPnP 認證裝置，而且路由器上已啟用 UPnP 設定，Windows Server Essentials 會自動設定路由器。

## <a name="possible-issues"></a>可能的問題
 您可能會遇到下列與遠端 Web 存取連線相關的問題：

-   路由器未開啟或未連線到網路。

-   路由器的 UPnP 設定已關閉。

-   路由器可能不完全支援 UPnP 標準。 Microsoft 維護一份適用於 Windows 作業系統的路由器清單。 若要檢視與 Windows Server Essentials 相容的路由器 (包括無線路由器) 清單，請瀏覽 [Windows 相容性中心](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)。

## <a name="possible-fixes"></a>可能的修正
 下列動作可能會修正這些問題：

- 確認路由器已開啟且運作正常。

- 確定伺服器直接連線到路由器，或連線到與路由器連線的交換器。

- 確認連線到網際網路服務提供者 (ISP) 的寬頻裝置已開啟、運作正常，而且路由器已連線到寬頻裝置。

- 開啟路由器的 UPnP 設定。 連線到路由器的設定網頁以開啟 UPnP 設定。 如需如何登入路由器及如何開啟 UPnP 設定的相關資訊，請參閱路由器的文件。 開啟 UPnP 設定之後，請再次執行 [開啟遠端 Web 存取嚮導] 來設定您的路由器。

- 如果路由器不完全支援 UPnP 標準，便無法自動設定。 您必須手動設定路由器，或購買支援 UPnP 標準的路由器。

   若要手動設定路由器，請完成下列工作：

  - 為 Windows Server Essentials 伺服器建立 IP 位址保留區。

     手動設定路由器將必要的連接埠轉送到 Windows Server Essentials 之前，必須為在路由器上執行 Windows Server Essentials 的伺服器設定動態主機設定通訊協定 (DHCP) 保留區。 這個步驟可確保所要轉送之連接埠的 IP 位址不會變更。

     如需有關如何在路由器上手動設定伺服器 DHCP 保留區的詳細資訊，請參閱製造商的路由器檔。

  - 請針對下列連接埠，在路由器上設定連接埠轉送：

    |服務或通訊協定|Port|
    |-------------------------|----------|
    |HTTP|TCP 80|
    |HTTPS|TCP 443|

    如需有關如何在路由器上手動設定埠轉送的詳細資訊，請參閱製造商的檔。

    一般路由器設定頁包含類似如下的表格。

  > [!NOTE]
  >  在這個表格中，執行 Windows Server Essentials 之電腦的 IP 位址是 192.168.0.100。 您必須判斷電腦的 IP 位址，並用表格中所顯示的 IP 位址來取代該 IP 位址。

  |IP 位址|通訊協定 (TCP/UDP)|排程|輸入篩選器|
  |----------------|---------------------------|--------------|--------------------|
  |192.168.0.100|TCP 80|一律|全部允許|
  |192.168.0.100|TCP 443|一律|全部允許|

   手動設定路由器之後，請執行 [開啟遠端 Web 存取 Wizard]，確定您在 **[開始使用] 頁面上**選取 [**略過路由器設定**] 選項。

- 如果路由器不完全支援 UPnP 標準，請購買新的路由器。

> [!TIP]
>  確定路由器已安裝最新的 BIOS 韌體。 您通常可以從路由器的設定網頁，更新路由器的 BIOS 韌體。 如需詳細資訊，請參閱路由器的文件。 更新路由器之後，請執行 [設定隨處存取精靈]。

## <a name="see-also"></a>另請參閱

-   [使用遠端 Web 存取](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [管理遠端 Web 存取](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [管理隨處存取](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [管理 Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

-   [支援 Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

