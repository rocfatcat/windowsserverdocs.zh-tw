---
title: wbadmin start recovery
description: Wbadmin 開始復原的參考文章，它會根據您指定的參數來執行復原操作。
ms.topic: reference
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 96c38a74f0a7f10e761ce1478e207666741eecc9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640254"
---
# <a name="wbadmin-start-recovery"></a>wbadmin start recovery

根據您指定的參數執行復原作業。

若要使用這個子命令執行復原，您必須是 **Backup Operators** 群組或 **Administrators** 群組的成員，或者必須已被委派適當的許可權。 此外，您必須從提升許可權的命令提示字元中執行 **wbadmin** 。  (開啟提升許可權的命令提示字元，按一下 [ **開始**]，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。 ) 

> [!NOTE]
> 使用 **wbadmin** 從媒體執行安裝之前，您應該考慮使用 **ntdsutil** 命令，因為 **ntdsutil** 只會複製所需的最少資料量，並使用更安全的資料傳輸方法。

## <a name="syntax"></a>語法

```
wbadmin start recovery
-version:<VersionIdentifier>
-items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>}
-itemtype:{Volume | App | File}
[-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}]
[-recursive]
[-overwrite:{Overwrite | CreateCopy | Skip}]
[-notRestoreAcl]
[-skipBadClusterCheck]
[-noRollForward]
[-quiet]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|--|--|
| -version | 以 MM/DD/YYYY-HH： MM 格式指定要復原的備份版本識別碼。 如果您不知道版本識別碼，請輸入 **wbadmin get**version。 |
| -items | 指定要復原之磁片區、應用程式、檔案或資料夾的逗號分隔清單。</br>-如果 **-itemtype** 是 **磁片**區，您可以藉由提供磁片區磁碟機號、磁片區掛接點或以 GUID 為基礎的磁片區名稱來指定單一磁片區。</br>-如果 **-itemtype** 是 **App**，您只能指定單一應用程式。 若要復原，應用程式必須已向 Windows Server Backup 註冊。 您也可以使用值 **ADIFM** 來復原 Active Directory 的安裝。 如需詳細資訊，請參閱中的備註。</br>-如果 **-itemtype** 是 **File**，您可以指定檔案或資料夾，但是它們應該是相同磁片區的一部分，而且應該位於相同的父資料夾。 |
| -itemtype | 指定要復原的專案類型。 必須是**磁片**區、**應用程式****或檔案**。 |
| -backupTarget | 指定包含您想要復原之備份的儲存位置。 當位置與此電腦的備份通常儲存位置不同時，此參數很有用。 |
| -電腦 | 指定您想要復原備份的電腦名稱稱。 當多部電腦備份至相同的位置時，此參數很有用。 當指定 **-backupTarget** 參數時，應使用此參數。 |
| -recoveryTarget | 指定要還原的位置。 如果這個位置與先前備份的位置不同，這個參數就很有用。 它也可以用於復原磁碟區、檔案或應用程式。 如果您要復原磁碟區，您可以指定替代磁片區的磁片區磁碟機號。 如果您要還原檔案或應用程式，您可以指定替代的復原位置。 |
| -遞迴 | 只有在復原檔案時才有效。 復原資料夾中的檔案，以及從屬於指定資料夾的所有檔案。 依預設，只會復原位於指定資料夾中的檔案。 |
| -覆寫 | 只有在復原檔案時才有效。 指定當正在復原的檔案已經存在於相同位置時要採取的動作。</br>-   **Skip** 會導致 Windows Server Backup 略過現有的檔案，並繼續進行下一個檔案的復原。</br>-   **CreateCopy** 會導致 Windows Server Backup 建立現有檔案的複本，因此不會修改現有的檔案。</br>-   **覆寫** 會導致 Windows Server Backup 使用備份中的檔案來覆寫現有的檔案。 |
| -notRestoreAcl | 只有在復原檔案時才有效。 指定不還原安全性存取控制清單 (Acl) 從備份復原的檔案。 預設會還原安全性 Acl (預設值為 **true) **。 如果使用此參數，則會從還原檔案的位置繼承還原檔案的 Acl。 |
| -skipBadClusterCheck | 只有在復原磁片區時才有效。 略過檢查您正在復原的磁片是否有錯誤的叢集資訊。 如果您要復原到替代伺服器或硬體，建議您不要使用此參數。 您可以隨時在這些磁片上手動執行命令 **chkdsk/b** 來檢查是否有錯誤的叢集，然後據此更新檔案系統資訊。</br>重要事項：在您執行 **Chkdsk** 之前（如所述），復原系統上回報的錯誤叢集可能不正確。 |
| -noRollForward | 只有在復原應用程式時才有效。 如果已選取備份的最新版本，可允許應用程式先前的時間點復原。 若是其他不是最新版本的應用程式，則先前的時間點恢復是以預設值來完成。 |
| -quiet | 執行子命令，而不提示使用者。 |

## <a name="remarks"></a>備註

-   若要查看可從特定備份版本復原的專案清單，請使用 **wbadmin get items**。 如果磁片區在備份時沒有掛接點或磁碟機號，則此子命令會傳回以 GUID 為基礎的磁片區名稱，以供復原磁片區使用。
-   當 **-itemtype** 為 **應用程式**時，您可以使用 **ADIFM** 的值來執行從 **媒體進行安裝** 作業，以復原 Active Directory Domain Services 所需的所有相關資料。 **ADIFM** 會建立 Active Directory 資料庫、登錄和 SYSVOL 狀態的複本，然後將此資訊儲存在 **-recoveryTarget**所指定的位置。 只有在指定 **-recoveryTarget** 時，才使用此參數。

## <a name="examples"></a>範例

若要在2013年3月31日（上午9:00）執行備份復原，請在磁片區 d：中輸入：
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
若要從2013年3月31日（從9:00 年3月31日）開始復原至磁片磁碟機 d，請輸入：
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
若要從2013年3月31日（從年3月31日）9:00 開始復原備份，請在 d:\folder 的 d:\folder 和資料夾中，輸入：
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
若要在2013年3月31日（上午9:00 時）執行備份復原，請在 volume \\ \\ ？ \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963} 中 \, 輸入：
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
若要從2013年4月30日上午9:00 執行備份復原，請在 server01 的共用資料夾 servername\share 中， \\ \\ 輸入：
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)
- [Backup](wbadmin.md)
- [WBFileRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) Cmdlet
- [WBHyperVRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) Cmdlet
- [WBSystemStateRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) Cmdlet
- [WBVolumeRecovery](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) Cmdlet
