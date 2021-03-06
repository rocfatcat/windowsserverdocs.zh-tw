---
title: 新增 TPM 信任證明的主機資訊
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 06/21/2019
ms.openlocfilehash: fc879fda0f6a708a8a1d4ebd60834f4e6543f3ba
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997168"
---
# <a name="add-host-information-for-tpm-trusted-attestation"></a>新增 TPM 信任證明的主機資訊

> 適用于： Windows Server 2019、Windows Server (半年通道) 、Windows Server 2016

針對 TPM 模式，網狀架構系統管理員會捕獲三種主機資訊，每個都必須新增至 HGS 設定：

- 每個 Hyper-v 主機 (EKpub) 的 TPM 識別碼
- 程式碼完整性原則，這是 Hyper-v 主機允許之二進位檔的白名單
- TPM 基準 (開機測量) ，代表在相同硬體類別上執行的一組 Hyper-v 主機

在網狀架構系統管理員捕捉到資訊之後，請將它新增至 HGS 設定，如下列程式所述。

1. 取得包含 EKpub 資訊的 XML 檔案，並將其複製到 HGS 伺服器。 每一部主機會有一個 XML 檔案。 然後，在 HGS 伺服器上提高許可權的 Windows PowerShell 主控台中，執行下列命令。 針對每個 XML 檔案重複此命令。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 如果您在新增與不受信任的簽署金鑰憑證有關的 TPM 識別碼時遇到錯誤 (EKCert) ，請確定已將[受信任的 TPM 根憑證新增](guarded-fabric-install-trusted-tpm-root-certificates.md)至 HGS 節點。
    > 此外，某些 TPM 廠商不會使用 EKCerts。
    > 您可以在 [記事本] 之類的編輯器中開啟 XML 檔案，並檢查是否有指出找不到 EKCert 的錯誤訊息，以檢查是否遺漏 EKCert。
    > 如果是這種情況，而且您信任電腦中的 TPM 是真實的，您可以使用旗標 `-Force` 來覆寫此安全性檢查，並將主機識別碼新增至 HGS。

2. 取得網狀架構系統管理員為主機建立的程式碼完整性原則，以二進位格式 (\* . p7b) 。 將它複製到 HGS 伺服器。 然後執行下列命令。

    針對 `<PolicyName>` ，指定 CI 原則的名稱，以描述其適用的主機類型。 最佳做法是在您的機器的製作/型號和其上執行的任何特殊軟體設定之後，將它命名為。<br>針對 `<Path>` ，指定程式碼完整性原則的路徑和檔案名。

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

    > [!NOTE]
    > 如果您使用的是已簽署的程式碼完整性原則，請向 HGS 註冊相同原則的不帶正負號複本。
    > 程式碼完整性原則的簽章可用來控制原則的更新，但不會測量到主機 TPM，因此 HGS 無法將其證明至。

3. 取得網狀架構系統管理員從參照主機所捕獲的 TCG 記錄檔。 將檔案複製到 HGS 伺服器。 然後執行下列命令。 一般來說，您會將原則命名為它所代表的硬體類別， (例如「製造商型號修訂」 ) 。

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

這會完成為 TPM 模式設定 HGS 叢集的程式。 網狀架構系統管理員可能會要求您從 HGS 提供兩個 Url，然後才能完成主機的設定。 若要取得這些 Url，請在 HGS 伺服器上執行[HgsServer](/powershell/module/hgsserver/get-hgsserver?view=win10-ps)。

## <a name="next-step"></a>後續步驟

> [確認證明](guarded-fabric-confirm-hosts-can-attest-successfully.md)