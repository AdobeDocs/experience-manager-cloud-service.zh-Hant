---
title: 代碼質量測試
description: 瞭解管道的代碼質量測試如何工作以及它如何提高部署質量。
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

代碼質量測試根據一組質量規則評估您的應用程式碼。 它是僅代碼質量管道的主要目的，並且在所有生產和非生產管道的構建步驟後立即執行。

請參閱文檔 [配置CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 瞭解有關不同類型管道的詳細資訊。

## 代碼質量規則 {#understanding-code-quality-rules}

代碼質量測試掃描原始碼以確保它滿足某些質量標準。 這是通過SonarQube和使用OakPAL的內容包級檢查的組合來實現的。 有100多個規則，將通用Java規則和特定AEM規則組合在一起。 某些特AEM定規則是根據工程部門的最AEM佳做法建立的，稱為 [自定義代碼質量規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

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
| 可靠性評級 | A =無錯誤 <br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤<br>E =至少1個阻止程式錯誤 | 關鍵 | &lt; D |
| 可維護性評級 | 由代碼氣味的未清補救成本定義，該成本佔已進入應用程式的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 由單位test行覆蓋和條件覆蓋的混合使用公式定義： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` =已評估為 `true` 運行設備test時至少一次</li><li>`CF` =已評估為 `false` 運行設備test時至少一次</li><li>`LC` =覆蓋行=行到覆蓋 — 未覆蓋行</li><li>`B` =條件總數</li><li>`EL` =可執行行（行到封面）總數</li></ul> | 重要 | &lt; 50% |
| 跳過的設備Test | 跳過的設備test數 | 資訊 | > 1 |
| 未解決問題 | 總體問題類型 — 漏洞、錯誤和代碼氣味 | 資訊 | > 0 |
| 重複行 | 定義為重複塊中涉及的行數。 在以下情況下，代碼塊被視為重複。<br>非Java項目：<ul><li>至少應有100個連續和重複的令牌。</li><li>這些令牌至少應該分佈在以下幾個方面： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行代碼供其他語言使用</li></ul>Java項目：<ul></li><li> 不管令牌和行數多少，至少應有10個連續重複的語句。</li></ul>在檢測重複項時，將忽略縮進和字串文字中的差異。 | 資訊 | > 1% |
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

但是，如果代碼是這樣的：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後，正確的解決方案是刪除硬編碼密碼。

>[!NOTE]
雖然這是最好的做法 `@SuppressWarnings` 注釋盡可能特定，即僅注釋導致問題的特定語句或塊，可以在類級別進行注釋。

>[!NOTE]
雖然沒有明確的安全測試步驟，但在代碼質量步驟中有與安全相關的代碼質量規則被評估。 請參閱文檔 [as a Cloud Service安全概AEM述](/help/security/cloud-service-security-overview.md) 瞭解有關Cloud Service安全的更多資訊。

## 內容包掃描優化 {#content-package-scanning-optimization}

作為質量分析流程的一部分，Cloud Manager會對Maven構建生成的內容包進行分析。 Cloud Manager提供優化功能以加速此過程，當觀察到某些打包約束時，此功能非常有效。 最重要的是，對輸出單個內容包的項目執行的優化，通常稱為「全部」包，其中包含由生成生成的許多其他內容包，這些內容包被標籤為已跳過。 當Cloud Manager檢測到此方案，而不是解包「全部」包時，將直接掃描各個內容包並根據相關性對其進行排序。 例如，請考慮以下生成輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` （內容包）
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` （跳過的內容包）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` （跳過的內容包）

如果只有內部項 `myco-all-1.0.0-SNAPSHOT.zip` 是兩個跳過的內容包，然後掃描兩個嵌入的包，而不是「全部」內容包。

對於生成數十個嵌入式軟體包的項目，顯示此優化後每執行管道可節省10分鐘。

當「全部」內容包包含跳過的內容包和OSGi包的組合時，可能會出現特殊情況。 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 其中包含了之前提到的兩個嵌入式軟體包以及一個或多個OSGi包，然後僅使用OSGi包構建一個新的、最小的內容包。 此包始終被命名 `cloudmanager-synthetic-jar-package` 包裝的束被放入 `/apps/cloudmanager-synthetic-installer/install`。

>[!NOTE]
* 此優化不會影響部署到的包AEM。
* 由於嵌入式內容包和跳過的內容包之間的匹配基於檔案名，因此如果多個跳過的內容包具有相同的檔案名或在嵌入時更改了檔案名，則無法執行此優化。

