---
title: 瞭解您的測試結果——雲端服務
description: 瞭解測試結果——雲端服務
translation-type: tm+mt
source-git-commit: ff9823f3d083ebc1dc5d130919144fe3678a13ed
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 3%

---


# 了解測試結果 {#understand-test-results}

使用 Cloud Manager 進行雲端服務管線執行時，會支援針對預備環境執行的測試。這與在「建立和裝置測試」步驟中執行的測試相反，這些測試會離線執行，而且無法存取任何執行中的AEM環境。

Cloud Manager for Cloud Services Pipeline支援的測試有三大類：

1. [程式碼品質測試](#code-quality-testing)
1. [功能測試](#functional-testing)
1. [內容審核測試](#content-audit-testing)

這些測試可以是：

* 客戶撰寫
* Adobe編寫
* Powered by Google的Lighthouse作為開放原始碼工具

   >[!NOTE]
   > 客戶撰寫的測試和Adobe撰寫的測試都可在專為執行這些類型測試而設計的容器化基礎架構中執行。


## 程式碼品質測試 {#code-quality-testing}

作為管道的一部分，會掃描原始碼，以確保部署符合特定的質量標準。 目前，這是由SonarQube和使用OakPAL的內容封裝層級檢查組合來實作的。 有超過100種規則結合一般Java規則和AEM特定規則。 下表摘要了測試標準的評分：

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全性分級 | A = 0漏洞 <br/>B =至少1個小漏洞<br/> C =至少1個大漏洞 <br/>D =至少1個嚴重漏洞 <br/>E =至少1個攔截器漏洞 | 關鍵 | &lt; B |
| 可靠性分級 | A = 0錯誤 <br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤E =至少1個攔截器錯誤 | 重要 | &lt; C |
| 可維護性評級 | 代碼氣味的未付補救成本是： <br/><ul><li>&lt;=5%已進入應用程式的時間，評分為A </li><li>6%到10%的評分是B </li><li>11%到20%的評分是C </li><li>21%到50%的評分是D</li><li>超過50%的項目是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 單位測試線覆蓋率與條件覆蓋率的混合使用公式： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>其中：CT =運行單元測試時至少評估為&#39;true&#39;的條件 <br/>CF =運行單元測試時評估為&#39;false&#39;的條件至少一次，而 <br/>LC =覆蓋行= lines_to_cover - uncovered_lines <br/><br/> B =條件 <br/>EL =可執行行(lines_to_cover)的總數 | 重要 | &lt; 50% |
| 跳過的設備測試 | 跳過的單元測試數。 | 資訊 | > 1 |
| 未結問題 | 整體問題類型——弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 複製行 | 重複塊中涉及的行數。 <br/>對於要視為複製的代碼塊： <br/><ul><li>**非Java專案：**</li><li>至少應有100個連續和重複的Token。</li><li>這些預付碼應至少分散於： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行其他語言的程式碼</li><li>**Java專案：**</li><li> 不論預付碼和行數為何，至少應有10個連續和重複的陳述式。</li></ul> <br/>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | > 1% |
| 雲端服務相容性 | 已識別的雲端服務相容性問題數目。 | 資訊 | > 0 |


>[!NOTE]
>
>請參閱 [量度定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，以取得詳細定義。

您可以在此處下載規 [則清單-quality-rules.xlsx](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx)

>[!NOTE]
>
>若要進一步瞭解 [!UICONTROL Cloud Manager執行的自訂代碼品質規則]，請參閱自 [訂代碼品質規則](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

### 處理誤報 {#dealing-with-false-positives}

品質掃描程式不完善，有時會錯誤地識別實際上沒有問題的問題。 這稱為「假陽性」。

在這些情況下，原始碼可以用標準Java注釋加以注 `@SuppressWarnings` 釋，該標準Java注釋指定規則ID作為注釋屬性。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於如何識別硬編碼密碼具有攻擊性。

若要檢視特定範例，此程式碼在AEM專案中相當常見，該專案具有連接至某些外部服務的程式碼：

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
>儘管最好使注釋盡可能具體 `@SuppressWarnings` （即僅注釋導致問題的特定語句或塊），但可以在類別級別注釋。

>[!NOTE]
>雖然沒有明確的「安全性測試」步驟，但在代碼品質步驟中仍會評估與安全性相關的代碼品質規則。 如需詳 [細資訊，請參閱AEM的安全性概觀(Security Overview for AEM a Cloud Service](/help/security/cloud-service-security-overview.md) )。

## 功能測試 {#functional-testing}

功能測試分為兩種類型：

* 產品功能測試
* 自訂功能測試

### 產品功能測試 {#product-functional-testing}

產品功能測試是一組穩定的HTTP整合測試(IT)，以製作、複製為主，可防止客戶在應用程式程式碼中斷AEM的核心功能時，對其應用程式碼進行變更。
每當客戶將新代碼部署到Cloud Manager時，這些代碼都會自動運行。

流水線中的產品功能測試步驟始終存在，不能跳過。此步驟是在階段部署後立即完成的。

### 自訂功能測試 {#custom-functional-testing}

管線中的「自訂功能」測試步驟始終存在，且無法跳過。

但是，如果構建版本未生成測試JAR，則預設情況下測試通過。

>[!NOTE]
>「下 **載日誌** 」按鈕允許訪問包含測試執行詳細表單日誌的ZIP檔案。這些記錄檔不包含實際AEM執行階段程式的記錄檔——這些記錄檔可使用一般的「下載」或「尾部記錄檔」功能來存取。 如需詳細 [資訊，請參閱存取和管理記錄](/help/implementing/cloud-manager/manage-logs.md) 。


#### 編寫功能測試 {#writing-functional-tests}

客戶撰寫的功能測試必須封裝為由要部署至AEM的對象所產生的個別JAR檔案。 通常，此模組是單獨的Maven模組。 生成的JAR檔案必須包含所有必需的從屬關係，通常使用maven-assembly-plugin使用jar-with-dependencies描述符建立。

此外，JAR必須將Cloud-Manager-TestType資訊清單標題設為integration-test。 未來預計會支援其他標題值。 maven-assembly-plugin的範例組態為：

```java
<build>
    <plugins>
        <!-- Create self-contained jar with dependencies -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifestEntries>
                        <Cloud-Manager-TestType>integration-test</Cloud-Manager-TestType>
                    </manifestEntries>
                </archive>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
```

在此JAR檔案中，要執行的實際測試的類名必須以IT結束。

例如，將執行名為 `com.myco.tests.aem.ExampleIT` 的類，但不執行名 `com.myco.tests.aem.ExampleTest` 為的類。

測試類必須是常規JUnit測試。 測試基礎架構的設計與設定可與aem-testing-clients測試程式庫所使用的慣例相容。 強烈建議開發人員使用此程式庫並遵循其最佳實務。 請參閱 [Git連結](https://github.com/adobe/aem-testing-clients) ，以取得詳細資訊。

## 內容審核測試 {#content-audit-testing}

「內容審核」是Cloud Manager Sites Production管道中的一項功能，由Google的開放原始碼工具Lighthouse提供支援。 所有Cloud Manager生產管道都啟用了此功能。

它可驗證部署程式，並協助確保已部署變更：

1. 符合效能、協助工具、最佳實務、搜尋引擎最佳化(SEO)和PWA（漸進式網頁應用程式）的基準標準。

1. 不要在這些維度中加入回歸。

Cloud Manager中的內容審核可確保網站上的使用者數位體驗維持在最高標準。 這些結果是提供資訊的，讓使用者可以查看目前和先前的分數之間的分數和變更。 此見解對於判斷目前部署中是否會引入回歸，十分有用。

### 瞭解內容審核結果 {#understanding-content-audit-results}

「內容審核」透過「生產管道」執行頁面提供匯總和詳細的頁面層級測試結果。

* 匯總層級量度會測量已稽核之頁面的平均分數。
* 您也可以透過向下切入來取得個別頁面層級的分數。
* 您可以取得分數的詳細資訊，以查看個別測試的結果，以及如何修正內容審核期間發現的任何問題的指引。
* 測試結果的歷史記錄保存在Cloud Manager中，因此客戶可以查看在管道運行中引入的更改是否包含先前運行的任何回歸。

#### 匯總分數 {#aggregate-scores}

每個測試類型（效能、協助工具、SEO、最佳實務和PWA）都有匯總的等級分數。

匯總層級分數會取得執行中所包含之頁面的平均分數。 匯總層級的變更代表目前執行中頁面的平均分數，與前次執行的平均分數相比，即使設定為包含的頁面集合在執行之間已變更亦然。

「變更」量度的值可能是下列其中一項：

* **正值** -自上次生產管線執行以來，所選測試的頁面已改善

* **負值** -自上次生產管線執行以來，頁面在所選測試上已退縮

* **無更改** -自上次生產管道運行以來，頁面的分數相同

* **N/A** —— 沒有舊分數可供比較

   ![](assets/content-audit-test1.png)

#### 頁面層級分數 {#page-level-scores}

透過鑽取任何測試，可檢視更詳細的頁面等級計分。 使用者將能夠查看個別頁面在特定測試中的分數，以及與上次測試執行時的變更。

按一下任何個別頁面的詳細資訊，將會提供已評估頁面元素的資訊，並指引您在偵測到改善機會時修正問題。 Google Lighthouse提供測試的詳細資訊和相關指引。

![](assets/page-level-scores.png)

## 本地測試執行 {#local-test-execution}

由於測試類是JUnit測試，因此可以從主流Java IDE（如Eclipse、IntelliJ、NetBeans等）中運行。

不過，當執行這些測試時，必須設定aem-testing-clients（和基礎Sling Testing Clients）預期的各種系統屬性。

系統屬性如下：

* `sling.it.instances - should be set to 2`
* `sling.it.instance.url.1 - should be set to the author URL, for example, http://localhost:4502`
* `sling.it.instance.runmode.1 - should be set to author`
* `sling.it.instance.adminUser.1 - should be set to the author admin user, e.g. admin`
* `sling.it.instance.adminPassword.1 - should be set to the author admin password`
* `sling.it.instance.url.2 - should be set to the author URL, for example, http://localhost:4503`
* `sling.it.instance.runmode.2 - should be set to publish`
* `sling.it.instance.adminUser.2 - should be set to the publish admin user, for example, admin`
* `sling.it.instance.adminPassword.2 - should be set to the publish admin password`

