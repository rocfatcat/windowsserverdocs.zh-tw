---
title: 詞彙
description: 定義 MultiPoint 服務中的單字、詞彙和概念
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 807bce1d-b993-49c6-9783-b01a3c55846c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: f6e98bd7f867cedb533e6e476f53f90a469ecdaf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970655"
---
# <a name="glossary"></a>詞彙
**關聯站**指定哪一個監視器用於哪些工作站和週邊裝置，例如鍵盤和滑鼠。 針對直接視頻連接的工作站，當系統提示您執行此動作時，請按下站鍵盤上的指定按鍵來完成此動作。 若是 USB 零用戶端連線的工作站，這通常會自動發生。

**匯流排驅動的中樞**從電腦的 USB 介面繪製所有電源的中樞。 匯流排驅動的中樞不需要個別的電源連線。 不過，許多裝置無法使用這種類型的中樞，因為其所需的電源比此中樞類型所提供的還要多。

**主控台模式**MultiPoint 服務的其中一種模式可以啟動。 當系統處於主控台模式時，沒有可供使用的工作站。 相反地，所有監視器都會被視為電腦系統之主控台會話的單一延伸桌面。 主控台模式通常用來安裝、更新或設定軟體，這在電腦處於工作站模式時無法完成。 另請參閱：*站模式*。

**直接連接視頻的站**一種 MultiPoint 工作站，其中包含直接連線到伺服器上影片輸出的監視器，而且至少會包含透過 USB 集線器連接到伺服器的鍵盤和滑鼠。

**網域使用者帳戶**在網域電腦上主控的使用者帳戶。 網域使用者帳戶可以從任何連線到網域的電腦存取，而且不會系結至任何特定的電腦。

**下游中樞**連線到站中樞的中樞，可為工作站裝置新增更多可用的埠。 下游中樞不能連接鍵盤。

**外部供電的集線器**此中樞也稱為自我供電中樞，可從外部電源供應器取得其電力;因此，它可以提供每個埠最多 500 mA) 的完整電源 (。 許多中樞可以做為以匯流排為技術或以外部為中心的集線器運作。

**HID 取用者控制裝置**人類介面裝置 (HID) 是直接與人類互動的電腦裝置。 它可能會接受輸入或將輸出傳遞給人類。 範例包括鍵盤、滑鼠、軌跡球、觸控板、指向卡、圖形資料表、搖桿、指紋掃描器、遊戲台、網路攝影機、耳機和駕駛模擬器裝置。 HID 取用者控制裝置是特定類別的 HID 裝置，其中包含音訊音量控制和多媒體和瀏覽器控制金鑰。

**中繼中樞**在伺服器上的*根中樞*與站中樞之間的中樞。 中繼中樞通常用來增加工作站中樞的可用埠數目，或延長工作站與電腦之間的距離。

**本機使用者帳戶**特定電腦上的使用者帳戶。 本機使用者帳戶只能在已定義帳戶的電腦上使用。

**多功能集線器**請參閱*USB 零用戶端*。

**MultiPoint 服務系統**由一部電腦所組成的硬體和軟體集合，其中包含安裝了 MultiPoint 服務角色且至少有一個 MultiPoint 工作站的 Windows Server 2016。 如需系統版面配置選項的詳細資訊，請參閱[MultiPoint 服務網站規劃](MultiPoint-services-Site-Planning.md)

**分割**區實體磁片上的空間區段，其功能就如同另一個磁片。

**主要工作站**當 MultiPoint 服務啟動時，第一個要啟動的工作站。 系統管理員可以使用主要工作站來存取啟動功能表和設定。 當系統管理員未使用它時，可以使用它做為正常的工作站 (不需要為系統管理) 專門保留。 主要工作站的監視必須一律直接連線到執行 MultiPoint 服務之電腦上的影片輸出。 另請參閱：工作站。

透過**區域網路連線的工作站**一部是瘦用戶端、傳統桌上型電腦或筆記本電腦的工作站，使用遠端桌面通訊協定 (RDP) 透過區域網路 (LAN) 連線到 MultiPoint 服務。

**根中樞**一種 USB 集線器，內建于電腦主機板上的主機控制器。

**分割畫面**可以使用單一監視器來顯示兩個獨立使用者桌面的工作站。 兩組集線器、鍵盤和滑鼠都會與單一監視器相關聯。 其中一個集合與監視器的左側相關聯，另一個集合則與監視的右側相關聯。

**標準站**相對於*主要工作站*（可由系統管理員用來存取啟動功能表），標準電臺不會顯示啟動功能表，而且只能在 MultiPoint 服務完成啟動程式之後使用。 另請參閱：工作站。

*站*用來連接到執行 MultiPoint 服務之電腦的使用者端點。 支援的工作站類型有三種：直接連接視頻、USB-零用戶端連線，以及由 RDP over LAN 連線的工作站。 如需有關工作站的詳細資訊，請參閱[MultiPoint 電臺](MultiPoint-services-Stations.md)。

**站中樞**與監視相關聯的 USB 集線器，以建立 MultiPoint 工作站。 它會將週邊 USB 裝置連接到 MultiPoint 服務。另請參閱： *USB 零用戶端*和*usb 集線器*。

**工作站模式**MultiPoint 服務的其中一種模式可以啟動。 MultiPoint 服務系統通常是站模式。 在工作站模式中，MultiPoint 服務站的行為會如同每個工作站是執行 Windows 作業系統的個別電腦，而多個使用者可以同時使用系統。 另請參閱：*主控台模式*。

**USB 集線器**符合通用序列匯流排 (USB) 2.0 或更新版本規格的一般多埠 USB 擴充集線器。 這類中樞通常會有數個 USB 埠，可讓多個 USB 裝置連接到電腦上的單一 USB 埠。 USB 集線器通常是獨立的裝置，可以是*外部電源*或*匯流排驅動*。 有些其他裝置（例如某些鍵盤和視頻監視器）可能會在其設計中納入 USB 集線器。 另請參閱： *USB 零用戶端*。

**USB Over Ethernet 零用戶端**USB 零用戶端，透過 LAN 連線而非 USB 埠連接到電腦。 此用戶端會以 USB 裝置的形式顯示在伺服器上，即使透過乙太網路連線傳送資料也一樣。

**USB 零用戶端**透過 USB 埠連接到電腦的擴充中樞，可讓您將各種不同的非 USB 裝置連線到中樞。 USB 零用戶端是由特定硬體製造商所產生，而且需要安裝裝置特定驅動程式。 USB 零用戶端支援透過 VGA、DVI 等) ，以及透過 USB (的週邊設備（有時是 PS/2 和類比音訊) ）來連接影片監視器 (。 USB 零用戶端可以是*外部電源*或*匯流排驅動*。 另請參閱「USB 集線器」**。

**USB 零用戶端連線的工作站**一種 MultiPoint 服務站，其中包含的 (最小) 監視器、鍵盤及滑鼠，這會透過 USB 零用戶端連線到伺服器。

