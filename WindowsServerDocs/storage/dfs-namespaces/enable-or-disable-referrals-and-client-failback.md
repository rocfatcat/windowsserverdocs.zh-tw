---
title: 啟用或停用轉介和用戶端容錯回復
description: 本文說明如何啟用或停用轉介和用戶端容錯回復。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 20ac61f86ede938efd574fc6a048775437a51211
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835019"
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>啟用或停用轉介和用戶端容錯回復

> 適用於：Windows Server 2019，Windows Server （半年通道）、 Windows Server 2016、 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008

轉介是伺服器的排序清單，當使用者存取命名空間根目錄或包含目標的 DFS 資料夾時，用戶端電腦就會收到來自網域控制站或命名空間伺服器的轉介。 電腦接收轉介之後，就會嘗試存取清單中的第一部伺服器。 如果伺服器無法使用，用戶端電腦就會嘗試存取下一部伺服器。 如果伺服器變得無法使用，則可將用戶端設定成在恢復可用之後容錯回復到偏好的伺服器。

下列章節提供如何啟用或停用轉介和用戶端容錯回復的相關資訊：

## <a name="enable-or-disable-referrals"></a>啟用或停用轉介

透過停用命名空間伺服器或資料夾目標的轉介，可以防止使用者導向到該命名空間伺服器或資料夾目標。 這個方法在您需要暫時將伺服器離線進行維護時相當實用。

-   若要啟用或停用轉介至資料夾目標，請使用下列步驟：

    1.  在 \[DFS 管理\] 主控台樹狀目錄的 **\[命名空間\]** 節點之下，按一下包含目標的資料夾，然後按一下 **\[詳細資料\]** 窗格中的 **\[資料夾目標\]** 索引標籤。
    2.  在資料夾目標上按一下滑鼠右鍵，然後按一下 **\[停用資料夾目標\]** 或 **\[啟用資料夾目標\]**。

-   若要啟用或停用轉介至命名空間伺服器，請使用下列步驟：

    1.  在 \[DFS 管理\] 主控台樹狀目錄中，選取適當的命名空間，然後按一下 **\[命名空間伺服器\]** 索引標籤。
    2.  在適當的命名空間伺服器上按一下滑鼠右鍵，然後按一下 **\[停用命名空間伺服器\]** 或 **\[啟用命名空間伺服器\]**。


> [!TIP]
> 若要啟用或停用轉介，使用 Windows PowerShell，請使用[組 DfsnRootTarget – 狀態](https://technet.microsoft.com/library/jj884266.aspx)或是[組 DfsnServerConfiguration](https://technet.microsoft.com/library/jj884277.aspx)導入 Windows Server 2012 中的 cmdlet。

## <a name="enable-client-failback"></a>啟用用戶端容錯回復

如果目標變得無法使用，則可將用戶端設定成當目標還原後錯誤後回復到該目標。 容錯回復能夠運作，用戶端電腦必須符合下列主題中所列的需求：[檢閱 DFS 命名空間用戶端需求](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)。


> [!NOTE]
> 若要使用 Windows PowerShell 來啟用命名空間根目錄上的用戶端容錯回復，請使用 [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx) Cmdlet。 若要在 DFS 資料夾上啟用用戶端容錯回復，請使用 [Set-DfsnFolder](https://technet.microsoft.com/library/jj884283.aspx) Cmdlet。


## <a name="to-enable-client-failback-for-a-namespace-root"></a>為命名空間根目錄啟用用戶端容錯回復

1.  按一下 [開始]，指向 [系統管理工具]，然後按一下 [DFS 管理]。

2.  在主控台樹狀目錄的 [命名空間] 節點下，以滑鼠右鍵按一下命名空間，然後按一下 [內容]。

3.  在 [轉介] 索引標籤上，選取 [用戶端容錯回復至慣用目標] 核取方塊。

含目標的資料夾會繼承命名空間根目錄中的用戶端容錯回復設定。 如果在命名空間根目錄上停用用戶端容錯回復，則可使用下列程序讓用戶端容錯回復到含目標的資料夾。

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>為含目標的資料夾啟用用戶端容錯回復

1.  按一下 [開始]，指向 [系統管理工具]，然後按一下 [DFS 管理]。

2.  在主控台樹狀目錄的 [命名空間] 節點下，以滑鼠右鍵按一下含目標的資料夾，然後按一下 [內容]。

3.  在 [轉介] 索引標籤上，按一下 [用戶端容錯回復至慣用目標] 核取方塊。

## <a name="see-also"></a>另請參閱 

-   [調整 DFS 命名空間](tuning-dfs-namespaces.md)
-   [檢閱 DFS 命名空間用戶端需求](https://technet.microsoft.com/library/cc771913(v=ws.11).aspx)
-   [委派管理 DFS 命名空間的權限](delegate-management-permissions-for-dfs-namespaces.md)