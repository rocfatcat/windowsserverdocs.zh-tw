---
title: 應在虛擬機器中啟用顯示介面卡，以提供影片功能
description: 此最佳做法分析程式規則的線上版本文字。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ba22545a0e1d66a0f0d8f03dd7f7a42054a41d44
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960611"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>應在虛擬機器中啟用顯示介面卡，以提供影片功能

>適用於：Windows Server 2016



*如需最佳做法和掃描的詳細資訊，請參閱*[最佳做法分析](https://go.microsoft.com/fwlink/?LinkId=122786)程式。

|屬性|詳細資料|
|-|-|
|**作業系統**|Windows Server 2016|
|**產品/功能**|Hyper-V|
|**嚴重性**|警告|
|**類別**|組態|

在下列各節中，斜體表示在此問題的最佳做法分析程式工具中出現的 UI 文字。

## <a name="issue"></a>問題

*Microsoft 虛擬機器匯流排 Video 裝置可能已在虛擬機器中停用。*

Microsoft 虛擬機器匯流排 Video 裝置是針對與 Hyper-v 虛擬機器搭配使用而優化的虛擬視訊卡。 當虛擬機器未設定為使用 Microsoft 虛擬機器匯流排 Video 裝置時，會使用舊版視訊卡。 Microsoft 虛擬機器匯流排 Video 裝置的執行效果優於舊版視訊卡。

## <a name="impact"></a>影響

*下列虛擬機器的影片效能將會降低：*

\<list of virtual machine names>

## <a name="resolution"></a>解決方法

*使用客體作業系統中的 Device Manager 來啟用 Microsoft 虛擬機器匯流排視頻裝置。*

使用 Device Manager 所需的步驟會根據作業系統而有所不同。 如需指示，請參閱客體作業系統中的說明。



