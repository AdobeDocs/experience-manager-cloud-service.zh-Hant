---
title: 計劃碼品質測試
description: 了解管道計劃碼品質測試如何運作及如何提高部署品質。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: d60659f443d130a195fd81cfe4773cd87df28264
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 100%

---

# 計劃碼品質測試 {#code-quality-testing}

了解管道計劃碼品質測試如何運作及如何提高部署品質。

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="計劃碼品質測試"
>abstract="計劃碼品質測試根據一組品質規則評估您的應用計劃計劃碼。這是計劃碼品質管道的主要目的，並在所有生產和非生產管道中的建構步驟之後立即執行。"

## 簡介 {#introduction}

計劃碼品質測試根據一組品質規則評估您的應用計劃計劃碼。這是計劃碼品質管道的主要目的，並在所有生產和非生產管道中的建構步驟之後立即執行。

參考文件[設定 CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)了解有關不同類型管道的更多資訊。

## 計劃碼品質規則 {#understanding-code-quality-rules}

計劃碼品質測試會掃描原始計劃碼以確保其符合特定的品質標準。這是透過 SonarQube 和使用 OakPAL 的內容包級別檢查的組合來實現的。有超過 100 條規則結合了通用 Java 規則和 AEM 特定規則。部分 AEM 特定規則是根據 AEM 工程團隊的最佳做法建立的，並被稱為[自訂計劃碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

>[!NOTE]
>
>若要下載完整的規則清單，可[使用此連結。](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### 三層級評等 {#three-tiered-gate}

計劃碼品質測試確定的問題被指派到三個類別之一。

* **嚴重** - 這些問題會導致管道立即失敗。

* **重要** - 這些問題會導致管道進入暫停狀態。部署管理員、專案管理員或企業所有者可以覆寫問題，這種情況下管道會繼續進行，或者他們也可以接受問題，這種情況下管道則會因失敗而停止。

* **資訊** - 這些問題純粹是為了參考目的而提供，對管道執行沒有影響。

>[!NOTE]
>
>在僅限計劃碼品質的管道中，不能覆寫計劃碼品質閘道中的重要失敗，因為計劃碼品質測試步驟是管道中的最後一步。

### 評等 {#ratings}

此步驟的結果交付為&#x200B;**評級**。

下表總結了各關鍵、重要和資訊類別的評級和故障閾值。

| 名稱 | 定義 | 類別 | 失敗臨界值 |
|--- |--- |--- |--- |
| 安全評等 | A = 無漏洞<br/>B = 至少 1 個輕微漏洞<br/>C = 至少 1 個重大漏洞<br/>D = 至少 1 個嚴重漏洞<br/>E = 至少 1 個阻斷式漏洞 | 嚴重 | &lt; B |
| 可靠度評等 | A = 無錯誤<br/>B = 至少 1 個輕微錯誤<br/>C = 至少 1 個重大錯誤<br/>D = 至少 1 個嚴重錯誤<br>E = 至少 1 個阻斷式錯誤 | 嚴重 | &lt; D |
| 可維護性評等 | 由計劃碼異味的待處理修復成本定義為已進入應用計劃的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 使用以下公式將單位測試行適用範圍和條件適用範圍混合後定義：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = 在執行單位測試時已經至少一次評估為 `true` 的條件</li><li>`CF` = 在執行單位測試時已經至少一次評估為 `false` 的條件</li><li>`LC` = 適用行數 = lines_to_cover - uncovered_lines</li><li>`B` = 條件總數</li><li>`EL` = 可執行行的總數 (lines_to_cover)</li></ul> | 重要 | &lt; 50% |
| 略過的單位測試 | 略過的單位測試總數 | 資訊 | > 1 |
| 未解決的問題 | 整體問題類型 - 漏洞、錯誤和計劃碼異味 | 資訊 | > 0 |
| 重複的行 | 定義為重複區塊中包含的行數。在以下條件下，會將計劃碼區塊視為重複。<br>非 Java 專案：<ul><li>應該至少有 100 個連續和重複的權杖。</li><li>這些權杖應至少分佈在： </li><li>COBOL 的 30 行計劃碼 </li><li>ABAP 的 20 行計劃碼 </li><li>其他語言的 10 行計劃碼</li></ul>Java 專案：<ul></li><li> 無論權杖和行的數量如何，應至少有 10 個連續和重複的陳述式。</li></ul>偵測重複時會忽略縮排和字串常值中的差異。 | 資訊 | > 1% |
| 雲端服務相容性 | 識別出的雲端服務相容性問題的數量 | 資訊 | > 0 |

>[!NOTE]
>
>如需更多詳細資訊，請參閱 [SonarQube 的量度定義](https://docs.sonarqube.org/latest/user-guide/metric-definitions/)。

>[!NOTE]
>
>若要了解由[!UICONTROL 雲端管理員]執行的自訂計劃碼品質規則的詳細資訊，請參閱文件：[自訂計劃碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 處理誤判 {#dealing-with-false-positives}

品質掃描流程並非完美無瑕，有時會錯誤地識別出實際上不構成問題的問題。這即稱為&#x200B;**誤判**。

在這些情況下，可以使用標準 Java `@SuppressWarnings` 註解來標註原始計劃碼，將規則 ID 指定為註解屬性。例如，一種常見的誤判是用於偵測硬式編碼密碼的 SonarQube 規則可能對如何識別硬式編碼密碼過於積極。

以下計劃碼在 AEM 專案中相當常見，其中包含連接到某些外部服務的計劃碼。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube 因此會提出阻斷式漏洞。但在查看計劃碼後，您會發現這並非漏洞，然後可以使用適當的規則 ID 標註計劃碼。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但如果計劃碼確實有此問題：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

則正確的解決方案是移除硬式編碼的密碼。

>[!NOTE]
>
>雖然最佳做法是使 `@SuppressWarnings` 註解盡可能具體 (即僅標註導致問題的特定陳述式或區塊)，但可以在分類層級進行註解。

>[!NOTE]
>雖然沒有明確的安全測試步驟，但在計劃碼品質步驟中評估了與安全相關的計劃碼品質規則。參考文件[AEM as a Cloud Service的安全總覽](/help/security/cloud-service-security-overview.md)了解有關雲端服務安全性的更多資訊。

## 掃描最佳化的內容套件 {#content-package-scanning-optimization}

在品質分析流程中，Cloud Manager 會對 Maven 組建產生的內容套件進行分析。Cloud Manager 可提供最佳化功能以加速此流程，若需遵守某些套件限制，前述功能即有助益。最顯著的是針對輸出單一內容套件的專案執行的最佳化，該套件通常稱為「全」套件，其中會包含由組建產生並標記為已略過的一些其他內容套件。當 Cloud Manager 偵測到這種情況時，會直接掃描個別內容套件並根據相依性進行排序，而不是將「全」套件解除封裝。例如，考慮以下組建輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (klipped-content-package)

如果 `myco-all-1.0.0-SNAPSHOT.zip` 內的項目只有兩個已略過的內容套件，則將掃描這兩個嵌入的套件而不是「全」內容套件。

對於產生數十個嵌入套件的專案，已證明這種最佳化將在每次管道執行節省 10 分鐘以上的時間。

當「全」內容套件包含已略過的內容套件和 OSGi 套裝的組合時，可能會出現一種特殊情況。例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 包含前面提到的兩個嵌入套件以及一個或多個 OSGi 套裝，則會建構出一個全新、最小的內容套件，且僅包含 OSGI 套裝。此套件一律名為 `cloudmanager-synthetic-jar-package`，而且會將所包含的套裝放在 `/apps/cloudmanager-synthetic-installer/install` 中。

>[!NOTE]
>
>* 此最佳化並不會影響部署到 AEM 的套件。
>* 由於嵌入的內容套件和已略過的內容套件之間的對應是根據檔案名稱，因此若有多個已略過的內容套件檔案名稱完全相同或嵌入時檔案名稱變更，即無法進行此最佳化。

