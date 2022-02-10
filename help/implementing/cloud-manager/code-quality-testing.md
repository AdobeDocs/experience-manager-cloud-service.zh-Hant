---
title: 代碼質量測試
description: Learn how code quality testing of pipelines works and how it can improve the quality of your deployments.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: ca3c1f255b8441a8d376a55a5353d58848384b8b
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 1%

---

# 代碼質量測試 {#code-quality-testing}

瞭解管道的代碼質量測試如何工作以及它如何提高部署質量。

>[!CONTEXTUALHELP]
>
>
## 簡介 {#introduction}

Code quality testing evaluates your application code based on a set of quality rules. 它是僅代碼質量管道的主要目的，並且在所有生產和非生產管道的構建步驟後立即執行。

Refer to the document [Configuring Your CI-CD Pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) to learn more about different types of pipelines.

## Code Quality Rules {#understanding-code-quality-rules}

Code quality testing scans the source code to ensure that it meets certain quality criteria. 這是通過SonarQube和使用OakPAL的內容包級檢查的組合來實現的。 有100多個規則，將通用Java規則和特定AEM規則組合在一起。 某些特AEM定規則是根據工程部門的最AEM佳做法建立的，稱為 [自定義代碼質量規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

>[!NOTE]
您可以下載規則的完整清單 [連結。](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### 三層評級 {#three-tiered-gate}

由代碼質量測試確定的問題被分配給三個類別中的一個。

* **關鍵**  — 這些問題導致管道立即失效。

* **重要**  — 這些問題導致管道進入暫停狀態。 部署經理、項目經理或業務所有者可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道將因失敗而停止。

* **資訊**  — 這些問題純粹是為了提供資訊而提供的，對管道執行沒有影響

此步驟的結果將作為 **評級**。

下表匯總了每個關鍵、重要和資訊類別的評級和故障閾值。

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全等級 | A =無漏洞 <br/>B =至少1個次要漏洞<br/> C =至少1個主要漏洞 <br/>D =至少1個嚴重漏洞 <br/>E =至少1個阻止程式漏洞 | 關鍵 | &lt; B |
| 可靠性評級 | A =無錯誤 <br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤<br>E =至少1個阻止程式錯誤 | Critical | &lt; D |
| 可維護性評級 | 由代碼氣味的未清補救成本定義，該成本佔已進入應用程式的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 由單位test行覆蓋和條件覆蓋的混合使用公式定義： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Conditions that have been evaluated as `true` at least once while running unit tests</li><li>`CF` =已評估為 `false` 運行設備test時至少一次</li><li>`LC` =覆蓋行=行到覆蓋 — 未覆蓋行</li><li>`B` =條件總數</li><li>`EL` = total number of executable lines (lines_to_cover)</li></ul> | 重要 | &lt; 50% |
| 跳過的設備Test | 跳過的設備test數 | 資訊 | > 1 |
| 未解決問題 | 總體問題類型 — 漏洞、錯誤和代碼氣味 | 資訊 | > 0 |
| 重複行 | Defined as the number of lines involved in duplicated blocks. 在以下情況下，代碼塊被視為重複。<br>非Java項目：<ul><li>至少應有100個連續和重複的令牌。</li><li>這些令牌至少應該分佈在以下幾個方面： </li><li>COBOL的30行代碼 </li><li>20 lines of code for ABAP </li><li>10行代碼供其他語言使用</li></ul>Java項目：<ul></li><li> There should be at least 10 successive and duplicated statements regardless of the number of tokens and lines.</li></ul>Differences in indentation as well as in string literals are ignored when detecting duplicates. | 資訊 | > 1% |
| Cloud Service相容性 | 確定的雲服務相容性問題數 | 資訊 | > 0 |

>[!NOTE]
請參閱 [SonarQube的度量定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 的子菜單。

>[!NOTE]
瞭解有關由執行的自定義代碼質量規則的詳細資訊 [!UICONTROL 雲管理器]，請參閱文檔 [自定義代碼質量規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 處理誤報 {#dealing-with-false-positives}

質量掃描過程不完善，有時會錯誤地識別實際上沒有問題的問題。 這稱為 **假陽性**。

在這些情況下，可以使用標準Java對原始碼進行注釋 `@SuppressWarnings` 注釋，將規則ID指定為注釋屬性。 例如，一個常見的誤報是，用於檢測硬編碼密碼的SonarQube規則在如何識別硬編碼密碼方面具有攻擊性。

以下代碼在項目中相當常AEM見，該項目具有連接到某些外部服務的代碼。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後將引發阻止程式漏洞。 但是，在查看代碼後，您會發現這不是漏洞，並且可以使用相應的規則ID對代碼進行注釋。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

However, if the code was actually this:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後，正確的解決方案是刪除硬編碼密碼。

>[!NOTE]
雖然這是最好的做法 `@SuppressWarnings` 注釋盡可能特定，即僅注釋導致問題的特定語句或塊，可以在類級別進行注釋。

>[!NOTE]
雖然沒有明確的安全測試步驟，但在代碼質量步驟中有與安全相關的代碼質量規則被評估。 Refer to the document [Security Overview for AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) to learn more about security in Cloud Service.

## 內容包掃描優化 {#content-package-scanning-optimization}

作為質量分析流程的一部分，Cloud Manager會對Maven構建生成的內容包進行分析。 Cloud Manager offers optimizations to accelerate this process, which are effective when certain packaging constraints are observed. 最重要的是，對輸出單個內容包的項目執行的優化，通常稱為「全部」包，其中包含由生成生成的許多其他內容包，這些內容包被標籤為已跳過。 When Cloud Manager detects this scenario, rather than unpack the &quot;all&quot; package, the individual content packages are scanned directly and sorted based on dependencies. 例如，請考慮以下生成輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` （內容包）
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` （跳過的內容包）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` （跳過的內容包）

如果只有內部項 `myco-all-1.0.0-SNAPSHOT.zip` 是兩個跳過的內容包，然後掃描兩個嵌入的包，而不是「全部」內容包。

對於生成數十個嵌入式軟體包的項目，顯示此優化後每執行管道可節省10分鐘。

當「全部」內容包包含跳過的內容包和OSGi包的組合時，可能會出現特殊情況。 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 其中包含了之前提到的兩個嵌入式軟體包以及一個或多個OSGi包，然後僅使用OSGi包構建一個新的、最小的內容包。 此包始終被命名 `cloudmanager-synthetic-jar-package` 包裝的束被放入 `/apps/cloudmanager-synthetic-installer/install`。

>[!NOTE]
* 此優化不會影響部署到的包AEM。
* Because the matching between the embedded content packages and the skipped content packages is based on file names, this optimization cannot be performed if multiple skipped content packages have exactly the same file name or if the file name is changed while embedding.

