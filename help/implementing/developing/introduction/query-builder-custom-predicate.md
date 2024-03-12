---
title: 為查詢產生器實作自訂述詞求值器
description: AEM中的查詢產生器提供簡單且可自訂的方式來查詢內容存放庫
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 為查詢產生器實作自訂述詞求值器 {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本檔案說明如何延伸 [查詢產生器](query-builder-api.md) 實作自訂述詞求值器。

## 概觀 {#overview}

此 [查詢產生器](query-builder-api.md) 提供查詢內容存放庫的簡單方法。 AEM隨附 [一組述詞評估器](#query-builder-predicates.md) 可協助您查詢資料。

不過，您可能想要實作自訂述詞評估器來簡化查詢，該評估器會隱藏一些複雜度並確保語意更佳。

自訂述詞也可以執行其他不直接與XPath一起執行的動作，例如：

* 正在查詢其他服務的資料
* 根據計算的自訂篩選

>[!NOTE]
>
>實作自訂述詞時必須考慮效能問題。

>[!TIP]
>
>您可在以下網址找到查詢範例： [查詢產生器](query-builder-api.md) 檔案。

>[!TIP]
>
>您可以在GitHub上找到此頁面的程式碼
>
>* [在GitHub上開啟aem-search-custom-predicate-evaluator專案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

>[!NOTE]
>
>GitHub上的連結程式碼以及本檔案中的程式碼片段僅供示範之用。

### 述詞求值器詳細資料 {#predicate-evaluator-in-detail}

述詞評估器處理特定述詞的評估，這些述詞是查詢的定義限制。

這會對應較高層級的搜尋限制(例如 `width>200`)至符合實際內容模型的特定JCR查詢(例如， `metadata/@width > 200`)。 或者，它可以手動篩選節點並檢查其限制。

>[!TIP]
>
>如需關於的詳細資訊 `PredicateEvaluator` 和 `com.day.cq.search` 套件請參閱 [Java檔案](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### 實施復寫中繼資料的自訂述詞求值器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

本節以範例說明如何建立自訂述詞評估器，協助根據復寫中繼資料的資料：

* `cq:lastReplicated` 儲存上次復寫動作的日期
* `cq:lastReplicatedBy` 會儲存觸發上次復寫動作之使用者的id
* `cq:lastReplicationAction` 儲存上次的復寫動作（例如啟用、停用）

#### 使用預設述詞評估器查詢復寫中繼資料 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查詢會擷取下列位置的節點清單： `/content` 已由啟用的分支 `admin` 從年初開始。

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

的目標 `ReplicationPredicateEvaluator` 是使用下列語法支援上述查詢。

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
>詳細說明新AEM專案的設定，包括使用Maven [wknd教學課程。](develop-wknd-tutorial.md)

首先，您需要更新專案的Maven相依性。 此 `PredicateEvaluator` 是 `cq-search` 成品，因此必須將其新增至您的Maven pom檔案。

>[!NOTE]
>
>範圍 `cq-search` 相依性已設定為 `provided` 因為 `cq-search` 由 `OSGi` 容器。

下列程式碼片段顯示 `pom.xml` 檔案，在 [統一的差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

此 `cq-search` 專案包含 `AbstractPredicateEvaluator` 抽象類別。 您只需幾個步驟即可擴充此功能，以實作您自己的自訂述詞評估器 `(PredicateEvaluator`)。

>[!NOTE]
>
>下列程式說明如何建置 `Xpath` 篩選資料的運算式。 另一個選項是實作 `includes` 以列為基礎選取資料的方法。 請參閱 [Java檔案](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) 以取得詳細資訊。

1. 建立可擴充的新Java類別 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用為課程加上註釋 `@Component` 如中的程式碼片段顯示 [統一的差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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
   >此 `factory`必須是唯一的字串，開頭為 `com.day.cq.search.eval.PredicateEvaluator/`結尾為您的自訂名稱 `PredicateEvaluator`.

   >[!NOTE]
   >
   >的名稱 `PredicateEvaluator` 是建立查詢時使用的述詞名稱。

1. 覆寫：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆寫方法中，您建置 `Xpath` 運算式基礎為 `Predicate` 在引數中給出。

### 復寫中繼資料的自訂述詞求值器範例 {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

此專案的完整實作 `PredicateEvaluator` 可能與以下類別類似。

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
