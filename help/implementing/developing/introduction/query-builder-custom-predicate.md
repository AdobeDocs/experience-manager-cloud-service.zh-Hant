---
title: 為查詢產生器實作自訂述詞求值器
description: AEM中的查詢產生器提供簡單且可自訂的方式來查詢內容存放庫
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 為查詢產生器實作自訂述詞求值器 {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本檔案說明如何實作自訂述詞求值器來擴充[查詢產生器](query-builder-api.md)。

## 概觀 {#overview}

[查詢產生器](query-builder-api.md)提供查詢內容存放庫的簡單方法。 AEM隨附[一組述詞評估器](#query-builder-predicates.md)，可協助您查詢資料。

不過，您可能想要實作自訂述詞評估器來簡化查詢，該評估器會隱藏一些複雜度並確保語意更佳。

自訂述詞也可以執行其他不直接與XPath一起執行的動作，例如：

* 正在查詢其他服務的資料
* 根據計算的自訂篩選

>[!NOTE]
>
>實作自訂述詞時必須考慮效能問題。

>[!TIP]
>
>您可以在[查詢產生器](query-builder-api.md)檔案中找到查詢範例。

>[!TIP]
>
>您可以在GitHub上找到此頁面的程式碼
>
>* 在GitHub上[開啟aem-search-custom-predicate-evaluator專案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* 將專案下載為[ZIP檔](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

>[!NOTE]
>
>GitHub上的連結程式碼以及本檔案中的程式碼片段僅供示範之用。

### 述詞求值器詳細資料 {#predicate-evaluator-in-detail}

述詞評估器處理特定述詞的評估，這些述詞是查詢的定義限制。

它將較高層級的搜尋條件約束（例如`width>200`）對應到符合實際內容模型（例如`metadata/@width > 200`）的特定JCR查詢。 或者，它可以手動篩選節點並檢查其限制。

>[!TIP]
>
>如需`PredicateEvaluator`與`com.day.cq.search`封裝的詳細資訊，請參閱[Java檔案](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html)。

### 實施復寫中繼資料的自訂述詞求值器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

本節以範例說明如何建立自訂述詞評估器，協助根據復寫中繼資料的資料：

* 儲存上次復寫動作日期的`cq:lastReplicated`
* `cq:lastReplicatedBy`儲存觸發上次復寫動作之使用者的識別碼
* 儲存上次復寫動作（例如啟用、停用）的`cq:lastReplicationAction`

#### 使用預設述詞評估器查詢復寫中繼資料 {#querying-replication-metadata-with-default-predicate-evaluators}

下列查詢會擷取`/content`分支中自年初以來由`admin`啟動的節點清單。

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

此查詢有效，但難以讀取，且不會強調三個復寫屬性之間的關係。 實作自訂述詞求值器將降低複雜性並改善此查詢的語意。

#### 目標 {#objectives}

`ReplicationPredicateEvaluator`的目標是使用下列語法支援上述查詢。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自訂述詞求值器將復寫中繼資料述詞分組，有助於建立有意義的查詢。

#### 更新Maven相依性 {#updating-maven-dependencies}

>[!TIP]
>
>[WKND教學課程](develop-wknd-tutorial.md)會詳細說明新AEM專案的設定，包括使用Maven。

首先，您需要更新專案的Maven相依性。 `PredicateEvaluator`是`cq-search`成品的一部分，因此必須將其新增到您的Maven pom檔案。

>[!NOTE]
>
>`cq-search`相依性的範圍已設定為`provided`，因為`cq-search`是由`OSGi`容器所提供。

下列程式碼片段顯示`pom.xml`檔案中的差異，格式為[統一的diff](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### 正在寫入ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

`cq-search`專案包含`AbstractPredicateEvaluator`抽象類別。 這可以透過幾個步驟來延伸以實作您自己的自訂述詞求值器`(PredicateEvaluator`)。

>[!NOTE]
>
>下列程式說明如何建置`Xpath`運算式以篩選資料。 另一個選項是實作以列為基礎選取資料的`includes`方法。 如需詳細資訊，請參閱[Java檔案](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)。

1. 建立擴充`com.day.cq.search.eval.AbstractPredicateEvaluator`的新Java類別
1. 以`@Component`統一的diff格式[使用](https://en.wikipedia.org/wiki/Diff#Unified_format)之類的程式碼片段來標註您的類別

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >`factory`必須是以`com.day.cq.search.eval.PredicateEvaluator/`開頭並以自訂`PredicateEvaluator`的名稱結尾的唯一字串。

   >[!NOTE]
   >
   >`PredicateEvaluator`的名稱是建立查詢時使用的述詞名稱。

1. 覆寫：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆寫方法中，您會根據引數中指定的`Xpath`建置`Predicate`運算式。

### 復寫中繼資料的自訂述詞求值器範例 {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

此`PredicateEvaluator`的完整實作可能類似於以下類別。

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
