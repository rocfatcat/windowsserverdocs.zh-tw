---
title: fsutil file
description: Fsutil file 命令的參考檔，它會依使用者名稱尋找檔案、查詢配置的檔案範圍、設定檔案的簡短名稱、設定檔案的有效資料長度、設定檔案的零資料，或建立新的檔案。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: 69ef36a03c22d7e14d4d657ce5ebab85b63afbd7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037376"
---
# <a name="fsutil-file"></a>fsutil file

> 適用于： Windows Server (半年通道) 、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

依使用者名稱尋找檔案 (如果已啟用磁片配額) 、查詢配置的檔案範圍、設定檔案的簡短名稱、設定檔案的有效資料長度、為檔案設定零資料，或建立新的檔案。

## <a name="syntax"></a>語法

```
fsutil file [createnew] <filename> <length>
fsutil file [findbysid] <username> <directory>
fsutil file [optimizemetadata] [/A] <filename>
fsutil file [queryallocranges] offset=<offset> length=<length> <filename>
fsutil file [queryextents] [/R] <filename> [<startingvcn> [<numvcns>]]
fsutil file [queryfileid] <filename>
fsutil file [queryfilenamebyid] <volume> <fileid>
fsutil file [queryoptimizemetadata] <filename>
fsutil file [queryvaliddata] [/R] [/D] <filename>
fsutil file [seteof] <filename> <length>
fsutil file [setshortname] <filename> <shortname>
fsutil file [setvaliddata] <filename> <datalength>
fsutil file [setzerodata] offset=<offset> length=<length> <filename>
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
| --------- | ----------- |
| createnew | 建立具有指定之名稱和大小的檔案，其內容由零組成。 |
| `<length>` | 指定檔案的有效資料長度。 |
| findbysid | 在啟用磁片配額的 NTFS 磁片區上，尋找屬於指定使用者的檔案。 |
| `<username>` | 指定使用者的使用者名稱或登入名稱。 |
| `<directory>` | 指定目錄的完整路徑，例如 C:\users。 |
| optimizemetadata | 這會對指定的檔案執行立即的中繼資料壓縮。 |
| /a | 分析優化之前和之後的檔案中繼資料。 |
| queryallocranges | 查詢 NTFS 磁片區上的檔案配置範圍。 適用于判斷檔案是否有稀疏區域。 |
| offset =`<offset>` | 指定應設為零的範圍起點。 |
| 長度 =`<length>` | 指定範圍 (的長度（以位元組為單位）) 。 |
| queryextents | 檔的查詢範圍。 |
| /r | 如果 <filename> 是重新分析點，請開啟它，而非其目標。 |
| `<startingvcn>` | 指定要查詢的第一個 VCN。 如果省略，請從 VCN 0 開始。 |
| `<numvcns>` | 要查詢的 VCNs 數目。 如果省略或0，則查詢到 EOF。 |
| queryfileid | 查詢 NTFS 磁片區上檔案的檔案識別碼。 |
| `<volume>` | 將磁片區指定為磁片磁碟機名稱，後面接著冒號。 |
| queryfilenamebyid | 顯示 NTFS 磁片區上所指定檔案識別碼的隨機連結名稱。 由於檔案可以有一個以上的連結名稱指向該檔案，因此不保證會提供哪個檔案連結作為檔案名的查詢結果。 |
| `<fileid>` | 指定 NTFS 磁片區上的檔案識別碼。 |
| queryoptimizemetadata | 查詢檔案的中繼資料狀態。 |
| queryvaliddata | 查詢檔案的有效資料長度。 |
| /d | 顯示詳細的有效資料資訊。 |
| seteof | 設定指定檔案的 EOF。 |
| setshortname | 針對 NTFS 磁片區上的檔案，將簡短名稱 (8.3 字元長度的檔案名) 。 |
| `<shortname>` | 指定檔案的簡短名稱。 |
| setvaliddata | 設定 NTFS 磁片區上檔案的有效資料長度。 |
| `<datalength>` | 指定檔案的長度（以位元組為單位）。 |
| setzerodata | 將檔案的 *位移* 和 *長度*) 指定的範圍 (設定為零，以清空檔案。 如果檔案是稀疏檔案，則會已取消認可基礎配置單位。 |

#### <a name="remarks"></a>備註

- 在 NTFS 中，檔案長度有兩個重要概念：檔案結尾 (EOF) 標記，以及有效的資料長度 (VDL) 。 EOF 表示檔案的實際長度。 VDL 會識別磁片上有效資料的長度。 VDL 和 EOF 之間的任何讀取都會自動傳回0，以保持 C2 物件重複使用需求。

- **Setvaliddata**參數僅供系統管理員使用，因為它需要執行磁片區維護工作 (SeManageVolumePrivilege) 許可權。 只有 advanced 多媒體和系統區域網路絡案例才需要這項功能。 **Setvaliddata**參數的正值必須大於目前的 VDL，但小於目前的檔案大小。

    它適用于在下列情況中設定 VDL 的程式：

    - 透過硬體通道將原始叢集直接寫入磁片。 這可讓程式通知檔案系統此範圍包含可傳回給使用者的有效資料。

    - 在效能問題時建立大型檔案。 這可避免在建立或擴充檔案時，以零填滿檔案所花的時間。

### <a name="examples"></a>範例

若要尋找磁片磁碟機 C 上 *scottb* 所擁有的檔案，請輸入：

```
fsutil file findbysid scottb c:\users
```

若要查詢 NTFS 磁片區上的檔案配置範圍，請輸入：

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt
```

若要優化檔案的中繼資料，請輸入：

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

若要查詢檔案的範圍，請輸入：

```
fsutil file queryextents C:\Temp\sample.txt
```

若要設定檔案的 EOF，請輸入：

```
fsutil file seteof C:\testfile.txt 1000
```

若要設定檔案的簡短名稱，請在磁片磁碟機 C 上 *longfilename.txt* *longfile.txt*，輸入：

```
fsutil file setshortname c:\longfilename.txt longfile.txt
```

若要針對 NTFS 磁片區上名為*testfile.txt*的檔案，將有效資料長度設為*4096 個位元組*，請輸入：

```
fsutil file setvaliddata c:\testfile.txt 4096
```

若要將 NTFS 磁片區上的檔案範圍設定為零，請輸入：

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt
```

## <a name="additional-references"></a>其他參考資料

- [命令列語法關鍵](command-line-syntax-key.md)

- [fsutil](fsutil.md)
