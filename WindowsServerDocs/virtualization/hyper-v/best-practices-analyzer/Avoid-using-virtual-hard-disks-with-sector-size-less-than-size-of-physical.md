---
title: 避免使用磁區大小小於儲存虛擬硬碟檔案之實體儲存體磁區大小的虛擬硬碟
description: 此最佳做法分析程式規則的線上版本文字。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ff44972fd2eae3fac89fbdd014f5cfd115f9ce23
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968495"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>避免使用磁區大小小於儲存虛擬硬碟檔案之實體儲存體磁區大小的虛擬硬碟

>適用於：Windows Server 2016

如需最佳做法與掃描的相關詳細資訊，請參閱[執行最佳做法分析程式掃描及管理掃描結果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。

|屬性|詳細資料|
|-|-|
|**運作中** <br />**系統**|Windows Server 2016|
|**產品/功能**|Hyper-V|
|**嚴重性**|警告|
|**類別**|組態|

在下列各節中，斜體表示在此問題的最佳做法分析程式工具中出現的 UI 文字。

## <a name="issue"></a>**問題**
*一或多個虛擬硬碟的實體磁區大小，小於虛擬硬碟檔案所在存放裝置的實體磁區大小。*

## <a name="impact"></a>**影響**
*使用虛擬硬碟的虛擬機器或應用程式可能會發生效能問題。這會影響下列虛擬機器：*

\<list of virtual machines>

## <a name="resolution"></a>**解決方案**
*請執行下列其中一項：*

-   *執行存放裝置遷移，將虛擬硬碟移至新的實體系統*

-   *使用 Windows PowerShell 或 WMI 來啟用 VHDX 格式的虛擬硬碟，以報告特定磁區大小*

-   *使用登錄設定來啟用 VHD 格式的虛擬硬碟，以報告4k 的實體磁區大小*



