---
title: 監視連線的遠端用戶端以查看其活動和狀態
description: 本主題是 Windows Server 2016 中遠端存取監視和帳戶處理指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 831b429c69bdeac7a9e0aec69a7f79bf385f321f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970225"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>監視連線的遠端用戶端以查看其活動和狀態

>適用於：Windows Server (半年度管道)、Windows Server 2016

**注意：** Windows Server 2012 將 DirectAccess 與遠端存取服務 (RAS) 合併為單一遠端存取角色。

您可以使用遠端存取服務器上的管理主控台來監視遠端用戶端活動和狀態。

> [!NOTE]
> 您必須以 Domain Admins 群組成員或每部電腦上 Administrators 群組成員的身分登入，才能完成本主題中所述的工作。 如果您使用 Administrators 群組成員的帳戶登入時無法完成工作，請嘗試在使用屬於 Domain Admins 群組成員的帳戶登入時執行此項工作。

#### <a name="to-monitor-remote-client-activity-and-status"></a>監視遠端用戶端活動和狀態

1.  在 [伺服器管理員]**** 中，按一下 [工具]****，然後按一下 [遠端存取管理]****。

2.  按一下 [**報表**]，流覽至**遠端存取管理主控台**中的 [**遠端存取報告**]。

3.  按一下 [**遠端用戶端狀態**]，在 [**遠端存取管理] 主控台**中流覽至遠端用戶端活動和狀態使用者介面。

4.  您會看到已連線到遠端存取服務器的使用者清單，以及相關的詳細統計資料。 按一下清單中對應至用戶端的第一個資料列。 當您選取資料列時，[遠端使用者] 活動會顯示在 [預覽] 窗格中。

![Windows PowerShell](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>windows powershell 對等命令</em>***

下列 Windows PowerShell Cmdlet 執行與前述程序相同的功能。 在單一行中，輸入各個 Cmdlet (即使因為格式限制，它們可能會在這裡出現自動換行成數行)。

```
PS> Get-RemoteAccessConnectionStatistics
```

您可以使用下表中的欄位，根據條件選取專案來篩選使用者統計資料。

|欄位名稱|值|
|-------|-----|
|使用者名稱|遠端使用者的使用者名稱或別名。 萬用字元可以用來選取使用者群組，例如 contoso \\ * 或 \* \administrator。|
|主機名稱|遠端使用者的電腦帳戶名稱。 也可以指定 IPv4 或 IPv6 位址。|
|類型|DirectAccess 或 VPN。 如果選取 [DirectAccess]，則會列出所有使用 DirectAccess 連線的遠端使用者。 如果選取 VPN，則會列出所有使用 VPN 連線的遠端使用者。|
|ISP 位址|遠端使用者的 IPv4 或 IPv6 位址。|
|IPv4 位址|將遠端使用者連接到公司網路之通道的內部 IPv4 位址。|
|IPv6 位址|將遠端使用者連接到公司網路之通道的內部 IPv6 位址|
|通訊協定/通道|遠端用戶端所使用的轉換技術。 這是適用于 DirectAccess 使用者的 Teredo、6to4 或 IP-HTTPS，其為 VPN 使用者的 PPTP、L2TP、SSTP 或 IKEv2。|
|已存取資源|存取特定公司資源或端點的所有使用者。 對應至這個欄位的值是伺服器的主機名稱/IP 位址。|
|伺服器|用戶端連線的遠端存取伺服器。 這僅與叢集和多站台部署相關。|





