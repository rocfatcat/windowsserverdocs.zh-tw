---
title: 建立受防護主機的安全性群組，並向 HGS 註冊群組
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: efcf148356910a250a06ee9165c544c96226e10e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971415"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>建立受防護主機的安全性群組，並向 HGS 註冊群組

> 適用於：Windows Server (半年度管道)、Windows Server 2016

> [!IMPORTANT]
> 從 Windows Server 2019 開始，AD 模式已淘汰。 針對不可能進行 TPM 證明的環境，請設定[主機金鑰證明](guarded-fabric-initialize-hgs-key-mode.md)。 主機金鑰證明提供與 AD 模式類似的保證，而且設定起來較簡單。

本主題說明使用系統管理員信任的證明 (AD 模式) ，準備 Hyper-v 主機成為受防護主機的中繼步驟。 執行這些步驟之前，請先完成[針對將成為受防護主機的主機設定網狀架構 DNS](guarded-fabric-configuring-fabric-dns-ad.md)中的步驟。


## <a name="create-a-security-group-and-add-hosts"></a>建立安全性群組並新增主機

1. 在網狀架構網域中建立新的**全域**安全性群組，並新增將執行受防護 Vm 的 hyper-v 主機。 重新開機主機以更新其群組成員資格。

2. 使用 New-adgroup 來取得安全性群組 (SID) 的安全識別碼，並將其提供給 HGS 系統管理員。

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![具有輸出的 New-adgroup 命令](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>向 HGS 註冊安全性群組的 SID

1. 在 HGS 伺服器上，執行下列命令以向 HGS 註冊安全性群組。
   視需要重新執行命令以進行其他群組。
   為群組提供易記的名稱。
   不需要符合 Active Directory 安全性群組名稱。

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. 若要確認已新增群組，請執行[HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)。

## <a name="next-step"></a>後續步驟

> [!div class="nextstepaction"]
> [確認證明](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>其他參考資料

- [部署受防護主機和受防護 VM 的主機守護者服務](guarded-fabric-deploying-hgs-overview.md)
