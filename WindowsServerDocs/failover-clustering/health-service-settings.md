---
title: 健全狀況服務設定
manager: eldenc
ms.author: cosdar
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 389dfa8890e67b3caf7d9ec6fb69b16ae6a8083b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953380"
---
# <a name="health-service-settings"></a>健全狀況服務設定

> 適用於：Windows Server 2019、Windows Server 2016

健全狀況服務是 Windows Server 2016 中的新功能，可改善執行儲存空間直接存取之叢集的日常監視和操作體驗。

許多管理健全狀況服務行為的參數都會公開為設定。 您可以修改這些資訊來微調錯誤或動作的增強功能、開啟/關閉特定行為，以及執行其他操作。

使用下列 PowerShell Cmdlet 來設定或修改設定。

### <a name="usage"></a>使用狀況

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>
```

#### <a name="example"></a>範例

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>一般設定

以下列出一些經常修改的設定，以及其預設值。

#### <a name="volume-capacity-threshold"></a>磁片區容量閾值

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>集區保留容量閾值

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>實體磁片生命週期

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>支援的元件檔

請參閱上一節。

#### <a name="firmware-rollout"></a>固件推出

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Platform/靜止

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>計量

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>偵錯

```
"System.LogLevel" = 4
```

## <a name="additional-references"></a>其他參考資料

- [Windows Server 2016 中的健全狀況服務](health-service-overview.md)
- [Windows Server 2016 中的儲存空間直接存取](../storage/storage-spaces/storage-spaces-direct-overview.md)
