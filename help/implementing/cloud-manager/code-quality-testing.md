---
title: 程式碼品質測試-Cloud Services
description: 程式碼品質測試-Cloud Services
translation-type: tm+mt
source-git-commit: 5a945cbb138aea64ecc6da3728827531569d6d63
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---


# 程式碼品質測試{#code-quality-testing}

「程式碼品質測試」會評估您的應用程式碼的品質。 它是僅限程式碼品質管道的核心目標，並會立即在所有非生產及生產管道的建立步驟後執行。

請參閱[配置CI-CD管線](/help/implementing/cloud-manager/configure-pipeline.md)以進一步瞭解不同類型的管線。

## 瞭解代碼質量規則{#understanding-code-quality-rules}

在「程式碼品質測試」中，會掃描原始碼，以確保其符合特定品質標準。 目前，這是由SonarQube和使用OakPAL的內容封裝層級檢查組合來實作的。 有超過100種規則結合一般Java規則和AEM特定規則。 有些特定AEM規則是根據工程部門的最佳實踐AEM而建立，稱為[自訂代碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

>[!NOTE]
>您可以下載規則的完整清單[這裡](/help/implementing/cloud-manager/assets/CodeQuality-rules-CS.xlsx)。

**三層門**

此程式碼品質測試步驟中有三層結構，可針對已識別的問題：

* **重要**:這些是由澆口確定的問題，導致管線立即失效。

* **重要**:這些是由門所標識的導致管線進入暫停狀態的問題。部署經理、專案經理或業務負責人可以覆寫問題（在這種情況下，管道會繼續），或者接受問題（在這種情況下，管道會因故障而停止）。

* **資訊**:這些問題由網關確定，僅供參考，對管線執行沒有影響

此步驟的結果以&#x200B;*Ratings*&#x200B;的形式提供。

下表匯總了每個「嚴重」、「重要」和「資訊」類別的分級和故障閾值：

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全性分級 | A = 0漏洞<br/>B =至少1個小漏洞<br/> C =至少1個主漏洞<br/>D =至少1個嚴重漏洞<br/>E =至少1個攔截器漏洞 | 重要 | &lt; B |
| 可靠性分級 | A = 0錯誤<br/>B =至少1個次要錯誤<br/>C =至少1個主要錯誤<br/>D =至少1個嚴重錯誤E =至少1個攔截器錯誤 | 重要 | &lt; C=&quot;&quot;> |
| 可維護性評級 | 代碼氣味的未付補救成本是：<br/><ul><li>&lt;> </li><li>6%到10%的評分是B </li><li>11%到20%的評分是C </li><li>21%到50%的評分是D</li><li>超過50%的項目是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 單位測試線覆蓋率與條件覆蓋率的混合使用公式：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>其中：CT =運行單元測試時評估為「true」的條件，運行單元測試時，評估為「false」的條件，運行單元測試時，評估為「false」的條件至少一次，運行單元測試時，LC =覆蓋行= lines_to_cover - ouncated_lines <br/><br/> B =條件總數<br/>EL =可執行行總數(lines_to_cover)<br/><br/> | 重要 | &lt; 50% |
| 跳過的設備測試 | 跳過的單元測試數。 | 資訊 | > 1 |
| 未結問題 | 整體問題類型——弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 複製行 | 重複塊中涉及的行數。 <br/>對於要視為複製的代碼塊：  <br/><ul><li>**非Java專案：**</li><li>至少應有100個連續和重複的Token。</li><li>這些預付碼應至少分散於： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行其他語言的程式碼</li><li>**Java專案：**</li><li> 不論預付碼和行數為何，至少應有10個連續和重複的陳述式。</li></ul> <br/>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | > 1% |
| Cloud Service相容性 | 已識別的Cloud Service相容性問題數。 | 資訊 | > 0 |

>[!NOTE]
>
>請參閱[量度定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)以取得更詳細的定義。


>[!NOTE]
>
>若要進一步瞭解[!UICONTROL Cloud Manager]執行的自訂代碼品質規則，請參閱[自訂代碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 處理誤報{#dealing-with-false-positives}

品質掃描程式不完善，有時會錯誤地識別實際上沒有問題的問題。 這稱為&#x200B;*false陽性*。

在這些情況下，原始碼可以用標準Java `@SuppressWarnings`注釋加以注釋，該標準Java 注釋指定規則ID作為注釋屬性。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於如何識別硬編碼密碼具有攻擊性。

若要檢視特定範例，此程式碼在專案中相當常見，AEM專案中有程式碼可連接至某些外部服務：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後會提出一個「攔截器漏洞」。 在檢閱程式碼後，您會發現此程式碼不是弱點，並可使用適當的規則ID加以註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後，正確的解決方案是移除硬式編碼密碼。

>[!NOTE]
>
>儘管最佳做法是盡可能使`@SuppressWarnings`注釋具體，即僅注釋導致問題的特定語句或塊，但可以在類別級別注釋。

>[!NOTE]
>雖然沒有明確的「安全性測試」步驟，但在代碼品質步驟中仍會評估與安全性相關的代碼品質規則。 請參閱[安全性概述，以AEM作為Cloud Service](/help/security/cloud-service-security-overview.md)，以進一步瞭解Cloud Service中的安全性。
