---
title: Windows Vista 應該使用建議的記憶體數量來設定
description: 提供指示來解決此 Best Practices Analyzer 規則所回報的問題。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 64f4e53b-4adb-4e1d-bc48-c24f5f9d222f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ba96b713bc838ec1ebfc577df7cbbeeb39b1c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826299"
---
# <a name="windows-vista-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Vista 應該使用建議的記憶體數量來設定

>適用於：Windows Server 2016

如需最佳做法和掃描的詳細資訊，請參閱 [最佳做法分析程式](https://go.microsoft.com/fwlink/?LinkId=122786)。  
  
|屬性|詳細資料|  
|-|-|  
|**作業系統**|Windows Server 2016|  
|**產品/功能**|Hyper-V|  
|**Severity**|警告|  
|**分類**|組態|  
  
在下列章節中，斜體表示會出現在此問題的最佳做法分析程式工具的 UI 文字。  
  
## <a name="issue"></a>問題  
  
*執行 Windows Vista 的虛擬機器已使用少於 1 gb 的 RAM 建議數量。*  
  
## <a name="impact"></a>影響  
  
*客體作業系統和應用程式可能執行效能不佳。不可能記憶體不足，無法同時執行多個應用程式。這會影響下列虛擬機器：*  
  
\<清單中的虛擬機器名稱 >  
  
## <a name="resolution"></a>解析度  
  
*您可以使用 HYPER-V 管理員來增加配置給此虛擬機器至少 1 GB 的記憶體。*  
  
### <a name="to-increase-the-memory-allocated-to-a-virtual-machine"></a>若要增加配置給虛擬機器的記憶體  
  
1.  開啟 \[Hyper-V 管理員\]。 按一下 [開始]，指向 [系統管理工具]，然後按一下 [Hyper-V 管理員]。  
  
2.  在 [結果] 窗格中，在**虛擬機器**，選取您想要設定的虛擬機器。 虛擬機器的狀態應該會列為**關閉**。 如果沒有，請以滑鼠右鍵按一下 虛擬機器，然後按一下**關機**。  
  
3.  在 [執行] 窗格的虛擬機器名稱之下，按一下 [設定]。  
  
4.  在 [導覽] 窗格中，按一下**記憶體**。  
  
5.  在 **記憶體**頁面上，將**啟動 RAM**為至少 1 GB，然後按一下**確定**。  
  
### <a name="increase-the-memory-using-windows-powershell"></a>增加使用 Windows PowerShell 的記憶體  
  
1.  開啟 Windows PowerShell。 (從桌面上，按一下**開始**，並開始輸入**Windows PowerShell**。)  
  
2.  以滑鼠右鍵按一下**Windows PowerShell**然後按一下**系統管理員身分執行**。  
  
3.  執行此命令之後取代\<MyVM > 您的虛擬機器的名稱：  
  
```  
Set-VMMemory <MyVM> -StartupBytes 1GB  
```  
  
## <a name="see-also"></a>另請參閱  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  

