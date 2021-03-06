---
title: 在伺服器上設定 WinSAT 分數
description: 說明如何使用 Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 56769966cbfb6778c06abc4ba07d21f258e900a4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623347"
---
# <a name="set-the-winsat-score-on-the-server"></a>在伺服器上設定 WinSAT 分數

>適用于： Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

您應該為執行 Windows Server Essentials 作業系統的伺服器設定 WinSAT CPU 分數，以優化影片串流解析度。 建立並安裝含有 WinSAT 分數資訊的 .xml 檔案，即可達到此目的。

## <a name="obtain-the-winsat-cpu-score"></a>取得 WinSAT CPU 分數
 OPK 隨附一個名為 WinServerSAT.exe 的程式，這個程式會探索 WinSAT CPU 分數，並將該資訊放置在作業系統會讀取的 WinServerSAT.xml 檔案中。

#### <a name="to-obtain-the-winsat-cpu-score"></a>若要取得 WinSAT CPU 分數

1. 將 \\ ADK 媒體中的 Resources\WinServerSAT * 複製到參照電腦。

2. 在參照電腦上，開啟提高權限的命令提示字元視窗。

3. 如果 %ProgramFiles%\Windows Server\Bin\OEM 資料夾不存在，請輸入以下命令，然後按 Enter。

    **mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**

4. 輸入以下命令，然後按 Enter。

    **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**

   以下範例顯示已建立的 WinServerSAT.xml 檔案的 XML 內容。

```

<?xml version="1.0" encoding="UTF-16"?>
<WinSAT>
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>
</WinSAT>
```

 其中 *WinSAT_Score* 會以在伺服器上探索的值取代。

> [!IMPORTANT]
>  在擷取映像之前，您必須先將參照電腦上的 WinServerSAT.exe、winsat.prx、winsat.wmv 和 WinSATEncode.wmv 檔案移除。
