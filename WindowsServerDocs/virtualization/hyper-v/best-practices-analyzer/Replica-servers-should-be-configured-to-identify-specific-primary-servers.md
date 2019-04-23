---
title: 複本伺服器應該設定為識別特定授權傳送複寫流量的主要伺服器
description: 提供指示來解決此 Best Practices Analyzer 規則所回報的問題。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 47b215d4c84e68d93ae1189ddd370358e2781eff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822239"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>複本伺服器應該設定為識別特定授權傳送複寫流量的主要伺服器

>適用於：Windows Server 2016

如需最佳做法與掃描的相關詳細資訊，請參閱[執行最佳做法分析程式掃描及管理掃描結果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。  
  
|屬性|詳細資料|  
|-|-|  
|**作業系統**|Windows Server 2016|  
|**產品/功能**|Hyper-V|  
|**Severity**|警告|  
|**分類**|組態|  
  
在下列章節中，斜體表示會出現在此問題的最佳做法分析程式工具的 UI 文字。  
  
## <a name="issue"></a>問題  
*所設定，則這個複本伺服器接受複寫流量的所有主要伺服器，並將它們儲存在單一位置。*  
  
### <a name="impact"></a>影響  
*所有的複寫，從所有主要伺服器會儲存在單一位置，可能會造成隱私權或安全性問題。*  
  
## <a name="resolution"></a>解析度  
*您可以使用 HYPER-V 管理員來建立特定的主要伺服器的新授權項目，並指定為每個個別的存放位置。您可以使用萬用字元來分組為每個授權項目集的主要伺服器。*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>建立使用 HYPER-V 管理員的授權項目  
  
1.  開啟 \[Hyper-V 管理員\]。 (從 [伺服器管理員] 中，按一下**工具** > **HYPER-V 管理員**。)  
  
2.  從清單中的主機，請以滑鼠右鍵按一下，然後按一下其中一個**HYPER-V 設定**。  
  
3.  在 [導覽] 窗格中，按一下**複寫組態**。  
  
4.  底下**授權與存放裝置**，按一下**允許來自指定伺服器的複寫**。  
  
5.  底下的 伺服器清單中，按一下 **新增**。  
  
6.  底下**新增的授權項目**:  
  
    -   輸入第一部伺服器的完整限定的名稱。  
  
    -   指定專用的位置來儲存只有該伺服器的檔案。  
  
7.  按一下 [確定] 。  
  
8.  針對每一部主要伺服器重複。  
  
9. 按一下 **確定**一次以完成並關閉視窗。  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>建立使用 Windows PowerShell 的授權項目  
  
1.  開啟 Windows PowerShell。 (從桌面上，按一下 [開始]，並開始輸入**Windows PowerShell**。)  
  
2.  以滑鼠右鍵按一下**Windows PowerShell**然後按一下**系統管理員身分執行**。  
  
3.  執行類似下列的命令，並將：  
  
    -   主要伺服器名稱 server01.domain01.contoso.com 與您伺服器的完整的網域名稱。  
  
    -   以您位置 D:\ReplicaVMStorage 位置。  
  
    -   如果您已建立一個，信任群組名為您的群組名稱，預設值。 如果沒有，則使用預設值。  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  
## <a name="see-also"></a>另請參閱  
[New-VMReplicationAuthorizationEntry](https://technet.microsoft.com/library/hh848606.aspx)  
  

