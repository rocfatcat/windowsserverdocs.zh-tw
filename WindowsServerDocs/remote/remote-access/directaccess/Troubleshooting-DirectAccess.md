---
title: 對 DirectAccess 進行疑難排解
description: 本主題提供針對 Windows Server 2016 中的 DirectAccess 部署進行疑難排解的相關資訊。
manager: brianlic
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 265924bb8993f8dd71c9509be4eacb38501d8180
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951259"
---
# <a name="troubleshooting-directaccess"></a>對 DirectAccess 進行疑難排解

>適用於：Windows Server (半年度管道)、Windows Server 2016

請遵循下列步驟，針對 (DirectAccess) 問題的遠端存取進行疑難排解。

|**問題**|**解決方案**|
|--|--|
|遠端存取管理主控台無法顯示 DirectAccess 設定|**還原遺失的設定資訊**<br />-如果您要針對多網站部署進行疑難排解，請確定最接近進入點的網域控制站可供使用。<br />-使用**DAEntrypointDC** Cmdlet 來抓取最接近進入點的網域控制站名稱。 如果網域控制站未執行，請使用**DAEntryPointDC** Cmdlet 指向另一個網域控制站。<br />-從伺服器上提高許可權的命令提示字元執行**gpresult** ，以確保伺服器會取得 DirectAccess 群組原則物件。<br />-啟用使用者介面 (UI) 記錄。<br />-使用下列命令來啟動 Windows PowerShell 記錄：<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>-關閉並重新開啟使用者介面。<br />-停用 Windows Powershell 記錄。 收集事件追蹤記錄檔。 此外，請收集 **% windir%/tracing**資料夾中的所有記錄檔。|
|套用 DirectAccess 設定失敗|**重新整理 DirectAccess 設定**<br />-如果您要針對多網站部署進行疑難排解，請確定最接近進入點的網域控制站可供使用。<br />-使用**DAEntrypointDC** Cmdlet 來抓取最接近進入點的網域控制站名稱。 如果網域控制站未執行，請使用**DAEntryPointDC** Cmdlet 指向另一個網域控制站。<br />-使用下列命令來啟動 Windows Powershell 記錄：<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />-按一下 **[** 套用]。<br />-失敗發生之後，請停用 Windows Powershell 記錄，並收集事件追蹤記錄檔。|
|DirectAccess 已設定，但用戶端無法連接到內部資源|**針對用戶端連接問題進行疑難排解**<br />-按一下 [遠端存取管理] 主控台中的 [**操作狀態**] 索引標籤，並確定所有元件都顯示綠色圖示。 如果沒有，請查看錯誤詳細資料，並遵循解決步驟。<br />- (BPA) 執行「遠端存取服務器」最佳做法分析程式。 如果有任何警告或錯誤，請遵循解決步驟來解決問題。|
|遇到與多網站設定相關的問題 (例如，啟用多網站、新增進入點，或設定進入點的網域控制站) |依照針對多網站[部署進行疑難排解](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj554657(v=ws.11))中的步驟進行。|
|[儀表板] 上的 [設定狀態] 磚顯示警告或錯誤|請依照[監視遠端存取服務器的設定發佈狀態](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574221(v=ws.11))中的步驟進行。|
|發生與設定負載平衡 (相關的問題（例如，當您啟用負載平衡時，設定會失敗），或當您在叢集中新增或移除伺服器時，發生問題) |如果您已啟用負載平衡或新增**節點，而當您按一下 [** 套用] 時重新整理了設定，但在伺服器上未正確形成叢集，請執行下列命令： **cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/v DebugFlag/t REG_DWORD/d" "0xffffffff" "** "，以收集新伺服器上的使用者介面記錄檔。|
|作業狀態會在下列步驟中顯示錯誤或警告，以更正情況|如果作業狀態顯示不正確的資訊 (例如錯誤，即使在您修正之後) ：<p>-啟用登錄機碼**cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/V EnableTracing/t REG_DWORD/d" "5" "**"。<br />-重新整理作業狀態，並收集 **% windir%/tracing**的記錄檔。|
|Windows 8 和更新版本的 DirectAccess 用戶端電腦會將「沒有網際網路」報告為 DirectAccess 連線的狀態，而網路連線狀態指示器 (NCSI) 報告連線能力有限。|當 DirectAccess 設定中已啟用強制通道時，就會發生這種情況，因此，只會使用 IPHTTPS。 若要解決此問題，您可以建立及設定 proxy 伺服器。 然後 NCSI 會使用 proxy 伺服器來執行網際網路連線能力檢查。 建議您使用下列程式，將靜態 proxy 新增至名稱解析原則資料表 (NRPT) 。<p>執行此程式中的命令之前，請確定將所有功能變數名稱、電腦名稱稱和其他 Windows PowerShell 命令變數取代為適用于您部署的值。<p>**為 NRPT 規則設定靜態 proxy**<br />1. 顯示 "."NRPT 規則：`Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2. 記下 "." (GUID) 的名稱NRPT 規則。  (GUID) 的名稱應該以**DA-{...}** 開頭<br />3. 設定 "." 的 proxy要**proxy.corp.example.com:8080**的 NRPT 規則：`Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4. 顯示 "."執行以再次執行 NRPT 規則 `Get-DnsClientNrptRule` ，並確認已正確設定**ProxyFQDN： port** 。<br />5. 在 `gpupdate /force` 內部連線用戶端時，在 DirectAccess 用戶端上執行來重新整理群組原則，然後使用顯示 NRPT， `Get-DnsClientNrptPolicy` 並確認 "." 規則顯示**ProxyFQDN： port**。|
