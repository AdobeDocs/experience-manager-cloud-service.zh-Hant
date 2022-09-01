---
title: 程式碼品質測試
description: 了解管道的程式碼品質測試如何運作，以及如何改善部署的品質。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: d60659f443d130a195fd81cfe4773cd87df28264
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 1%

---

# 程式碼品質測試 {#code-quality-testing}

了解管道的程式碼品質測試如何運作，以及如何改善部署的品質。

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="程式碼品質測試"
>abstract="程式碼品質測試會根據一組品質規則來評估您的應用程式程式碼。 這是僅限程式碼品質管道的主要用途，會在所有生產及非生產管道的建立步驟後立即執行。"

## 簡介 {#introduction}

程式碼品質測試會根據一組品質規則來評估您的應用程式程式碼。 這是僅限程式碼品質管道的主要用途，會在所有生產及非生產管道的建立步驟後立即執行。

請參閱檔案 [設定CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 以進一步了解不同類型的管道。

## 程式碼品質規則 {#understanding-code-quality-rules}

代碼質量測試掃描原始碼，以確保它滿足某些質量標準。 這是透過SonarQube與內容封裝層級檢查的組合，使用OakPAL來實作。 有100多個規則，結合一般Java規則和AEM專用規則。 部分AEM專用規則是根據AEM Engineering的最佳實務建立，並稱為 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>
>您可以下載完整的規則清單 [連結。](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### 三級評級 {#three-tiered-gate}

由程式碼品質測試所識別的問題會指派給三個類別中的一個。

* **關鍵**  — 這些問題是導致管道立即失效的問題。

* **重要**  — 這些問題會導致管道進入暫停狀態。 部署經理、項目經理或業務負責人可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道會因故障而停止。

* **資訊**  — 這些問題僅僅供參考，對管道執行沒有影響

>[!NOTE]
>
>在僅限程式碼品質的管道中，無法覆寫程式碼品質閘道中的重要失敗，因為程式碼品質測試步驟是管道中的最後一步。

### 評等 {#ratings}

此步驟的結果以 **評等**.

下表概括了每個關鍵、重要和資訊類別的評級和故障閾值。

| 名稱 | 定義 | 類別 | 失敗閾值 |
|--- |--- |--- |--- |
| 安全性評等 | A =沒有漏洞 <br/>B =至少1個小漏洞<br/> C =至少1個重大漏洞 <br/>D =至少1個嚴重漏洞 <br/>E =至少1個阻止程式漏洞 | 關鍵 | &lt; B |
| 可靠性等級 | A =沒有錯誤 <br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤<br>E =至少1個封鎖程式錯誤 | 關鍵 | &lt; D |
| 維修性等級 | 由代碼的未清補救成本定義，其氣味是已進入應用程式的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 由混合使用公式的單位測試線覆蓋和條件覆蓋定義： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` =已評估為 `true` 運行單元測試時至少一次</li><li>`CF` =已評估為 `false` 運行單元測試時至少一次</li><li>`LC` =覆蓋行= linestocover - uncoveredlines</li><li>`B` =條件總數</li><li>`EL` =可執行行的總數(lines_to_cover)</li></ul> | 重要 | &lt; 50% |
| 已跳過的單元測試 | 已跳過的單元測試數 | 資訊 | > 1 |
| 未結問題 | 整體問題類型 — 弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 重複行 | 定義為重複塊中涉及的行數。 在下列條件下，會將程式碼區塊視為重複。<br>非Java專案：<ul><li>至少應有100個連續和重複的代號。</li><li>這些代號應至少分佈於： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行代碼以供其他語言使用</li></ul>Java項目：<ul></li><li> 無論代號和行數多寡，至少應有10個連續且重複的陳述式。</li></ul>偵測重複項目時，縮排和字串文字的差異會被忽略。 | 資訊 | > 1% |
| Cloud Service相容性 | 已識別的雲端服務相容性問題數 | 資訊 | > 0 |

>[!NOTE]
>
>請參閱 [SonarQube的度量定義](https://docs.sonarqube.org/latest/user-guide/metric-definitions/) 以取得更詳細的定義。

>[!NOTE]
>
>若要進一步了解由執行的自訂程式碼品質規則 [!UICONTROL Cloud Manager]，請參閱檔案 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## 處理誤判 {#dealing-with-false-positives}

質量掃描過程不完美，有時會錯誤地識別實際上沒有問題的問題。 這稱為 **偽陽性**.

在這些情況下，可以使用標準Java對原始碼進行注釋 `@SuppressWarnings` 將規則ID指定為注釋屬性的注釋。 例如，一個常見的誤判是，用於檢測硬式編碼密碼的SonarQube規則對於硬式編碼密碼的識別方式可能具有攻擊性。

下列程式碼在AEM專案中相當常見，其程式碼可連線至某些外部服務。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後會引發一個阻斷程式漏洞。 但在檢閱程式碼後，您會發現這並非漏洞，並可以使用適當的規則ID在程式碼上加上註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

不過，如果程式碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那麼正確的解決方案就是刪除硬式編碼的密碼。

>[!NOTE]
>
>雖然最佳實務是讓 `@SuppressWarnings` 注釋盡可能具體，即僅注釋導致問題的特定語句或塊，可以在類級別進行注釋。

>[!NOTE]
>雖然沒有明確的安全性測試步驟，但在代碼品質步驟期間仍會評估與安全性相關的代碼品質規則。 請參閱檔案 [AEM安全性概述as a Cloud Service](/help/security/cloud-service-security-overview.md) 深入了解Cloud Service的安全性。

## 內容套件掃描最佳化 {#content-package-scanning-optimization}

在品質分析程式中，Cloud Manager會對Maven組建版本產生的內容套件執行分析。 Cloud Manager提供最佳化措施來加速此程式，當發現某些封裝限制時，這些措施就十分有效。 最重要的是針對輸出單一內容套件的專案所執行的最佳化，通常稱為「全部」套件，其中包含由組建產生的許多其他內容套件，並標示為已略過。 當Cloud Manager偵測到此情況時，系統會直接掃描個別內容套件，並根據相依性排序，而非解壓縮「所有」套件。 例如，請考量下列組建輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (klipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (klipped-content-package)

如果內部只有 `myco-all-1.0.0-SNAPSHOT.zip` 是兩個已略過的內容套件，則會掃描兩個內嵌套件，而不是「全部」內容套件。

對於產生數十個內嵌套件的專案，此最佳化顯示為每個管道執行節省10分鐘以上。

「all」內容套件包含已略過內容套件和OSGi套件組合時，可能會發生特殊情況。 例如，若 `myco-all-1.0.0-SNAPSHOT.zip` 包含先前提到的兩個嵌入式包以及一個或多個OSGi包，然後只使用OSGi包構建新的最小內容包。 此包始終命名 `cloudmanager-synthetic-jar-package` 並且包裝在 `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* 此最佳化不會影響部署至AEM的套件。
>* 由於嵌入式內容包和跳過的內容包之間的匹配基於檔案名，因此如果多個跳過的內容包具有相同的檔案名或在嵌入時更改了檔案名，則無法執行此優化。

