---
title: 當父系和子系虛擬硬碟位於不同磁片區時，請避免在使用差異虛擬硬碟時啟用存放裝置服務品質
description: 此最佳做法分析程式規則的線上版本文字。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b208a7a10679804666ff41a02d4cddbb4d8c6762
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939180"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>當父系和子系虛擬硬碟位於不同磁片區時，請避免在使用差異虛擬硬碟時啟用存放裝置服務品質

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
*在不同磁片區上具有父系和子系虛擬硬碟的差異虛擬硬碟，已啟用存放裝置服務品質。*

## <a name="impact"></a>**影響**
*此設定可能會導致差異虛擬硬碟的非預期儲存服務行為，以及父和子磁片區上的其他虛擬硬碟。這會影響下列虛擬硬碟：*

\<list of virtual hard disks>

## <a name="resolution"></a>**解決方案**
*停用參照虛擬硬碟上的存放裝置服務品質，或執行存放裝置遷移，將父系和子虛擬硬碟移至相同的磁片區。*



