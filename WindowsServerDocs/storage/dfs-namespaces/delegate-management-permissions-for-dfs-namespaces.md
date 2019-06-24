---
title: 委派 DFS 命名空間的管理權限
description: 本文描述如何委派 DFS 命名空間的管理權限，以及哪些群組預設可以執行命名空間工作
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7895432ca16dd13c6425d966f99104fc03db100d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829489"
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>委派 DFS 命名空間的管理權限

> 適用於：Windows Server 2019，Windows Server （半年通道）、 Windows Server 2016、 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008

下表描述預設可以執行基本命名空間工作的群組，以及委派執行這些工作之能力的方法：

|工作 | 預設可以執行此工作的群組 | 委派方法 |
|---|---|---|
|建立網域型命名空間|設定命名空間之網域中的 Domain Admins 群組|在主控台樹狀目錄的 **\[命名空間\]** 節點上按一下滑鼠右鍵，然後按一下 **\[委派管理權限\]**。 或使用 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) 和 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)。 Windows PowerShell Cmdlet (於 Windows Server 2012 中引進)。 您也必須新增使用者至命名空間伺服器上的本機系統管理員群組。|
|新增命名空間伺服器至網域型命名空間|設定命名空間之網域中的 Domain Admins 群組| 在主控台樹狀目錄的網域型命名空間上按一下滑鼠右鍵，然後按一下 **\[委派管理權限\]**。 或使用 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) 和 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)。 Windows PowerShell Cmdlet (於 Windows Server 2012 中引進)。 您也必須新增使用者至要新增的命名空間伺服器上的本機系統管理員群組。|
|管理網域型命名空間|每個命名空間伺服器上的本機系統管理員群組| 在主控台樹狀目錄的網域型命名空間上按一下滑鼠右鍵，然後按一下 **\[委派管理權限\]**。 |
|建立獨立命名空間|命名空間伺服器上的本機系統管理員群組| 新增使用者至命名空間伺服器上的本機系統管理員群組。 |
|管理獨立命名空間*|命名空間伺服器上的本機系統管理員群組| 在主控台樹狀目錄的獨立命名空間上按一下滑鼠右鍵，然後按一下 **\[委派管理權限\]**。 或使用 [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) 和 [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot)。 Windows PowerShell Cmdlet (於 Windows Server 2012 中引進)。|
|建立複寫群組或在資料夾上啟用 DFS 複寫|設定命名空間之網域中的 Domain Admins 群組| 在主控台樹狀目錄的 \[複寫\] 節點上按一下滑鼠右鍵，然後按一下 **\[委派管理權限\]**。 |

<br />

\*委派管理權限來管理獨立命名空間並未授與使用者能夠檢視和管理所使用的安全性**委派**索引標籤上，除非該使用者是本機 Administrators 群組的成員上命名空間伺服器。 這個問題是因為 DFS 管理嵌入式管理單元無法從登錄擷取獨立命名空間的判別存取控制清單 (DACL)。 若要啟用嵌入式管理單元顯示委派資訊，您必須遵循的步驟，在 Microsoft<sup>®</sup>眭妎踱恅：[KB314837:如何管理登錄的遠端存取](https://go.microsoft.com/fwlink?linkid=46803)