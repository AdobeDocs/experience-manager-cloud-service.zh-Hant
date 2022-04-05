---
title: 學習將GraphQL與AEM樣例內容和查詢一起使用
description: 學習將GraphQL與一起AEM使用，通過瀏覽示例內容和查詢來無拘無束地為內容提供服務。
feature: Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
source-git-commit: a2e36e296749c79040c9687bbd88288d8977086d
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 6%

---

# 學習將GraphQL與AEM樣例內容和查詢一起使用 {#learn-graphql-with-aem-sample-content-queries}

學習將GraphQL與一起AEM使用，通過瀏覽示例內容和查詢來無拘無束地為內容提供服務。

>[!NOTE]
>
>此頁應與以下內容一起閱讀：
>
>* [內容片段](/help/assets/content-fragments/content-fragments.md)
>* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
>* [用AEM於內容片段的GraphQL API](/help/headless/graphql-api/content-fragments.md)


要開始使用GraphQL查詢以及它們如何使用內容AEM片段，可以查看一些實用示例。

要幫助此操作，請參閱：

* A [示例內容片段結構](#content-fragment-structure-graphql)

* 還有 [示例GraphQL查詢](#graphql-sample-queries)，基於樣本內容片段結構（內容片段模型和相關內容片段）。


## GraphQL — 使用示例內容片段結構的示例查詢 {#graphql-sample-queries-sample-content-fragment-structure}

有關建立查詢的圖例以及示例結果，請參閱這些示例查詢。

>[!NOTE]
>
>根據實例，您可以直接訪問 [GraphQL API附帶的AEMGraphiQL介面](/help/headless/graphql-api/graphiql-ide.md) 用於提交和測試查詢。
>
>例如：`http://localhost:4502/aem/graphiql.html`

>[!NOTE]
>
>示例查詢基於 [用於GraphQL的示例內容片段結構](#content-fragment-structure-graphql)

### 示例查詢 — 所有可用方案和資料類型 {#sample-all-schemes-datatypes}

這將返回所有 `types` 的下界。

**示例查詢**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### 示例查詢 — 有關所有城市的所有資訊 {#sample-all-information-all-cities}

要檢索有關所有城市的所有資訊，可以使用非常基本的查詢：
**示例查詢**

```xml
{
  cityList {
    items
  }
}
```

執行時，系統將自動擴展查詢以包括所有欄位：

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### 示例查詢 — 所有城市的名稱 {#sample-names-all-cities}

這是一個簡單的查詢，用於返回 `name`所有條目中 `city`架構。

**示例查詢**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### 示例查詢 — 單個特定城市片段 {#sample-single-specific-city-fragment}

這是一個查詢，用於返回儲存庫中特定位置的單個片段條目的詳細資訊。

**示例查詢**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### 示例查詢 — 具有命名變體的所有城市 {#sample-cities-named-variation}

如果您建立新變體，名為「柏林中心」(`berlin_centre`) `city` 然後，您可以使用查詢返回變體的詳細資訊。

**示例查詢**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### 示例查詢 — 公司CEO和員工的完整詳細資訊 {#sample-full-details-company-ceos-employees}

使用嵌套片段的結構，此查詢將返回公司CEO及其所有員工的完整詳細資訊。

**示例查詢**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### 示例查詢 — 名稱為「Jobs」或「Smith」的所有人員 {#sample-all-persons-jobs-smith}

這將篩選所有 `persons` 任何有名字的 `Jobs`或 `Smith`。

**示例查詢**

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### 示例查詢 — 沒有「職務」名稱的所有人員 {#sample-all-persons-not-jobs}

這將篩選所有 `persons` 任何有名字的 `Jobs`或 `Smith`。

**示例查詢**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### 示例查詢 — 所有冒險 `_path` 以特定前置詞開頭 {#sample-wknd-all-adventures-cycling-path-filter}

全部 `adventures` 何處 `_path` 以特定前置詞(`/content/dam/wknd/en/adventures/cycling`)。

**示例查詢**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### 示例查詢 — 位於德國或瑞士人口在40000至99999之間的所有城市 {#sample-all-cities-d-ch-population}

在此，將篩選欄位組合。 安 `AND` （隱式）用於選擇 `population`範圍 `OR` （顯式）用於選擇所需的城市。

**示例查詢**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### 示例查詢 — 名稱中包含SAN的所有城市，不考慮大小寫 {#sample-all-cities-san-ignore-case}

此查詢將詢問所有 `SAN` 名字裡，不管大小寫。

**示例查詢**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### 示例查詢 — 對包含項的陣列進行篩選，該項必須至少發生一次 {#sample-array-item-occur-at-least-once}

此查詢篩選具有項的陣列(`city:na`)必須至少發生一次。

**示例查詢**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 示例查詢 — 對精確陣列值進行篩選 {#sample-array-exact-value}

此查詢將篩選精確的陣列值。

**示例查詢**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 嵌套內容片段的查詢示例 — 至少有一個員工的名稱為「Smith」的所有公司 {#sample-companies-employee-smith}

此查詢說明了對任何 `person` 共 `name` 「Smith」，從兩個嵌套片段返回資訊 —  `company` 和 `employee`。

**示例查詢**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### 嵌套內容片段的查詢示例 — 所有員工都獲得「Gamestar」獎的所有公司 {#sample-all-companies-employee-gamestar-award}

此查詢說明了跨三個嵌套片段的篩選 —  `company`。 `employee`, `award`。

**示例查詢**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### 元資料查詢示例 — 列出標題為GB的獎項的元資料 {#sample-metadata-awards-gb}

此查詢說明了跨三個嵌套片段的篩選 —  `company`。 `employee`, `award`。

**示例查詢**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**示例結果**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## 使用WKND項目的示例查詢 {#sample-queries-using-wknd-project}

這些示例查詢基於WKND項目。 這包括：

* 可從以下位置獲得內容片段模型：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 以下位置提供的內容片段（和其他內容）:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>由於結果可能很廣，因此此處不再複製。

### 具有指定屬性的特定模型的所有內容片段的示例查詢 {#sample-wknd-all-model-properties}

此示例查詢詢問：

* 適用於所有類型的內容片段 `article`
* 和 `path`和 `author` 屬性。

**示例查詢**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 元資料的示例查詢 {#sample-wknd-metadata}

此查詢詢問：

* 適用於所有類型的內容片段 `adventure`
* 中繼資料

**示例查詢**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 給定模型的單個內容片段的示例查詢 {#sample-wknd-single-content-fragment-of-given-model}

此示例查詢詢問：

* 類型的單個內容片段 `article` 在特定路徑上
   * 其中，所有格式的內容：
      * HTML
      * Markdown
      * 純文字
      * JSON

**示例查詢**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### 從模型中查詢內容片段模型的示例 {#sample-wknd-content-fragment-model-from-model}

此示例查詢詢問：

* 單個內容片段
   * 底層內容片段模型的詳細資訊

**示例查詢**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### 嵌套內容片段的示例查詢 — 單模型類型{#sample-wknd-nested-fragment-single-model}

此查詢詢問：

* 類型的單個內容片段 `article` 在特定路徑上
   * 其中，引用（嵌套）片段的路徑和作者

>[!NOTE]
>
>欄位 `referencearticle` 具有資料類型 `fragment-reference`。

**示例查詢**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### 嵌套內容片段的示例查詢 — 多模型類型{#sample-wknd-nested-fragment-multiple-model}

此查詢詢問：

* 用於多個類型的內容片段 `bookmark`
   * 與特定模型類型的其他片段的片段引用 `article` 和 `adventure`

>[!NOTE]
>
>欄位 `fragments` 具有資料類型 `fragment-reference`，與模型 `Article`。 `Adventure` 的下界。

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### 具有內容引用的特定模型的內容片段的示例查詢{#sample-wknd-fragment-specific-model-content-reference}

此查詢有兩種類型：

1. 返回所有內容引用。
1. 返回類型的特定內容引用 `attachments`。

這些查詢會詢問：

* 用於多個類型的內容片段 `bookmark`
   * 內容引用到其他片段

#### 具有預取引用的多個內容片段的示例查詢 {#sample-wknd-multiple-fragments-prefetched-references}

以下查詢通過使用 `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### 帶附件的多個內容片段的示例查詢 {#sample-wknd-multiple-fragments-attachments}

以下查詢返回所有 `attachments`  — 特定欄位（子組）類型 `content-reference`:

>[!NOTE]
>
>欄位 `attachments` 具有資料類型 `content-reference`的子菜單。

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### 具有RTE內聯引用的單個內容片段的示例查詢 {#sample-wknd-single-fragment-rte-inline-reference}

此查詢詢問：

* 類型的單個內容片段 `bookmark` 在特定路徑上
   * 在此內，RTE內聯引用

>[!NOTE]
>
>RTE內聯引用在 `_references`。

**示例查詢**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 給定模型的單個內容片段變體的示例查詢 {#sample-wknd-single-fragment-given-model}

此查詢詢問：

* 類型的單個內容片段 `article` 在特定路徑上
   * 其中，與變化相關的資料： `variation1`

**示例查詢**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 給定模型多個內容片段的命名變體的示例查詢 {#sample-wknd-variation-multiple-fragment-given-model}

此查詢詢問：

* 用於類型的內容片段 `article` 具體變化： `variation1`

**示例查詢**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 給定區域設定的多個內容片段的示例查詢 {#sample-wknd-multiple-fragments-given-locale}

此查詢詢問：

* 用於類型的內容片段 `article` 在 `fr` 區域

**示例查詢**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## 示例內容片段結構（與GraphQL一起使用） {#content-fragment-structure-graphql}

示例查詢基於以下結構，該結構使用：

* 一個或多個， [示例內容片段模型](#sample-content-fragment-models-schemas)  — 構成GraphQL架構的基礎

* [示例內容片段](#sample-content-fragments) 基於上述模型

### 示例內容片段模型（架構） {#sample-content-fragment-models-schemas}

對於示例查詢，我們將使用以下內容模型及其相互關係（引用 — >）:

* [公司](#model-company)
-> [人員](#model-person)
    -> [獎](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定義公司的基本欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 公司名稱 | 單行文字 |  |
| 首席執行官 | 片段引用（單個） | [人員](#model-person) |
| 員工 | 片段引用（多欄位） | [人員](#model-person) |

#### 人員 {#model-person}

定義人員（也可以是員工）的欄位：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 名字 | 單行文字 |  |
| 獎項 | 片段引用（多欄位） | [獎](#model-award) |

#### 獎 {#model-award}

定義獎勵的欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 快捷方式/ID | 單行文字 |  |
| 標題 | 單行文字 |  |

#### 城市 {#model-city}

定義城市的欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 國家/地區 | 單行文字 |  |
| 人口 | 數量 |  |
| 類別 | 標記 |  |

### 示例內容片段 {#sample-content-fragments}

以下片段用於相應的模型。

#### 公司 {#fragment-company}

| 公司名稱 | 首席執行官 | 員工 |
|--- |--- |--- |
| Apple | 史蒂夫·喬布斯 | 杜克馬什<br>馬克斯·考菲爾德 |
|  小馬公司 | 亞當·斯密 | 拉拉·克羅夫特<br>刀刀刀 |
| NextStep公司 | 史蒂夫·喬布斯 | 喬·史密斯<br>阿貝·林肯 |

#### 人員 {#fragment-person}

| 名稱 | 名字 | 獎項 |
|--- |--- |--- |
| 林肯 |  阿部 |  |
| 史密斯 | Adam |   |
| 斯拉德 |  刀具 |  加梅布利茨<br>加梅斯塔 |
| 馬什 |  杜克 |   |   |
|  史密斯 |  喬 |   |
| 克羅夫特 |  拉拉 | 加梅斯塔 |
| 考菲爾德 |  最大值 |  加梅布利茨 |
|  工作 |  史蒂夫 |   |

#### 獎 {#fragment-award}

| 快捷方式/ID | 標題 |
|--- |--- |
| GB | 加梅布利茨 |
|  GS | 加梅斯塔 |
|  OSC | 奧斯卡 |

#### 城市 {#fragment-city}

| 名稱 | 國家/地區 | 人口 | 類別 |
|--- |--- |--- |--- |
| 巴塞爾 | 瑞士 | 172258 | 城市：emea |
| 柏林 | 德國 | 3669491 | 城市：首都<br>城市：emea |
| 布加勒斯特 | 羅馬尼亞 | 1821000 |  城市：首都<br>城市：emea |
| 舊金山 |  美國 |  883306 |  城市：海灘<br>城市：納 |
| 聖荷西 |  美國 |  102635 |  城市：納 |
| 斯圖加特 |  德國 |  634830 |  城市：emea |
|  蘇黎世 |  瑞士 |  415367 |  城市：首都<br>城市：emea |
