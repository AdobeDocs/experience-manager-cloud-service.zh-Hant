---
title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
translation-type: tm+mt
source-git-commit: 49bb443019edc6bdec22e24b8a8c7733abe54e35
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# 記錄 {#logging}

AEM即雲端服務是客戶可加入自訂程式碼的平台，可為客戶群建立獨特的體驗。 有鑑於此，記錄是本端開發和雲端環境（尤其是雲端服務的Dev環境）上除錯和瞭解程式碼執行的重要功能。

AEM記錄和記錄檔層級會在設定檔中管理，這些設定檔會以Git儲存為AEM專案的一部分，並透過Cloud Manager部署為AEM專案的一部分。 以雲端服務身分登入AEM可分為兩個邏輯集：

* AEM記錄，在AEM應用程式層級執行記錄
* Apache HTTPD Web Server/Dispatcher日誌記錄，它在發佈層執行Web伺服器和Dispatcher的日誌記錄。

## AEM記錄 {#aem-loggin}

在AEM應用程式層級登入，由三個記錄檔處理：

1. AEM Java記錄檔，可為AEM應用程式轉譯Java記錄陳述式。
1. HTTP請求記錄檔，此記錄檔記錄有關HTTP請求及其由AEM提供之回應的資訊
1. HTTP存取記錄檔，記錄AEM所提供的摘要資訊和HTTP要求

請注意，從發佈層的Dispatcher快取或上游CDN所提供的HTTP請求不會反映在這些記錄檔中。

### AEM Java記錄 {#aem-java-logging}

AEM as a Cloud Service&#39;s提供Java記錄陳述式的存取權。 AEM應用程式開發人員應遵循一般Java記錄最佳實務，在下列記錄層級記錄有關執行自訂程式碼的相關陳述式：

<table>
<tr>
<td>
<b>AEM環境</b></td>
<td>
<b>記錄層級</b></td>
<td>
<b>說明</b></td>
<td>
<b>日誌語句可用性</b></td>
</tr>
<tr>
<td>
開發</td>
<td>
除錯</td>
<td>
說明應用程式中的情況。<br>

當DEBUG記錄處於活動狀態時，會記錄提供活動發生情況的清楚說明以及影響處理的任何關鍵參數的語句。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
</ul></td>
</tr>
<tr>
<td>
分段</td>
<td>
警告</td>
<td>
說明可能成為錯誤的條件。<br>
當WARN日誌記錄處於活動狀態時，只記錄指示接近子最優性的條件語句。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
<li>分段</li>
</ul></td>
</tr>
<tr>
<td>
生產</td>
<td>
錯誤</td>
<td>
說明指出失敗且需要解決的條件。<br>
當ERROR日誌記錄處於活動狀態時，僅記錄指示失敗的語句。 ERROR log語句表示應盡快解決的嚴重問題。</td>
<td>
<ul>
<li> 地方開發</li>
<li>開發</li>
<li>分段</li>
<li>生產</li>
</ul></td>
</tr>
</table>