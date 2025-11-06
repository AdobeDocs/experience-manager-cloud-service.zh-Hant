---
title: 程式碼品質測試
description: 了解管道程式碼品質測試如何運作及如何提高部署品質。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 80%

---

# 程式碼品質測試 {#code-quality-testing}

了解管道程式碼品質測試如何運作及如何提高部署品質。

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="程式碼品質測試"
>abstract="程式碼品質測試根據一組品質規則評估您的應用計劃程式碼。這是程式碼品質管道的主要目的，並在所有生產和非生產管道中的建構步驟之後立即執行。"

## 簡介 {#introduction}

程式碼品質測試根據一組品質規則評估您的應用計劃程式碼。這是程式碼品質管道的主要目的，並在所有生產和非生產管道中的建構步驟之後立即執行。

請參閱[設定 CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)，深入了解不同類型管道。

## 程式碼品質規則 {#understanding-code-quality-rules}

程式碼品質測試會掃描原始程式碼以確保其符合特定的品質標準。SonarQube和使用OakPAL的內容套件層級檢查的組合會實作此步驟。 有超過100條規則結合了通用Java規則和AEM特定規則。 部分AEM特定規則是根據AEM工程團隊的最佳做法，稱為[自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

你可以[使用此連結](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)下載目前完整的規則清單。

>[!IMPORTANT]
>
>從 2025 年 2 月 13 日 (星期四) (Cloud Manager 2025.2.0) 開始，Cloud Manager 程式碼品質將使用更新後的 SonarQube 9.9 版本和更新後的規則清單 (可[在此處下載](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS-2024-12-0.xlsx))。

### 三層級評等 {#three-tiered-gate}

程式碼品質測試確定的問題被指派到三個類別之一。

* **嚴重** - 會導致管道立即失敗的問題。

* **重要** - 會導致管道進入暫停狀態的問題。部署管理員、專案管理員或企業所有者可以覆寫此問題，讓管道繼續。 或者，他們可以接受這些問題，導致管道因失敗而停止。

* **資訊** — 純粹為了參考目的而提供，對管道執行沒有影響的問題

>[!NOTE]
>
>在僅限程式碼品質的管道中，不能覆寫程式碼品質閘道中的重要失敗，因為程式碼品質測試步驟是管道中的最後一步。

### 評等 {#ratings}

此步驟的結果以&#x200B;**評等**&#x200B;傳遞。

下表總結了各關鍵、重要和資訊類別的評級和故障閾值。

| 名稱 | 定義 | 類別 | 失敗臨界值 |
|--- |--- |--- |--- |
| 安全評等 | A = 無漏洞<br/>B = 至少 1 個輕微漏洞<br/>C = 至少 1 個重大漏洞<br/>D = 至少 1 個嚴重漏洞<br/>E = 至少 1 個阻斷式漏洞 | 嚴重 | &lt; B |
| 可靠度評等 | A = 無錯誤<br/>B = 至少 1 個輕微錯誤<br/>C = 至少 1 個重大錯誤<br/>D = 至少 1 個嚴重錯誤<br>E = 至少 1 個阻斷式錯誤 | 嚴重 | &lt; D |
| 可維護性評等 | 由程式碼異味的待處理修復成本定義為已進入應用計劃的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 使用以下公式將單位測試行適用範圍和條件適用範圍混合後定義：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = 在執行單位測試時已經至少一次評估為 `true` 的條件</li><li>`CF` = 在執行單位測試時已經至少一次評估為 `false` 的條件</li><li>`LC` = 適用行數 = lines_to_cover - uncovered_lines</li><li>`B` = 條件總數</li><li>`EL` = 可執行行的總數 (lines_to_cover)</li></ul> | 重要 | &lt; 50% |
| 略過的單位測試 | 略過的單位測試總數 | 資訊 | > 1 |
| 未解決的問題 | 整體問題類型 - 漏洞、錯誤和程式碼異味 | 資訊 | > 0 |
| 重複的行 | 定義為重複區塊中包含的行數。在以下條件下，會將程式碼區塊視為重複。<br>非 Java 專案：<ul><li>應該至少有 100 個連續和重複的權杖。</li><li>這些權杖應至少分佈在： </li><li>COBOL 的 30 行程式碼 </li><li>ABAP 的 20 行程式碼 </li><li>其他語言的 10 行程式碼</li></ul>Java 專案：<ul></li><li> 無論權杖和行的數量如何，應至少有 10 個連續和重複的陳述式。</li></ul>偵測重複時會忽略縮排和字串常值中的差異。 | 資訊 | > 1% |
| 雲端服務相容性 | 識別出的雲端服務相容性問題的數量 | 資訊 | > 0 |

>[!NOTE]
>
>如需更詳細的定義，請參閱 [SonarQube 的量度定義](https://docs.sonarsource.com/sonarqube-server/latest/user-guide/code-metrics/metrics-definition/)。

>[!NOTE]
>
>若要深入了解 [!UICONTROL Cloud Manager] 執行的自訂程式碼品質規則，請參閱[自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 處理誤判 {#dealing-with-false-positives}

品質掃描流程並非完美無瑕，有時會錯誤地識別出實際上不是問題的問題。 此狀態稱為&#x200B;**誤判**。

在這些情況下，可以使用標準 Java `@SuppressWarnings` 註解來標註原始程式碼，將規則 ID 指定為註解屬性。例如，一種常見的誤判是用於偵測硬式編碼密碼的 SonarQube 規則可能對如何識別硬式編碼密碼過於積極。

以下程式碼在 AEM 專案中相當常見，其中包含連接到某些外部服務的程式碼。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube提出阻斷式漏洞。 但在查看程式碼後，您會發現這個問題並非漏洞，然後可以使用適當的規則 ID 標註程式碼。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但如果程式碼實際上如下：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

則正確的解決方案是移除硬式編碼的密碼。

>[!NOTE]
>
>雖然最佳做法是使`@SuppressWarnings`註解儘可能具體 — 例如僅標註導致問題的陳述式或區塊 — 但也可以在類別層級進行註解。

>[!NOTE]
>雖然沒有明確的安全測試步驟，但在程式碼品質步驟中評估了與安全相關的程式碼品質規則。請參閱 [AEM as a Cloud Service 安全性概觀](/help/security/cloud-service-security-overview.md)，深入了解雲端服務的安全性。

## 掃描最佳化的內容套件 {#content-package-scanning-optimization}

在品質分析流程中，Cloud Manager 會對 Maven 組建產生的內容套件進行分析。Cloud Manager提供最佳化功能，可加速此流程，若需遵守某些套件限制，前述功能即有助益。 最顯著的最佳化目標為產生單一「全」套件的專案，其中包含組建中的多個內容套件，這些套件標示為已略過。 當 Cloud Manager 偵測到這種情況時，會直接掃描個別內容套件並根據相依性進行排序，而不是將「全」套件解除封裝。例如，考慮以下組建輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

如果 `myco-all-1.0.0-SNAPSHOT.zip` 內的項目只有兩個已略過的內容套件，則掃描這兩個嵌入的套件而不是「所有」內容套件。

對於產生數十個嵌入套件的專案，已證明這種最佳化將在每次管道執行節省 10 分鐘以上的時間。

當「全」內容套件包含已略過的內容套件和 OSGi 套裝的組合時，可能會出現一種特殊情況。例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 包含前面提到的兩個嵌入套件以及一個或多個 OSGi 套裝，則會建構出一個全新、最小的內容套件，且僅包含 OSGI 套裝。此套件一律名為 `cloudmanager-synthetic-jar-package`，而且會將所包含的套裝放在 `/apps/cloudmanager-synthetic-installer/install` 中。

>[!NOTE]
>
>* 此最佳化並不會影響部署到 AEM 的套件。
>* 內嵌內容套件和略過的內容套件之間的比對取決於檔案名稱。 如果多個略過的套件共用相同的檔案名稱，或檔案名稱在嵌入期間有所變更，則無法進行此最佳化。
