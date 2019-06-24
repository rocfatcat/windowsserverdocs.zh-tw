---
ms.assetid: 342173ca-4e10-44f4-b2c9-02a6c26f7a4a
title: 規劃儲存空間直接存取中的磁碟區
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: c68444be5662480293cee630970d5eb76b52268a
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453192"
---
# <a name="planning-volumes-in-storage-spaces-direct"></a>規劃儲存空間直接存取中的磁碟區

> 適用於：Windows Server 2019，Windows Server 2016

此主題提供如何規劃儲存空間直接存取中的磁碟區，符合您工作負載的效能與容量需要，包括選擇它們的系統、復原類型和大小。

## <a name="review-what-are-volumes"></a>檢閱：磁碟區有哪些？

磁碟區是資料存放區，這裡放置您工作負載需要的檔案，例如用於 Hyper-V 虛擬機器的 VHD 或 VHDX 檔案。 磁碟區結合儲存集區的磁碟機，導入儲存空間直接存取的容錯、延展性和效能好處。

   >[!NOTE]
   > 在儲存空間直接存取的文件中，我們將磁碟區和其下的虛擬磁碟，包括提供其他內建 Windows 功能如叢集共用磁碟區 (CSV) 和 ReFS 所提供的功能，合稱為「磁碟區」一詞。 成功計劃及順利部署儲存空間直接存取，不需要了解這些實作層級區別。

![what-are-volumes](media/plan-volumes/what-are-volumes.png)

所有磁碟區可以由叢集中所有伺服器同時存取。 建立之後，它們會顯示在**C:\ClusterStorage\\** 所有伺服器上。

![csv-folder-screenshot](media/plan-volumes/csv-folder-screenshot.png)

## <a name="choosing-how-many-volumes-to-create"></a>選擇建立多少磁碟區

我們建議磁碟區數目是您叢集中伺服器數目的倍數。 例如，如果您有 4 部伺服器，則會發生更一致的效能，使用 4 個總計超過包含的磁碟區 3 或 5。 這可以讓叢集在伺服器之間平均分配磁碟區「擁有權」（針對每個磁碟區，一個伺服器處理中繼資料協調流程）。

建議您限制磁碟區的總數：

| Windows Server 2016          | Windows Server 2019          |
|------------------------------|------------------------------|
| 每個叢集最多 32 個磁碟區 | 每個叢集最多 64 個磁碟區 |

## <a name="choosing-the-filesystem"></a>選擇檔案系統

我們建議將新的[復原檔案系統 (ReFS)](../refs/refs-overview.md) 用於儲存空間直接存取。 ReFS 是專為模擬化用途打造的頂級檔案系統，提供許多好處，包括大幅效能加速和內建的資料毀損保護。 它支援幾乎所有 NTFS 的重要功能，包括 Windows Server 1709 版和更新版本中的重複資料刪除。 請參閱 ReFS[功能比較表](../refs/refs-overview.md#feature-comparison)如需詳細資訊。

如果您的工作負載需要 ReFS 尚未支援的功能，您可以改為使用 NTFS。

   >[!TIP]
   > 有不同檔案系統的磁碟區可以同時存在於相同叢集中。

## <a name="choosing-the-resiliency-type"></a>選擇復原類型

儲存空間直接存取中的磁碟區提供復原功能，防範硬體問題，例如磁碟機或伺服器故障，以及在整個伺服器維護期間 (例如軟體更新) 啟用持續可用性。

   >[!NOTE]
   > 可以選擇的復原類型，不受您擁有的磁碟機類型影響。

### <a name="with-two-servers"></a>具有兩部伺服器

具有兩個伺服器的叢集的唯一選項是雙向鏡像。 這保留所有資料的兩份複本，每個伺服器的磁碟機上各有一份複本。 其儲存效率是 50%，因此若要撰寫 1 TB 的資料，儲存集區需要至少 2 TB 的實體儲存容量。 雙向鏡像可以放心地一次容許一部硬體故障（磁碟機或伺服器）。

![two-way-mirror](media/plan-volumes/two-way-mirror.png)

如果您有兩個以上伺服器，我們建議改為使用下列一種復原類型。

### <a name="with-three-servers"></a>具有三部伺服器

有三種伺服器，您應該使用三向鏡像，以取得更好的容錯和效能。 三向鏡像保留所有資料的三份複本，每個伺服器的磁碟機上各有一份複本。 其儲存效率是 33.3%，因此若要撰寫 1 TB 的資料，儲存集區需要至少 3 TB 的實體儲存容量。 三向鏡像可安全地[一次容許至少兩個硬體問題（磁碟機或伺服器）](storage-spaces-fault-tolerance.md#examples)。 如果 2 個節點變成無法使用儲存體集區會失去仲裁，，因為 2/3 的磁碟無法使用，而虛擬磁碟將會無法存取。 不過，節點可以是下另一個節點上的一個或多個磁碟可能會失敗並將虛擬磁碟會保持離線狀態。 例如，如果您重新開機一部伺服器，同時突然另一部磁碟機或伺服器故障，所有資料會保持安全，持續可供存取。

![three-way-mirror](media/plan-volumes/three-way-mirror.png)

### <a name="with-four-or-more-servers"></a>具有四個以上伺服器

使用四個或更多的伺服器，您可以選擇每個磁碟區使用三向鏡像、雙同位（通常稱為「清除編碼」）或兩者組合。

雙同位提供與三向鏡像相同的容錯功能，但具有更佳的儲存效率。 使用四個伺服器，其儲存效率是 50.0%，因此若要儲存 2 TB 的資料，儲存集區需要至少 4 TB 的實體儲存容量。 使用七部伺服器時增加到 66.7% 儲存效率，並持續增至 80.0% 儲存效率。 缺點是同位編碼大量耗用運算資源，這可能會限制其效能。

![dual-parity](media/plan-volumes/dual-parity.png)

要使用的復原類型，端視您的工作負載需求。 以下是摘要說明哪些工作負載是不錯的選擇，每個復原類型，以及每個復原類型的效能和儲存體效率的資料表。

| **復原類型**| **容量效率**| **速度**| **工作負載**
|--------------------|--------------------------------|--------------------------------|--------------------------
| **鏡像**         | ![儲存體效率顯示 33%](media/plan-volumes/3-way-mirror-storage-efficiency.png)<br>三向鏡像：33% <br>Two-雙向鏡像：50%     |![效能顯示 100%](media/plan-volumes/three-way-mirror-perf.png)<br> 最高的效能  | 虛擬化工作負載<br> 資料庫<br>其他的高效能工作負載 |
| **鏡像加速的同位** |![顯示大約 50%的儲存空間效率](media/plan-volumes/mirror-accelerated-parity-storage-efficiency.png)<br> 取決於鏡像和同位檢查的比例 | ![顯示大約 20%的效能](media/plan-volumes/mirror-accelerated-parity-perf.png)<br>遠低於鏡像，但最多兩倍速度雙同位<br> 最適合大型循序寫入和讀取 | 封存與備份<br> 虛擬桌面基礎結構     |
| **Dual-parity**               | ![顯示大約 80%的儲存空間效率](media/plan-volumes/dual-parity-storage-efficiency.png)<br>4 部伺服器：50% <br>16 部伺服器： 最多 80% | ![顯示大約 10%的效能](media/plan-volumes/dual-parity-perf.png)<br>最高的 I/O 延遲和寫入的 CPU 使用量<br> 最適合大型循序寫入和讀取 | 封存與備份<br> 虛擬桌面基礎結構  |

#### <a name="when-performance-matters-most"></a>當效能是最重要時

有嚴格延遲需求，或需要很多混合隨機 IOPS (例如 SQL Server 資料庫或重視效能的 Hyper-V 虛擬機器) 的工作負載，應該執行於使用鏡像的磁碟區上，以達到最佳效能。

   >[!TIP]
   > 鏡像比任何其他復原類型都還要快速。 我們幾乎所有的效能範例都會使用鏡像。

#### <a name="when-capacity-matters-most"></a>當容量最關緊要時

不常寫入的工作負載 (例如資料倉儲或「冷」的儲存空間)，應該執行於使用雙同位的磁碟區上，將儲存效率最大化。 某些其他工作負載，例如傳統檔案伺服器、虛擬桌面基礎結構 (VDI)，或不會建立許多快速飄移隨機 IO 流量和/或不需要最佳效能的其他項目，在您的審慎考慮後，也可以使用雙同位。 相較於鏡像，同位不可避免地增加 CPU 使用率和 IO 延遲，尤其是在寫入時。

#### <a name="when-data-is-written-in-bulk"></a>當大量寫入資料時

在大型、連續行程中寫入的工作負載 (例如封存或備份目標)，有另一種 Windows Server 2016 的新選項：一個磁碟區可以混合鏡像和雙同位。 寫入首先登陸鏡像部分，稍後逐漸移動至同位部分。 當大型寫入到達時，這會加速擷取並減少資源使用，藉由允許大量耗用運算資源的同位編碼以較長的時間發生。 當調整鏡像部分和同位部分大小，請考慮將一次發生的寫入數量（例如一次每日備份）應該會舒適地放在鏡像部分中。 例如，如果您每日一次擷取 100 GB，考慮使用 150 GB 到 200 GB 的鏡像，其他部分則使用雙同位。

結果儲存效率視您選擇的比例而定。 如需範例，請參閱[此示範](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)。

   >[!TIP]
   > 如果您中途透過資料 injestion 觀察寫入效能突然下降，它可能表示鏡像部分並不夠大，或鏡像加速同位檢查不是適合您的使用案例。 例如，如果從 400 MB/秒的效能會降低寫入 40 MB/秒，請考慮擴充鏡像部分，或切換至 三向鏡像。

### <a name="about-deployments-with-nvme-ssd-and-hdd"></a>關於 NVMe、SSD 和 HDD 部署

在具有兩種磁碟機類型的部署中，較快的磁碟機提供快取，而較慢的磁碟機提供容量。 這是自動發生 – 如需詳細資訊，請參閱[了解儲存空間直接存取中的快取](understand-the-cache.md)。 在這類部署，所有磁碟區最終放在同一個類型的磁碟機 – 容量磁碟機上。

在具有全部三種磁碟機類型的部署中，只有最快的磁碟機 (NVMe) 提供快取，並讓其他兩種類型的磁碟機（SSD 及 HDD）提供容量。 針對每個磁碟區，您可以選擇將它完全放在 SSD 層上、完全放在 HDD 層上，或是它橫跨這兩個。

   >[!IMPORTANT]
   > 我們建議使用 SSD 層，將最重視效能的工作負載放在全快閃裝置上。

## <a name="choosing-the-size-of-volumes"></a>選擇磁碟區大小

我們建議您限制每個磁碟區的大小：

| Windows Server 2016 | Windows Server 2019 |
|---------------------|---------------------|
| 最高 32 TB         | 最高 64 TB         |

   >[!TIP]
   > 如果您使用依賴磁碟區陰影複製服務 (VSS) 和 Volsnap 軟體提供者的備份解決方案 (伺服器工作負載的常見情況)，將磁碟區大小限制為 10 TB，將會改進效能與可靠性。 使用較新 Hyper-V RCT API 和/或 ReFS 區塊複製和/或原生 SQL 備份 API 的備份解決方案，磁碟區大小達到 32 TB 以上時也可以順利執行。

### <a name="footprint"></a>使用量

磁碟區大小是指其可用容量，可以儲存的資料量。 這是由 **New-Volume** cmdlet 的 **-Size** 參數提供，然後當您執行 **Get-Volume** cmdlet 時顯示在 **Size** 屬性中。

大小不同於磁碟區*使用量*，它占儲存集區的實體儲存總容量。 使用量視其復原類型而定。 例如，使用三向鏡像的磁碟區有其大小三倍大的使用量。

磁碟區使用量需要放在儲存集區中。

![size-versus-footprint](media/plan-volumes/size-versus-footprint.png)

### <a name="reserve-capacity"></a>保留容量

在儲存集區中保留某些容量，提供磁碟空間在磁碟機故障之後「就地」修復，而改進資料安全性與效能。 如果容量充足，立即、就地、平行修復甚至可以在故障的磁碟機更換之前將磁碟區還原為完整復原。 此動作會自動執行。

我們建議每個伺服器保留相當於一個容量磁碟機的容量，最多 4 個磁碟機。 在您的審慎考慮後，您可以保留更多，但這個最低建議保證任何磁碟機故障之後的立即、就地、平行修復成功。

![reserve](media/plan-volumes/reserve.png)

例如，如果您有 2 部伺服器並使用數個 1 TB 容量磁碟機，將集區的 2 x 1 = 2 TB 設定為保留。 如果您有 3 部伺服器和數個 1 TB 容量磁碟機，設定 3 x 1 = 3 TB 為保留。 如果您有 4 部以上伺服器和數個 1 TB 容量磁碟機，設定 4 x 1 = 4 TB 為保留。

   >[!NOTE]
   > 在具有全部三種磁碟機類型 (NVMe + SSD + HDD) 的叢集中，我們建議每個伺服器保留相當於一個 SSD 加上一個 HDD 的容量，每個伺服器最多 4 個磁碟機。

## <a name="example-capacity-planning"></a>範例：容量計劃

請考慮一個有四部伺服器的叢集。 每個伺服器擁有一些快取磁碟機，加上 16 個 2 TB 磁碟機的容量。

```
4 servers x 16 drives each x 2 TB each = 128 TB
```

從這個儲存集區的 128 TB 中，我們將保留四個磁碟機 (或 8 TB)，以便在磁碟機故障之後進行就地修復，不需要急著更換磁碟。 集區中剩下 120 TB 實體儲存容量，我們可用來建立磁碟區。

```
128 TB – (4 x 2 TB) = 120 TB
```

假設我們的部署需要裝載某些高度活躍 Hyper-V 虛擬電腦，但是我們也有很多冷儲存空間儲存寒冷 – 要保留的舊檔案和備份。 因為我們有四部伺服器，我們建立四個磁碟區。

我們將在虛擬機器放在前兩個磁碟區，*Volume1* 和 *Volume2*。 我們選擇 ReFS 做為檔案系統（適用於更快速的建立和檢查點）和三向鏡像復原類型以達到最佳效能。 我們將冷儲存空間放在其他兩個磁碟區 *Volume 3* 和 *Volume 4*。 我們選擇 NTFS 做為檔案系統 (適用於重複資料刪除) 和雙同位復原類型，將容量最大化。

我們不需要讓所有磁碟區大小相同，但為了簡化，例如我們可以讓它們全部都是 12 TB。

*Volume1* 和 *Volume2* 每個佔用 12 TB x 33.3% 效率 = 36 TB 的實體儲存空間容量。

*Volume3* 和 *Volume4* 每個佔用 12 TB x 50.0% 效率 = 24 TB 的實體儲存空間容量。

```
36 TB + 36 TB + 24 TB + 24 TB = 120 TB
```

四個磁碟區上可完全容納在我們集區中的可用實體儲存空間容量。 完美！

![範例](media/plan-volumes/example.png)

   >[!TIP]
   > 您不需要立即建立所有磁碟區。 您隨時可以延伸磁碟區，或稍後建立新的磁碟區。

為了簡化，這整個範例使用十進位 (以 10 為底數) 單位，表示 1 TB = 1,000,000,000,000 位元組。 不過，Windows 中的儲存數量以二進位 (以 2 為底數) 單位表示。 例如，每個 2 TB 磁碟機在 Windows 中顯示為 1.82 TiB。 同樣地，128 TB 儲存集區顯示為 116.41 TiB。 此為預期性行為。

## <a name="usage"></a>使用量

請參閱[建立儲存空間直接存取中的磁碟區](create-volumes.md)。

### <a name="see-also"></a>另請參閱

- [儲存空間直接存取概觀](storage-spaces-direct-overview.md)
- [選擇磁碟機的儲存空間直接存取](choosing-drives.md)
- [容錯與儲存空間效率](storage-spaces-fault-tolerance.md)