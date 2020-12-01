---
title: 學習搭配使用GraphQL與AEM —— 範例內容與查詢
description: 瞭解如何搭配AEM使用GraphQL —— 範例內容與查詢。
translation-type: tm+mt
source-git-commit: 46e179faa7875c4b3e9da30356d2b82d4b25b130
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 6%

---


# 瞭解如何搭配AEM使用GraphQL —— 範例內容與查詢{#learn-graphql-with-aem-sample-content-queries}

>[!CAUTION]
>
>AEM GraphQL API（針對內容片段傳送）將於2021年初發行。
>
>相關檔案已可供預覽使用。

若要開始使用GraphQL查詢，以及查詢如何使用AEM內容片段，請參閱一些實用範例。

若要協助此項作業，請參閱：

* A [範例內容片段結構](#content-fragment-structure-graphql)

* 以及一些[範例GraphQL查詢](#graphql-sample-queries)，基於範例內容片段結構（內容片段模型和相關內容片段）。

## GraphQL for AEM —— 某些擴展{#graphql-some-extensions}

使用GraphQL for AEM對查詢的基本操作符合標準GraphQL規範。 對於具有AEM的GraphQL查詢，有幾個擴充功能：

* 如果您需要單一結果：
   * 使用模型名稱；eg城市

* 如果您希望得到結果清單：
   * 在模型名稱中添加「清單」;例如，`cityList`

* 如果要使用邏輯OR:
   * 使用&quot; _logOp:OR&quot;

* 邏輯AND也存在，但是是（通常）隱式的

* 您可以查詢與內容片段模型中欄位對應的欄位名稱

* 除了模型中的欄位外，還有一些系統產生的欄位（以底線為先）:

   * 針對內容：

      * `_locale` :揭露語言；基於語言管理器

      * `_metadata` :顯示片段的中繼資料

      * `_path` :儲存庫內內容碎片的路徑

      * `_references` :顯示參照；包括RTF編輯器中的內嵌引用

      * `_variations` :以顯示內容片段中的特定變化
   * 及營運：

      * `_operator` :適用特定運算子； `EQUALS`、 `EQUALS_NOT`、 `GREATER_EQUAL`、 `LOWER`、 `CONTAINS`、

      * `_apply` :適用特定條件；例如，   `AT_LEAST_ONCE`

      * `_ignoreCase` :在查詢時忽略大小寫


* 支援GraphQL聯合類型：

   * 使用`...on`


## 用於GraphQL {#content-fragment-structure-graphql}的示例內容片段結構

如需簡單範例，我們需要：

* 一個或多個[示例內容片段模型](#sample-content-fragment-models-schemas) —— 構成GraphQL架構的基礎

* [基於上](#sample-content-fragments) 述模型的範例內容片段

### 內容片段模型範例（結構）{#sample-content-fragment-models-schemas}

對於範例查詢，我們將使用下列內容模型及其相互關係（參照->）:

* [公司](#model-company)
->人 [員](#model-person)
    ->獎 [項](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定義公司的基本欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 公司名稱 | 單行文字 |  |
| 執行長 | 片段參考（單一） | [人員](#model-person) |
| 員工 | 片段參考（多欄位） | [人員](#model-person) |

#### 人員 {#model-person}

定義人員的欄位，也可以是員工：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 名字 | 單行文字 |  |
| 獎項 | 片段參考（多欄位） | [獎項](#model-award) |

#### 獎項{#model-award}

定義獎勵的欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 捷徑/ID | 單行文字 |  |
| 標題 | 單行文字 |  |

#### 城市 {#model-city}

用於定義城市的欄位包括：

| 欄位名稱 | 資料類型 | 引用 |
|--- |--- |--- |
| 名稱 | 單行文字 |  |
| 國家/地區 | 單行文字 |  |
| 人口 | 數量 |  |
| 類別 | 標記 |  |

### 範例內容片段{#sample-content-fragments}

以下片段用於適當的模型。

#### 公司 {#fragment-company}

| 公司名稱 | 執行長 | 員工 |
|--- |--- |--- |
| Apple | 史蒂夫·喬布斯 | 杜克·馬什<br>麥克斯·考爾菲爾德 |
|  小馬公司 | 亞當·斯密 | Lara Croft<br>Cutter Slade |
| NextStep Inc. | 史蒂夫·喬布斯 | 喬·史密斯<br>阿貝·林肯 |

#### 人員 {#fragment-person}

| 名稱 | 名字 | 獎項 |
|--- |--- |--- |
| 林肯 |  阿貝 |  |
| 史密斯 | Adam |   |
| 斯萊德 |  刀具 |  Gameblitz<br>Gamestar |
| 馬什 |  杜克 |   |   |
|  史密斯 |  喬 |   |
| 克羅夫特 |  拉拉 | Gamestar |
| Caulfield |  最大值 |  加梅布利茨 |
|  工作 |  史蒂夫 |   |

#### 獎項{#fragment-award}

| 捷徑/ID | 標題 |
|--- |--- |
| GB | 加梅布利茨 |
|  GS | Gamestar |
|  OSC | 奧斯卡 |

#### 城市 {#fragment-city}

| 名稱 | 國家/地區 | 人口 | 類別 |
|--- |--- |--- |--- |
| 巴塞爾 | 瑞士 | 郵編：172258 | 城市： emea |
| 柏林 | 德國 | 郵編：3669491 | 城市：資本<br>城市： emea |
| 布加勒斯特 | 羅馬尼亞 | 1821000 |  城市：資本<br>城市： emea |
| 舊金山 |  美國 |  郵編883306 |  城市：海灘<br>城市：na |
| 聖荷西 |  美國 |  郵編：102635 |  城市：納 |
| 斯圖加特 |  德國 |  郵編：634830 |  城市： emea |
|  蘇黎世 |  瑞士 |  郵編415367 |  城市：資本<br>城市： emea |

## GraphQL —— 使用示例內容片段結構{#graphql-sample-queries-sample-content-fragment-structure}的示例查詢

請參閱建立查詢的範例查詢以及範例結果。

>[!NOTE]
>
>根據您的例項，您可以直接存取AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)隨附的[Graph *i* QL介面，以提交和測試查詢。
>
>例如：`http://localhost:4502/content/graphiql.html`

### 示例查詢——所有可用方案和資料類型{#sample-all-schemes-datatypes}

這將返回所有可用方案的所有類型。

**範例查詢**

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

### 示例查詢——公司CEO和員工{#sample-full-details-company-ceos-employees}的完整詳細資訊

使用巢狀片段的結構，此查詢會傳回公司CEO及其所有員工的完整詳細資訊。

**範例查詢**

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

**範例結果**

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

### 範例查詢——所有城市的所有資訊{#sample-all-information-all-cities}

要檢索所有城市的所有資訊，可以使用非常基本的查詢：
**範例查詢**

```xml
{
  cityList {
    items
  }
}
```

執行時，系統會自動展開查詢以包含所有欄位：

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

**範例結果**

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

### Sample Query —所有城市的名稱{#sample-names-all-cities}

這是一個直接查詢，用於返回`city`模式中所有條目的`name`。

**範例查詢**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**範例結果**

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

### 範例查詢——單一城市片段{#sample-single-city-fragment}

這是一個查詢，用於在儲存庫中的特定位置返回單個片段條目的詳細資訊。

**範例查詢**

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

**範例結果**

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

### 範例查詢——具有命名變異{#sample-cities-named-variation}的所有城市

如果您為`city`柏林建立名為「柏林中心」(`berlin_centre`)的新變數，則可使用查詢來傳回變數的詳細資料。

**範例查詢**

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

**範例結果**

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

### 示例查詢——名稱為&quot;Jobs&quot;或&quot;Smith&quot; {#sample-all-persons-jobs-smith}的所有人員

這會針對名稱為`Jobs`或`Smith`的任何項目篩選所有`persons`。

**範例查詢**

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

**範例結果**

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

### 示例查詢——所有名稱不為&quot;Jobs&quot; {#sample-all-persons-not-jobs}的人員

這會針對名稱為`Jobs`或`Smith`的任何項目篩選所有`persons`。

**範例查詢**

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

**範例結果**

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

### 範例查詢——位於德國或瑞士的所有城市，人口在400000到999999之間{#sample-all-cities-d-ch-population}

在此篩選欄位組合。 `AND`（隱式）用於選擇`population`範圍，而`OR`（顯式）用於選擇所需城市。

**範例查詢**

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

**範例結果**

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

### 示例查詢——名稱中包含SAN的所有城市，不考慮大小寫{#sample-all-cities-san-ignore-case}

此查詢詢問名稱中包含`SAN`的所有城市，而不考慮大小寫。

**範例查詢**

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

**範例結果**

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

### Sample Query —— 對包含項目的陣列進行篩選，該項目必須至少發生一次{#sample-array-item-occur-at-least-once}

此查詢會篩選具有項目(`city:na`)的陣列，且該項目必須至少發生一次。

**範例查詢**

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

**範例結果**

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

### Sample Query - Filter on a exact array value {#sample-array-exact-value}

此查詢會篩選精確的陣列值。

**範例查詢**

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

**範例結果**

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

### 巢狀內容片段的查詢範例——所有至少有一名員工且姓名為&quot;Smith&quot; {#sample-companies-employee-smith}的公司

此查詢說明了對`name` &quot;Smith&quot;的任何`person`的過濾，從兩個嵌套片段返回資訊- `company`和`employee`。

**範例查詢**

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

**範例結果**

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

### 巢狀內容片段的查詢範例——所有員工皆獲得「Gamestar」獎項{#sample-all-companies-employee-gamestar-award}的公司

此查詢說明了對三個嵌套片段的篩選- `company`、`employee`和`award`。

**範例查詢**

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

**範例結果**

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

### 中繼資料的範例查詢——列出標題為GB {#sample-metadata-awards-gb}的獎項中繼資料

此查詢說明了對三個嵌套片段的篩選- `company`、`employee`和`award`。

**範例查詢**

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

**範例結果**

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

## 使用WKND項目{#sample-queries-using-wknd-project}的示例查詢

這些示例查詢基於WKND項目。

>[!NOTE]
>
>由於結果可以廣泛，所以在這裡沒有重現。

### 具有指定屬性{#sample-wknd-all-model-properties}的特定模型的所有內容片段的範例查詢

此示例查詢詢問：

* `article`類型的所有內容片段
* 和`path`屬性。`author`

**範例查詢**

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

### 中繼資料的範例查詢{#sample-wknd-metadata}

此查詢詢問：

* `adventure`類型的所有內容片段
* 中繼資料

**範例查詢**

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

### 給定模型{#sample-wknd-single-content-fragment-of-given-model}的單個內容片段的示例查詢

此示例查詢詢問：

* 針對特定模型的單一內容片段
* 適用於所有格式的內容：
   * HTML
   * Markdown
   * 純文字
   * JSON

**範例查詢**

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

### 巢狀內容片段的範例查詢——單一模型類型{#sample-wknd-nested-fragment-single-model}

**範例查詢**

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

### 巢狀內容片段的範例查詢——多模型類型{#sample-wknd-nested-fragment-multiple-model}

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

### 具有內容參考的特定模型內容片段的範例查詢{#sample-wknd-fragment-specific-model-content-reference}

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

### 具有預取參照{#sample-wknd-multiple-fragments-prefetched-references}的多個內容片段的範例查詢

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
  }
}
```

### 給定模型{#sample-wknd-single-fragment-given-model}的單一內容片段變化的範例查詢

**範例查詢**

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

### 特定地區設定{#sample-wknd-multiple-fragments-given-locale}中多個內容片段的範例查詢

**範例查詢**

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

### 具有RTE內嵌引用{#sample-wknd-single-fragment-rte-inline-reference}的單個內容片段的示例查詢

**範例查詢**

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

### 給定模型{#sample-wknd-variation-multiple-fragment-given-model}的多個內容片段的命名變化的示例查詢

**範例查詢**

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
