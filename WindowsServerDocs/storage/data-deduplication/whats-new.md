---
ms.assetid: d11acbc2-40c6-4ab2-9514-2bc3ad81499a
title: 重複資料刪除的新功能
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 04/17/2019
ms.openlocfilehash: 44a08443312d4e48b8fa518755e2a9b7aa50643c
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476090"
---
# <a name="whats-new-in-data-deduplication"></a>重複資料刪除的新功能

> 適用於：Windows Server 2019，Windows Server 2016 中，Windows Server （半年通道）

[重複資料刪除](overview.md)Windows Server 中已經最佳化，都相當好，有彈性且可管理私用雲端規模。 如需有關 Windows Server 內的軟體定義儲存堆疊的詳細資訊，請參閱[What's New in Windows Server 中的儲存體](../whats-new-in-storage.md)。

重複資料刪除會在 Windows Server 2019 有下列增強功能：

| 功能 | 新功能或更新功能 | 描述 |
|---------------|----------------|-------------|
| ReFS 支援  | 新的            | 重複資料刪除和壓縮 ReFS 檔案系統的相同磁碟區上儲存最多 10 倍的更多的資料。 (它有[只需要按一下](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be)開啟 Windows Admin Center 使用。)可變大小區塊存放區，以使用選用的壓縮最大化節省率，而多執行緒的後置處理架構，會保留效能影響最小。 支援的磁碟區最多 64 TB 及將重複資料刪除第一次的 4 TB 的每個檔案。|

重複資料刪除功能已從 Windows Server 2016 中的下列增強功能：

| 功能 | 新功能或更新功能 | 描述 |
|---------------|----------------|-------------|
| [支援大型磁碟區](whats-new.md#large-volume-support) | 已更新 | 在 Windows Server 2016 之前，使用者必須特別針對預期的變換設定磁碟區大小，而大於 10 TB 的磁碟區並不是重複資料刪除的良好候選項目。 在 Windows Server 2016 中，重複資料刪除支援最高 64 TB 的磁碟區大小。 |
| [支援大型檔案](whats-new.md#large-file-support) | 已更新 | 在 Windows Server 2016 之前，大小接近 1 TB 的檔案並不是重複資料刪除的良好候選項目。 在 Windows Server 2016 中，完全支援最高 1 TB 大小的檔案。 |
| [適用於 Nano Server 的支援](whats-new.md#nano-server-support) | 新的 | Windows Server 2016 的新 Nano 伺服器部署選項可以使用並且完全支援重複資料刪除。 |
| [簡化的備份支援](whats-new.md#simple-backup-support) | 新的 | Windows Server 2012 R2 是透過一系列的手動設定步驟來支援虛擬備份應用程式 (例如 Microsoft 的 [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx))。 Windows Server 2016 已加入新的預設使用類型 (Backup)，以便順暢地針對虛擬備份應用程式部署重複資料刪除。|
| [支援叢集 OS 輪流升級](whats-new.md#cluster-upgrade-support) | 新的 | 重複資料刪除完整支援 Windows Server 2016 新的[叢集 OS 輪流升級](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md)功能。 |

## <a name="large-volume-support"></a>支援大型磁碟區

**這個變更增加了什麼價值？**  
若要在 Windows Server 2012 R2 中取得重複資料刪除的最佳效能，必須適當調整磁碟區大小，以確保最佳化工作能跟上資料量變化或「變換」的速度。 一般來說，根據工作負載的寫入模式，這表示只有在 10 TB 或更小的磁碟區上執行重複資料刪除功能，效能才會高。

在 Windows Server 2016 中，即使在高達 64 TB 的磁碟區上執行重複資料刪除功能，還是能有相當高的效能。

**有哪些不同？**  
在 Windows Server 2012 R2 中，重複資料刪除工作管線會每個磁碟區使用一個執行緒與 I/O 佇列。 若要確保最佳化工作不會因為落後，而導致磁碟區的整體節省率降低，必須將大型資料集分割成較小的磁碟區。 適當的磁碟區大小取決於該磁碟區的預期變換。 平均而言，高變換磁碟區的最大值大約是 6-7 TB，而低變換磁碟區的大約是 9-10 TB。

在 Windows Server 2016 中，已針對每個磁碟區使用多個 I/O 佇列，將重複資料刪除工作管線重新設計為平行執行多個執行緒。 這導致先前只能將資料分割成多個較小磁碟區的效能。 下圖顯示這項變更：

![以視覺方式比較 Windows Server 2012 R2 與 Windows Server 2016 的重複資料刪除工作管線](media/server-2016-dedup-job-pipeline.png)

這些最佳化不僅適用於最佳化工作，也適用於[所有重複資料刪除工作](understand.md#job-info)。

## <a name="large-file-support"></a>支援大型檔案
**這個變更增加了什麼價值？**  
在 Windows Server 2012 R2 中，相當大型的檔案並非適合進行重複資料刪除的候選項目，原因是會讓重複資料刪除處理管線效能會降低。 在 Windows Server 2016 中，對高達 1 TB 的檔案進行重複資料刪除，還是能有相當高的效能，讓系統管理員可對更大範圍的工作負載套用重複資料刪除節省量。 例如，您可以針對一般與備份工作負載相關聯且相當大型的檔案，進行重複資料刪除。

**有哪些不同？**  
在 Windows Server 2016 中，重複資料刪除功能會利用新的資料流對應結構和其他「內部」增強功能，提升最佳化輸送量和存取效能。 此外，重複資料刪除處理管線現在可以在容錯移轉 (而不是重新啟動) 之後，繼續進行最佳化。 這些變更使得您即使對高達 1 TB 的檔案進行重複資料刪除，還是能有相當高的效能。

## <a name="nano-server-support"></a>適用於 Nano Server 的支援
**這個變更增加了什麼價值？**  
Nano 伺服器是 Windows Server 2016 中新的無周邊部署選項，所需的系統資源使用量最小、大幅加快啟動速度，而且需要的更新與重新啟動次數比 Windows Server Core 部署選項更少。 Nano 伺服器上完全支援重複資料刪除功能。 如需 Nano 伺服器的詳細資訊，請參閱[開始使用 Nano 伺服器](../../get-started/getting-started-with-nano-server.md)。

## <a name="simple-backup-support">簡化虛擬備份應用程式的設定</a>
**這個變更增加了什麼價值？**  
Windows Server 2012 R2 支援對虛擬備份應用程式進行重複資料刪除，但其需要手動調整重複資料刪除設定。 在 Windows Server 2016 中，大幅簡化了對虛擬化備份應用程式的重複資料刪除設定。 啟用磁碟區的重複資料刪除時，就像我們適用於一般用途的檔案伺服器和 VDI 的選項一樣，它會使用預先定義的 [使用類型] 選項。

## <a name="cluster-upgrade-support">支援叢集 OS 輪流升級</a>
**這個變更增加了什麼價值？**  
執行重複資料刪除的 Windows Server 容錯移轉叢集，其節點可以混合執行 Windows Server 2012 R2 版重複資料刪除功能的節點，以及執行 Windows Server 2016 版重複資料刪除功能的節點。 這項增強功能可在叢集輪流升級期間，完全存取所有重複資料刪除磁碟區的資料，允許在現有的 Windows Server 2012 R2 叢集上逐步推出新版本的重複資料刪除功能，不需要停機就能立即升級所有節點。

**有哪些不同？**<br />
使用舊版的 Windows Server，Windows Server 容錯移轉叢集會要求叢集中的所有節點都具備相同的 Windows Server 版本。 從 Windows Server 2016 開始，叢集輪流升級功能允許叢集以混合模式執行。 重複資料刪除支援這個新的混合模式叢集設定，可在輪流升級期間完全存取資料。