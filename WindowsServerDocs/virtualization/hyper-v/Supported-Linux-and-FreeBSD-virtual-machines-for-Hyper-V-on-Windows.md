---
title: Windows 上的 Hyper-v 支援的 Linux 和 FreeBSD 虛擬機器
description: 列出每個版本中包含的 Linux 整合服務和功能
manager: dongill
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 3c971b3b802f1059454bc8935b638ddcc10c825c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965625"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Windows 上的 Hyper-v 支援的 Linux 和 FreeBSD 虛擬機器

>適用于： Windows Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v server 2012 R2、Windows Server 2012、Hyper-v Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

Hyper-v 支援適用于 Linux 和 FreeBSD 虛擬機器的模擬和 Hyper-v 特定裝置。 使用模擬裝置執行時，不需要安裝任何其他軟體。 不過，模擬裝置不提供高效能，而且無法利用 Hyper-v 技術所提供的豐富虛擬機器管理基礎結構。 為了充分利用 Hyper-v 提供的所有優點，最好使用適用于 Linux 和 FreeBSD 的 Hyper-v 特定裝置。 執行 Hyper-v 特定裝置所需的驅動程式集合稱為 Linux Integration Services (.LIS) 或 FreeBSD Integration Services (BIS) 。

已將 .LIS 新增至 Linux 核心，並已針對新版本進行更新。 但是以較舊核心為基礎的 Linux 散發套件可能沒有最新的增強功能或修正。 Microsoft 提供下載內容，其中包含以這些舊版核心為基礎的部分 Linux 安裝的可安裝的 .LIS 驅動程式。 因為散發廠商包含 Linux Integration Services 的版本，所以最好在安裝時安裝最新可下載版本的 .LIS （如果適用的話）。

針對其他 Linux 散發版本，系統會定期將這些變更整合到作業系統核心和應用程式中，因此不需要個別下載或安裝。

針對 10.0) 之前 (的舊版 FreeBSD 版本，Microsoft 提供的埠包含可安裝的 BIS 驅動程式，以及 FreeBSD 虛擬機器的對應守護程式。 對於較新的 FreeBSD 版本，BIS 內建于 FreeBSD 作業系統中，不需要個別下載或安裝，除了 FreeBSD 10.0 所需的 KVP 埠下載。

> [!TIP]
> - 從評估中心下載[Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 。

本內容的目標是提供資訊，協助您在 Hyper-v 上部署 Linux 或 FreeBSD。 具體的詳細資料包括：

* 需要下載及安裝 .LIS 或 BIS 驅動程式的 Linux 散發套件或 FreeBSD 版本。

* Linux 散發套件或 FreeBSD 版本，其中包含內建的 .LIS 或 BIS 驅動程式。

* 功能發佈對應，指出主要 Linux 散發套件或 FreeBSD 版本中的功能。

* 每個散發或版本的已知問題和因應措施。

* 每個 .LIS 或 BIS 功能的功能描述。

**想要提出有關特性和功能的建議嗎？** 有沒有什麼可以做得好嗎？ 您可以使用[Windows Server User Voice](https://windowsserver.uservoice.com/forums/295062-linux-support)網站來建議 hyper-v 上的 Linux 和 FreeBSD 虛擬機器的新特性和功能，以及查看其他人的看法。

## <a name="in-this-section"></a>本節內容

* [Hyper-v 上支援的 CentOS 和 Red Hat Enterprise Linux 虛擬機器](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V 上支援的 Debian 虛擬機器](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支援的 Oracle Linux 虛擬機器](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支援的 SUSE 虛擬機器](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支援的 Ubuntu 虛擬機器](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支援的 FreeBSD 虛擬機器](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上 Linux 和 FreeBSD 虛擬機器的功能描述](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [在 Hyper-v 上執行 Linux 的最佳做法](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [在 Hyper-v 上執行 FreeBSD 的最佳做法](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
