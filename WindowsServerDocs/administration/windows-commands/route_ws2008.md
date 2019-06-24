---
title: route_ws2008
description: 了解如何修改，並顯示本機 IP 路由表中的項目。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afcd666c-0cef-47c2-9bcc-02d202b983b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 30843fe94ac7a4dc60092adcede60120bc9e627f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441766"
---
# <a name="routews2008"></a>route_ws2008

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

顯示及修改本機 IP 路由表中的項目。 不含參數，**路由**顯示說明。   

## <a name="syntax"></a>語法  
```  
route [/f] [/p] [<Command> [<Destination>] [mask <Netmask>] [<Gateway>] [metric <Metric>]] [if <Interface>]]  
```  

### <a name="parameters"></a>參數  

|參數|描述|  
|-------|--------|  
|/f|清除所有的項目不是主機路由 （路由網路遮罩為 255.255.255.255） 」、 「 回送網路路由 （127.0.0.0 的目的地和網路遮罩 255.0.0.0） 或 「 多點傳送的路由的路由表，目的地為 224.0.0.0 （路由和 240.0.0.0 的網路遮罩）。 如果這用來搭配其中一個命令 （例如新增、 變更或刪除），資料表就會清除之前執行命令。|  
|/p|[新增] 命令搭配使用時，將指定的路由新增至登錄，用來初始化 IP 路由表，每次啟動時的 TCP/IP 通訊協定。 根據預設，啟動 TCP/IP 通訊協定時，不會保留已新增的路由。 列印命令搭配使用時，會顯示持續性的路由清單。 針對所有其他命令，會忽略這個參數。 永久路由儲存在登錄位置**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\PersistentRoutes**。|  
|\<命令 >|指定您想要執行的命令。 下表列出有效的命令：<br /><br />-   **新增：** 新增一個路由。<br />-   **變更：** 修改現有的路由。<br />-   **刪除：** 刪除路由。<br />-   **列印：** 列印路由。|  
|\<目的地 >|指定的網路目的地的路由。 目的地可以是 IP 網路位址 （網路位址的主機位元會設為 0）、 主機路由，IP 位址或預設路由 0.0.0.0。|  
|遮罩\<網路遮罩 >|指定的網路目的地的路由。 目的地可以是 IP 網路位址 （網路位址的主機位元會設為 0）、 主機路由，IP 位址或預設路由 0.0.0.0。|  
|\<Gateway>|指定轉送或下一個躍點 IP 位址的網路目的地及子網路遮罩所定義的位址會連線到其中。 本機連接的子網路路由的閘道位址會是指派給連接至子網路的介面的 IP 位址。 遠端路由，都可以跨一或多個路由器的閘道位址是直接連接的 IP 位址指派給鄰近路由器。|  
|計量\<計量 >|指定 （範圍從 1 到 9999） 的整數成本公制的路由，可在多個路由的路由表中最緊密符合 轉送的封包的目的地位址選擇。 選擇具有最低公制的路由。 計量可反映出躍點數目、 路徑、 路徑可靠性、 路徑輸送量或系統管理內容的速度。|  
|如果\<介面 >|指定的目的地是連線到介面的介面索引。 如需清單的介面和其對應的介面索引，使用 route print 命令的顯示。 您可以使用十進位或十六進位值的介面索引。 十六進位值，如前面以 0x 的十六進位數字。 當省略參數時，如果介面從閘道位址來決定。|  
|/?|在命令提示字元顯示說明。|  

## <a name="remarks"></a>備註  
- 中的大數值**計量**路由表的資料行都是允許 TCP/IP 來自動判斷的 IP 位址、 子網路遮罩及預設閘道的組態為基礎的路由表中的路由的公制所造成每個 LAN 介面。 自動決定的介面公制，預設啟用，決定每個介面的速度，並調整每個介面的路由的計量，使最快的介面會建立具有最低公制的路由。 若要移除的大型的度量，停用自動判斷每個區域網路連線的 TCP/IP 通訊協定的進階屬性的介面公制。  
- 名稱可以用於*目的地*儲存在本機網路檔案中存有適當的項目<strong>systemroot\System32\Drivers\\</strong>等資料夾。 名稱可以用於*閘道*只要它們是可解析成 IP 位址，透過標準的主機名稱解析技巧，例如網域名稱系統 (DNS) 查詢，使用儲存在本機 Hosts 檔案<strong>systemroot\system32\drivers\\</strong>etc 資料夾和 NetBIOS 名稱解析。  
- 如果命令**列印**或是**刪除**，則*閘道*可以省略參數，而目的地和閘道，可以使用萬用字元。 *目的地*值可以是指定星號 （*） 萬用字元值。 如果指定的目的地會包含星號 (\*) 或問號 （？），它會被視為萬用字元，只有符合的目的地路由會列印或刪除。 星號符合任何字串，並在問號符合任何單一字元。 例如，10。\*.1、 192.168。\*、 127。\*，並\*224\*是星號萬用字元的有效用法。  
- 使用目的地和子網路遮罩 （網路遮罩） 值的無效組合將會顯示 「 路由： 不正確的閘道位址的網路遮罩 」 錯誤訊息。 目的地可包含一個或多個位元設為 1，在對應的子網路遮罩位元會設為 0 的位元位置時，就會出現此錯誤訊息。 若要測試這種狀況，表示使用二進位表示法的目的地和子網路遮罩。 在二進位表示法的子網路遮罩是由一系列的 1 位元為單位表示目的地的網路位址部分和一系列的 0 位元，表示目的地的主機位址部分所組成。 檢查以判斷是否有目的地設定為 1 的一部分，也就是主應用程式 （如子網路遮罩所定義） 目的地的位元。  
- **/P**參數僅適用於路由命令在 Windows NT 4.0、 Windows 2000，Windows Millennium edition、 Windows XP 和 Windows Server 2003。 這個參數不支援**路由**命令取得對於 Windows 95 或 Windows 98。  
- 此命令才會提供網際網路通訊協定 (TCP/IP) 通訊協定安裝為在 網路連線的網路介面卡的內容中的元件。  

## <a name="BKMK_Examples"></a>範例  
若要顯示 IP 路由表的整個內容，請輸入：  
```  
route print  
```  
若要開始使用 10 IP 路由表中顯示的路由，請輸入：  
```  
route print 10.*  
```  
若要新增預設閘道位址 192.168.12.1 的預設路由，請輸入：  
```  
route add 0.0.0.0 mask 0.0.0.0 192.168.12.1  
```  
若要新增至子網路遮罩 255.255.0.0 與下一個躍點位址 10.27.0.1 10.41.0.0 目的地的路由，請輸入：  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
若要加入子網路遮罩 255.255.0.0 與下一個躍點位址 10.27.0.1 目的地 10.41.0.0 持續的路由，請輸入：  
```  
route /p add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
若要將路由新增至目的地 10.41.0.0 與子網路遮罩為 255.255.0.0 下, 一個躍點位址 10.27.0.1 和成本公制為 7，請輸入：  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 metric 7  
```  
若要新增至子網路遮罩 255.255.0.0 的 10.41.0.0 目的地的路由下, 一個躍點位址 10.27.0.1 並使用介面索引 0x3，輸入：  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 if 0x3  
```  
若要刪除與子網路遮罩 255.255.0.0 10.41.0.0 目的地的路由，請輸入：  
```  
route delete 10.41.0.0 mask 255.255.0.0  
```  
若要刪除的所有路由 IP 路由表中開始使用 10，請輸入：  
```  
route delete 10.*  
```  
若要變更成 10.27.0.25 從 10.27.0.1 10.41.0.0 目的地與子網路遮罩 255.255.0.0 路由的下一個躍點位址，請輸入：  
```  
route change 10.41.0.0 mask 255.255.0.0 10.27.0.25  
```  

## <a name="additional-references"></a>其他參考資料  
-   [命令列語法關鍵](command-line-syntax-key.md)  