---
title: 針對在生產環境中執行伺服器工作負載的虛擬機器，不建議使用 VHD 格式的動態虛擬硬碟
description: 此最佳做法分析程式規則的線上版本文字。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 4865fcbc75ac135a6fe04622692aaf1ce2893a3a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960251"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>針對在生產環境中執行伺服器工作負載的虛擬機器，不建議使用 VHD 格式的動態虛擬硬碟

>適用於：Windows Server 2016

如需最佳做法與掃描的相關詳細資訊，請參閱[執行最佳做法分析程式掃描及管理掃描結果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。

|屬性|詳細資料|
|-|-|
|**作業系統**|Windows Server 2016|
|**產品/功能**|Hyper-V|
|**嚴重性**|警告|
|**類別**|組態|

在下列各節中，斜體表示在此問題的最佳做法分析程式工具中出現的 UI 文字。

## <a name="issue"></a>**問題**
*一或多部虛擬機器使用 VHD 格式動態擴充虛擬硬碟。*

## <a name="impact"></a>**影響**
*如果發生電源中斷，VHD 格式的動態虛擬硬碟可能會遇到一致性問題。如果實體磁片對 .vhd 檔案中的磁區執行了不完整或不正確的更新，但發生電源中斷時，就會發生一致性問題。這會影響下列虛擬機器：*

\<list of virtual machines>

## <a name="resolution"></a>**解決方案**
*關閉虛擬機器，並將 VHD 格式的動態虛擬硬碟轉換成 VHDX 格式的虛擬硬碟或固定的虛擬硬碟。 (VHDX 格式具有可靠性機制，可協助保護磁片因系統電源故障而損毀 ) 。不過，如果在某個時間點可能會附加至舊版 Windows，請不要轉換虛擬硬碟。Windows Server 2012 之前的 windows 版本不支援 VHDX 格式。*



