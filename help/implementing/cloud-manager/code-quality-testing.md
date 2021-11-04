---
title: 程式碼品質測試 — Cloud Services
description: 程式碼品質測試 — Cloud Services
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: f8695dd8fdc9ffb203bab943c335ab2957df6251
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 1%

---

# 程式碼品質測試 {#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="程式碼品質測試"
>abstract="程式碼品質測試會評估應用程式程式碼的品質。 這是僅限程式碼品質管道的核心目標，會在所有非生產和生產管道的建立步驟後立即執行。"

程式碼品質測試會評估應用程式程式碼的品質。 這是僅限程式碼品質管道的核心目標，會在所有非生產和生產管道的建立步驟後立即執行。

請參閱 [設定CI-CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 以進一步了解不同類型的管道。

## 了解程式碼品質規則 {#understanding-code-quality-rules}

在程式碼品質測試中，會掃描原始碼，以確保其符合特定品質標準。 目前，這是透過SonarQube與內容封裝層級檢查的組合，使用OakPAL來實作。 有100多個規則結合一般Java規則和AEM專用規則。 部分AEM專用規則是根據AEM Engineering的最佳實務建立，並稱為 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>您可以下載完整的規則清單 [此處](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

**三層門**

針對已識別的問題，此程式碼品質測試步驟中有三層結構：

* **關鍵**:這些是閘道所識別的問題，會造成管道立即失敗。

* **重要**:這些是閘道所識別的問題，導致管道進入暫停狀態。 部署經理、項目經理或業務負責人可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道會因故障而停止。

* **資訊**:這些是閘道所識別的問題，僅供參考，對管道執行沒有影響

此步驟的結果以 *評等*.

下表匯總了每個「關鍵」、「重要」和「資訊」類別的評級和故障閾值：

| 名稱 | 定義 | 類別 | 失敗閾值 |
|--- |--- |--- |--- |
| 安全性評等 | A = 0漏洞 <br/>B =至少1個小漏洞<br/> C =至少1個重大漏洞 <br/>D =至少1個嚴重漏洞 <br/>E =至少1個阻止程式漏洞 | 關鍵 | &lt; B |
| 可靠性等級 | A = 0錯誤 <br/>B =至少1個小錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤E =至少1個阻止程式錯誤 | 重要 | &lt; C |
| 維修性等級 | 代碼氣味的未補償成本是： <br/><ul><li>&lt;=5%已進入應用程式的時間，評等為A </li><li>6%到10%的評等是a B </li><li>11%到20%的評等是C </li><li>21%到50%的評等是D</li><li>超過50%的是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 使用以下公式的單元測試線覆蓋和條件覆蓋的組合： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>其中：CT =運行單元測試時至少評估為「true」的條件 <br/>CF =運行單元測試時已評估為「false」的條件 <br/>LC =覆蓋線= lines_to_cover - uncovered_lines <br/><br/> B =條件總數 <br/>EL =可執行行的總數(linestocover) | 重要 | &lt; 50% |
| 已跳過的單元測試 | 已跳過的單元測試數。 | 資訊 | > 1 |
| 未結問題 | 整體問題類型 — 弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 重複行 | 重複塊中涉及的行數。 <br/>若要將程式碼區塊視為重複： <br/><ul><li>**非Java專案：**</li><li>至少應有100個連續和重複的代號。</li><li>這些代號至少應散布在： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行代碼以供其他語言使用</li><li>**Java項目：**</li><li> 無論代號和行的數量多寡，至少應有10個連續且重複的陳述式。</li></ul> <br/>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | > 1% |
| Cloud Service相容性 | 已識別的Cloud Service相容性問題數。 | 資訊 | > 0 |

>[!NOTE]
>
>請參閱 [量度定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 以取得更詳細的定義。


>[!NOTE]
>
>若要進一步了解由執行的自訂程式碼品質規則 [!UICONTROL Cloud Manager]，請參閱 [自訂程式碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## 處理誤判 {#dealing-with-false-positives}

質量掃描過程不完美，有時會錯誤地識別實際上沒有問題的問題。 這稱為 *偽陽性*.

在這些情況下，可以使用標準Java對原始碼進行注釋 `@SuppressWarnings` 將規則ID指定為注釋屬性的注釋。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於硬編碼密碼的識別方式可能具有攻擊性。

若要查看特定範例，此程式碼在AEM專案中很常見，其程式碼可連線至某些外部服務：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後會引發Blocker漏洞。 檢閱程式碼後，您即可識別這不是漏洞，並可以使用適當的規則ID加以註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但另一方面，如果程式碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那麼正確的解決方案就是刪除硬式編碼的密碼。

>[!NOTE]
>
>雖然最佳實務是讓 `@SuppressWarnings` 注釋盡可能具體，即僅注釋導致問題的特定語句或塊，可以在類級別進行注釋。

>[!NOTE]
>雖然沒有明確的「安全性測試」步驟，但在程式碼品質步驟期間仍會評估與安全性相關的程式碼品質規則。 請參閱 [AEM安全性概述as a Cloud Service](/help/security/cloud-service-security-overview.md) 深入了解Cloud Service的安全性。
