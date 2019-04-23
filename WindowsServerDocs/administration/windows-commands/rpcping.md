---
title: rpcping
description: '適用於 Windows 命令主題 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfa1d08c81f8b26507a5cae5f688923a7b226e1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829989"
---
# <a name="rpcping"></a>rpcping

>適用於：Windows Server （半年通道），Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

確認執行 Microsoft Exchange Server 和任何支援的 Microsoft Exchange 用戶端工作站網路上的電腦之間的 RPC 連線。 此公用程式可用來檢查服務的 Microsoft Exchange 伺服器是否有回應 RPC 要求從用戶端工作站，透過網路使用。 

## <a name="syntax"></a>語法
```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,Majorver]] [/O <Interface Object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>參數

|參數|描述|
|-------|--------|
|/t \<protseq>|指定要使用的通訊協定順序。 可以是其中一個標準的 RPC 通訊協定順序，例如： ncacn_ip_tcp，連線，或 ncacn_http。<br /><br />如果未指定，預設值為 ncacn_ip_tcp。|
|/s \<server_addr>|指定伺服器位址。 如果未指定，本機電腦將會進行 ping。|
|/e \<endpoint>|指定要 ping 的端點。 如果未指定，將會進行 ping 目標電腦上的結束點對應程式。<br /><br />此選項是互斥的介面 (**/f**) 選項。|
|/o \<binding_options>|指定 RPC ping 的繫結選項。|
|/f\<介面 UUID > [，Majorver]|指定要 ping 的介面。 這個選項會與端點選項互斥。 介面會指定為一個 UUID。<br /><br />如果*Majorver*未指定，將會搜尋第 1 版的介面。<br /><br />指定介面時， **rpcping**會查詢端點對應程式在目標電腦上，若要擷取的指定介面的端點。 端點對應程式會使用命令列中指定的選項來查詢。|
|/O\<物件 UUID >|如果介面註冊其中一個，請指定物件的 UUID。|
|/i \<#_iterations>|指定要呼叫的數目。 預設值為 1。 此選項可用於測量連線延遲時間，如果指定了多個反覆項目。|
|/u \<security_package_id>|指定安全性套件 （安全性提供者） 會使用 RPC 進行呼叫。 安全性封裝被視為數字或名稱。 如果使用的數字，它是相同的數字，如同 RpcBindingSetAuthInfoEx API。 下列清單顯示的名稱和號碼。 名稱不區分大小寫：<br /><br />-Negotiate / 9 或一個的 nego，snego 或交涉<br />-NTLM / 10 或 ntlm 驗證<br />-SChannel / 14 或安全通道<br />Kerberos / 16 或 Kerberos<br />核心 / 20 或核心<br />    如果您指定這個選項時，您必須指定 [無] 以外的驗證層級。 沒有預設值，這個選項。 如果未指定，RPC 會不會用於 ping 的安全性。|
|/a \<authn_level>|指定要使用的驗證等級。 可能值為：<br /><br />-連線<br />-呼叫<br />-   pkt<br />-完整性<br />-隱私權<br /><br />如果指定此選項，安全性套件識別碼 (/ u) 也必須指定。 沒有預設值，這個選項。<br /><br />如果未指定此選項，RPC 會不會用於 ping 的安全性。|
|/N \<server_princ_name>|指定的伺服器主體名稱。<br /><br />只使用此欄位中選取的驗證層級和安全性封裝時。|
|/I \<auth_identity>|可讓您指定要連接到伺服器的替代身分識別。 識別是在表單的使用者、 網域、 密碼。 如果使用者名稱、 網域或密碼可由殼層解譯的特殊字元，請使用雙引號括住身分識別。 您可以指定**\*** 而不是密碼和 RPC 會提示您輸入的密碼，而不需要回應在螢幕上。 如果未指定此欄位，則將使用的登入的使用者身分識別。<br /><br />只使用此欄位中選取的驗證層級和安全性封裝時。|
|/C \<capabilities>|指定的十六進位旗標的位元遮罩。 只使用此欄位中選取的驗證層級和安全性封裝時。|
|/T \<identity_tracking>|指定靜態或動態。 如果沒有指定，動態是預設值。<br /><br />只使用此欄位中選取的驗證層級和安全性封裝時。|
|/M \<impersonation_type>|指定匿名、 識別、 模擬或委派。 預設值是模擬。<br /><br />只使用此欄位中選取的驗證層級和安全性封裝時。|
|/S \<server_sid>|指定預期的伺服器的 SID。<br /><br />只使用此欄位中選取的驗證層級和安全性封裝時。|
|/P \<proxy_auth_identity>|指定要使用 RPC/HTTP proxy 進行驗證的身分識別。 具有相同的格式與 /I 選項。 您必須指定安全性套件 (/ u)，驗證層級 （/），並驗證配置 (/ 小時) 才能使用此選項。|
|/F \<RPCHTTP_flags>|指定要針對 RPC/HTTP 前端驗證傳入的旗標。 旗標可能會指定數字或目前已辨識的旗標的名稱為：<br /><br />-使用 SSL / 1 或 ssl 或 use_ssl<br />使用第一個驗證配置 / 2 或第一個或 use_first<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/H \<RPC/HTTP_authn_schemes>|指定要用於 RPC/HTTP 前端驗證的驗證配置。 此選項會是數值或名稱的逗號分隔的清單。 範例：基本、 NTLM。 認得的值為 （名稱不區分大小寫）：<br /><br />-基本 / 1 或基本<br />-NTLM / 2 或 ntlm 驗證<br />-憑證 / 65536 或憑證<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/B \<server_certificate_subject>|指定伺服器的憑證主旨。 您必須使用 SSL，此選項才能運作。<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/b|擷取伺服器憑證主體從伺服器所傳送的憑證，並將它列印至螢幕或記錄檔。 只有在 Proxy 回應只選項時才有效 (/ E) 和使用 SSL 選項所指定。<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/R|指定 HTTP proxy。 如果*無*，使用 RPC proxy。 該值*預設*表示使用 IE 設定中用戶端電腦。 任何其他值會視為明確 HTTP proxy。 如果您未指定此旗標，會假設預設值，也就是檢查 IE 設定。 這個旗標是時才有效 **/E** （只回應） 旗標已啟用。|
|/E|將 ping 限制只有 RPC/HTTP proxy。 Ping 就不會到達伺服器。 嘗試建立 RPC/HTTP proxy 是否可連線時很有用。 若要指定 HTTP proxy，請使用 [/R] 旗標。 如果 /o 旗標指定 HTTP proxy，則會忽略這個選項。<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/q|指定無訊息模式。 不會發出任何要求，但不包括密碼的提示。 假設*Y*回應所有的查詢。 小心使用此選項。|
|/c|使用智慧卡憑證。 rpcping 會提示使用者選擇智慧卡。|
|/A|指定用來驗證的 HTTP proxy 身分識別。 具有相同的格式與 /I 選項。<br /><br />您必須指定驗證配置 (/ U)、 安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/U|指定要用於 HTTP proxy 驗證的驗證配置。 此選項會是數值或名稱的逗號分隔的清單。 範例：基本、 NTLM。 認得的值為 （名稱不區分大小寫）：<br /><br />-基本 / 1 或基本<br />-NTLM / 2 或 ntlm 驗證<br /><br />您必須指定安全性套件 (/ u) 和驗證等級 （/） 才能使用此選項。|
|/r|如果指定了多個反覆項目，此選項可讓**rpcping**目前的執行統計資料會定期改為顯示在最後一次呼叫之後。 指定報告間隔以秒為單位。 預設值為 15。|
|/v|會告訴**rpcping**以讓輸出詳細程度。 預設值為 1。 2 和 3 提供詳細輸出**rpcping**。|
|/d|啟動 RPC 網路診斷的 UI。|
|/p|指定為提示認證，如果驗證失敗。|
|/?|在命令提示字元顯示說明。|

## <a name="BKMK_Examples"></a>範例
若要尋找您的 Exchange server，您透過 RPC/HTTP 連接是否可存取，請輸入：
```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P "username,domain,*" /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>其他參考資料
-   [命令列語法關鍵](command-line-syntax-key.md)