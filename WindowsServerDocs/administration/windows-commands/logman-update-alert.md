---
title: logman 更新警示
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8de8db0ae02b5e0ae439f9adb742bfc316abb82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847779"
---
# <a name="logman-update-alert"></a>logman 更新警示

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

更新現有的警示資料收集器的屬性。  
  
## <a name="syntax"></a>語法  
```  
logman update alert <[-n] <name>> [options]  
```  
## <a name="parameters"></a>參數  
|參數|描述|  
|-------|--------|  
|/?|顯示即時線上說明。|  
|-s <computer name>|在指定的遠端電腦上執行命令。|  
|-config <value>|指定包含命令選項的設定檔。|  
|[-n] <name>|目標物件的名稱。|  
|-[-]u <user [password]>|指定給執行身分的使用者。 輸入 * 產生密碼的提示字元的密碼。 當您輸入密碼的提示字元時，不會顯示密碼。|  
|-m <[start] [stop] [[start] [stop] [...]]>|將變更為手動啟動或停止而不是排程的開始或結束時間。|  
|-rf < [[hh:] mm:] ss >|執行指定的一段時間的資料收集器。|  
|-b <M/d/yyyy h:mm:ss[AM&#124;PM]>|開始收集資料，在指定的時間。|  
|-e <M/d/yyyy h:mm:ss[AM&#124;PM]>|結束於指定時間的資料收集。|  
|si < [[hh:] mm:] ss >|指定效能計數器資料收集器的取樣間隔時間。|  
|-o <path&#124;dsn!log>|指定的輸出記錄檔或資料來源名稱和記錄集名稱在 SQL database 中。|  
|-[-]r|重複資料收集器每日於指定的開始和結束時間。|  
|-[-]a|將附加至現有的記錄檔。|  
|-[-]ow|覆寫現有的記錄檔。|  
|-[-]v <nnnnnn&#124;mmddhhmm>|將檔案版本資訊附加至記錄檔名稱的結尾。|  
|-[-]rc <task>|執行命令，指定每個記錄檔關閉的時間。|  
|-[-]max <value>|記錄檔大小上限以 MB 或最大 SQL 記錄檔的記錄數目。|  
|-[-] cnf < [[hh:] mm:] ss >|指定時間時，請在經過指定的時間之後建立新的檔案。 未指定時間時，建立新的檔案超過大小上限時。|  
|-y|所有的問題是回應，而不提示。|  
|-cf <filename>|指定列出要收集的效能計數器的檔案。 此檔案應包含每行一個效能計數器名稱。|  
|-[-]el|啟用或停用事件記錄檔報告。|  
|第 < 臨界值 [臨界值 [...]]>|指定計數器和其警示的臨界值。|  
|-[-]rdcs <name>|指定資料收集器集合工具啟動時引發警示。|  
|-[-]tn <task>|指定當警示引發時執行的工作。|  
|-[-]targ <argument>|指定要搭配使用-tn 指定工作的工作引數。|  
## <a name="remarks"></a>備註  
當列出 [-] 時，額外的-變換正負號的選項。  
## <a name="BKMK_examples"></a>範例  
下列範例會更新現有的資料收集器 new_alert，計數器 %Processor time，40 %processor （_total） 計數器群組中的設定臨界值。  
```  
logman update alert new_alert -th "\Processor(_Total)\% Processor time>40"  
```  
#### <a name="additional-references"></a>其他參考資料  
[logman](logman.md)  
[logman 建立警示](logman-create-alert.md)  