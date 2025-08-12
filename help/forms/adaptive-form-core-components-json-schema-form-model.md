---
title: 如何為最適化表單核心元件設計JSON結構描述？
description: 瞭解如何為最適化表單核心元件建立JSON結構描述，並根據此結構描述建立最適化表單（核心元件），以產生結構描述投訴資料。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 185b12bc-cea9-45c8-9b57-dc313bd0cfaa
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 4%

---

# 設計最適化表單的 JSON 結構 (核心元件){#creating-adaptive-forms-using-json-schema}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| 基礎 | [按一下這裡](/help/forms/adaptive-form-json-schema-form-model.md) |
| 核心元件 | 本文章 |


## 先決條件 {#prerequisites}

使用JSON結構描述作為表單模型，根據核心元件製作調適型表單需要基本瞭解JSON結構描述。 建議您先閱讀下列內容，再閱讀本文。

* [根據核心元件建立最適化表單](/help/forms/creating-adaptive-form-core-components.md)
* [JSON結構描述](https://json-schema.org/)

## 使用JSON結構描述作為表單模型  {#using-a-json-schema-as-form-model}

Adobe Experience Manager Forms支援以現有JSON結構描述作為表單模型，根據核心元件建立最適化表單。 此JSON結構描述代表組織中後端系統產生或使用資料的結構。 您使用的JSON結構描述應符合[v4規格](https://json-schema.org/draft-04/schema)。

使用JSON結構描述的主要功能包括：

* JSON的結構在最適化表單的製作模式中，會以樹狀結構顯示在「內容尋找器」標籤中。 您可以根據核心元件，將元素從JSON階層拖曳並新增至調適型表單。
* 您可以使用與關聯結構描述相容的JSON預先填入表單。
* 在提交時，使用者輸入的資料會以JSON格式提交，且符合相關聯的結構描述。
* 您也可以根據[2012-20 version](https://json-schema.org/draft/2020-12/release-notes)的規格，以JSON結構描述為基礎建立表單。

JSON結構描述包含簡單和複雜的元素型別。 元素具有將規則新增至元素的屬性。 將這些元素和屬性拖曳至最適化表單時，會自動對應至對應的最適化表單元件。

JSON元素與最適化表單元件的對應如下：

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON元素、屬性或屬性</strong></th>
   <th><strong>最適化表單元件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames條件約束的字串屬性。</p> <p>語法，</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉式元件：</p>
    <ul>
     <li>enumNames中列出的值會顯示在拖放方塊中。</li>
     <li>列舉中列出的值會用於計算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>具有格式限制的字串屬性。 例如，電子郵件和日期。</p> <p>語法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>當型別為字串且格式為電子郵件時，會對映電子郵件元件。</li>
     <li>當型別為字串且格式為主機名稱時，會對應具有驗證的Textbox元件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 文字欄位<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number屬性<br /> </td>
   <td>子型別設定為float<br />的數值欄位 </td>
  </tr>
  <tr>
   <td>整數屬性<br /> </td>
   <td>子型別設定為整數<br />的數值欄位 </td>
  </tr>
  <tr>
   <td>布林值屬性<br /> </td>
   <td>切換<br /> </td>
  </tr>
  <tr>
   <td>物件屬性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>陣列屬性</td>
   <td>可重複面板，最小值和最大值分別等於minItems和maxItems。 僅支援同質陣列。 所以專案限制必須是物件，而不是陣列。<br /> </td>
  </tr>
 </tbody>
</table>

### 通用結構描述屬性 {#common-schema-properties}

最適化表單會使用JSON結構描述中可用的資訊來對應每個產生的欄位。 尤其是：

* `title`屬性做為最適化表單元件的標籤。
* `description`屬性已設定為最適化表單元件的完整說明。
* `default`屬性做為最適化表單欄位的初始值。
* `maxLength`屬性設定為文字欄位元件的`maxlength`屬性。
* `minimum`、`maximum`、`exclusiveMinimum`和`exclusiveMaximum`屬性用於數值方塊元件。
* 若要支援`DatePicker component`範圍，已提供其他JSON結構描述屬性`minDate`和`maxDate`。
* `minItems`和`maxItems`屬性是用來限制可從面板元件新增或移除的專案/欄位數目。
* `readOnly`屬性設定最適化表單元件的`readonly`屬性。
* `required`屬性將最適化表單欄位標籤為必要，但在面板（其中型別為物件）中，最終提交的JSON資料具有的欄位具有與該物件對應的空白值。
* `pattern`屬性設定為最適化表單中的驗證模式（規則運算式）。
* JSON結構描述檔案的副檔名必須保留為.schema.json。 例如，&lt;filename>.schema.json。

## 範例JSON結構描述 {#sample-json-schema}

>[!BEGINTABS]

>[!TAB JSON結構描述v4]

```json
  {
  "$schema": "https://json-schema.org/draft-04/schema#",
  "definitions": {
    "employee": {
    "type": "object",
    "properties": {
      "userName": {
       "type": "string"
     },
      "dateOfBirth": {
       "type": "string",
       "format": "date"
      },
      "email": {
      "type": "string",
      "format": "email"
      },
      "language": {
       "type": "string"
     },
      "personalDetails": {
       "$ref": "#/definitions/personalDetails"
     },
      "projectDetails": {
       "$ref": "#/definitions/projectDetails"
      }
    },
    "required": [
     "userName",
     "dateOfBirth",
     "language"
    ]
    },
      "personalDetails": {
     "type": "object",
    "properties": {
       "GeneralDetails": {
      "$ref": "#/definitions/GeneralDetails"
     },
      "Family": {
       "$ref": "#/definitions/Family"
      },
      "Income": {
       "$ref": "#/definitions/Income"
     }
     }
       },
    "projectDetails": {
     "type": "array",
     "items": {
     "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```


>[!TAB JSON結構描述2012-20]


```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/employee.schema.json",
  "$defs": {
    "employee": {
      "type": "object",
      "properties": {
        "userName": {
          "type": "string"
        },
        "dateOfBirth": {
          "type": "string",
          "format": "date"
        },
        "email": {
          "type": "string",
          "format": "email"
        },
        "language": {
          "type": "string"
        },
        "personalDetails": {
          "$ref": "#/$defs/personalDetails"
        },
        "projectDetails": {
          "$ref": "#/$defs/projectDetails"
        }
      },
      "required": [
        "userName",
        "dateOfBirth",
        "language"
      ]
    },
    "personalDetails": {
      "type": "object",
      "properties": {
        "GeneralDetails": {
          "$ref": "#/$defs/GeneralDetails"
        },
        "Family": {
          "$ref": "#/$defs/Family"
        },
        "Income": {
          "$ref": "#/$defs/Income"
        }
      }
    },
    "projectDetails": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projects": {
            "$ref": "#/$defs/projects"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projects": {
      "type": "array",
      "items": {
        "properties": {
          "name": {
            "type": "string"
          },
          "age": {
            "type": "number"
          },
          "projectsAdditional": {
            "$ref": "#/$defs/projectsAdditional"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "projectsAdditional": {
      "type": "array",
      "items": {
        "properties": {
          "Additional_name": {
            "type": "string"
          },
          "Additional_areacode": {
            "type": "number"
          }
        }
      },
      "minItems": 1,
      "maxItems": 4
    },
    "GeneralDetails": {
      "type": "object",
      "properties": {
        "age": {
          "type": "number"
        },
        "married": {
          "type": "boolean"
        },
        "phone": {
          "type": "number",
        },
        "address": {
          "type": "string"
        }
      }
      }
  }
  }
```

>[!ENDTABS]

從JSON結構描述V4到2020-12版本規範的主要變更為：

* ID宣告為`$id`
* 定義宣告為`$defs`

### 可重複使用的結構描述定義 {#reusable-schema-definitions}

定義索引鍵是用來識別可重複使用的結構描述。 可重複使用的結構描述定義用於建立片段。 <!-- It is similar to identifying complex types in XSD.-->具有定義的範例JSON結構描述如下：

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上述範例會定義客戶記錄，其中每個客戶都有送貨和帳單地址。 兩個地址的結構相同（地址有街道地址、城市和州/省），因此最好不要重複這些地址。 它也會讓您日後在變更欄位時輕鬆新增和刪除欄位。

<!--
## Pre-Configuring fields in JSON Schema Definition {#pre-configuring-fields-in-json-schema-definition}

You can use the **aem:afProperties** property to preconfigure JSON Schema field to map to a custom Adaptive Form component. An example is listed below:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}

```
-->

<!-- 
## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Stepper</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Radio Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telephone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Switch</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Check Box</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Drop-down</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Image Choice</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Date Input Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Date Picker</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>File Attachment</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

```json

"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}

```
-->

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至JSON結構元素，以限制最適化表單核心元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 結構描述屬性</strong></p> </td>
   <td><p><strong>資料類型</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>元件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的上限。 預設會包含最大值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器<br /> </li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定數值和日期的下限。 預設會包含最小值。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須小於為maximum屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須小於或等於為maximum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布林值</p> </td>
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於針對minimum屬性指定的數值或日期。</p> <p>若為false，則表單元件中指定的數值或日期必須大於或等於針對minimum屬性指定的數值或日期。</p> </td>
   <td>
    <ul>
     <li>數值方塊</li>
     <li>數值步進器</li>
     <li>日期挑選器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定元件中允許的最小字元數。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>字串</td>
   <td>指定元件中允許的最大字元數。 最大長度必須等於或大於零。</td>
   <td>
    <ul>
     <li>文字方塊</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字串</p> </td>
   <td><p>指定字元順序。 如果字元符合指定的模式，元件會接受字元。</p> <p>pattern屬性對應至對應的最適化表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>所有對應至XSD結構描述的最適化Forms元件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>字串</td>
   <td>指定陣列中專案的最大數量。 最大專案數必須等於或大於零。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>字串</td>
   <td>指定陣列中專案的最小數目。 最小專案數必須等於或大於零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>


## 啟用符合結構描述的資料 {#enablig-schema-compliant-data}

若要讓所有JSON結構描述型最適化Forms在表單提交時產生結構描述相容的資料，請遵循下列步驟：

1. 前往`https://server:host/system/console/configMgr`的Experience Manager Web主控台。
1. 找到&#x200B;**[!UICONTROL 最適化表單與互動式通訊Web通道組態]**。
1. 選取以在編輯模式中開啟設定。
1. 選取&#x200B;**[!UICONTROL 產生符合結構描述的資料]**&#x200B;核取方塊。
1. 儲存設定。

![最適化表單與互動式通訊Web通道組態](/help/forms/assets/af-ic-web-channel-configuration.png)


## 不支援的建構  {#non-supported-constructs}

最適化Forms不支援下列JSON結構描述：

* Null型別
* 等位型別，例如any和
* OneOf、AnyOf、AllOf及NOT
* 僅支援同質陣列。 因此，專案限制必須是物件，而不是陣列。
* $ref中的URI參考

## 常見問題 {#frequently-asked-questions}

**為什麼我無法為可重複的子表單（minOccours或maxOccurs值大於1）拖曳子表單的個別元素（由任何複雜型別產生的結構）？**

在可重複的子表單中，您必須使用完整的子表單。 如果您只想使用選擇性欄位，請使用整個結構並刪除不需要的結構。

**我在內容尋找器中有長而複雜的結構。 如何找到特定專案？**

您有兩個選項：

* 捲動瀏覽樹狀結構
* 使用搜尋方塊來尋找元素

**什麼應該是JSON結構描述檔案的副檔名？**

JSON結構描述檔案的副檔名必須是.schema.json。 例如，&lt;filename>.schema.json。

**在基於核心元件的最適化Forms中，是否支援`aem:afProperties`作為JSON結構描述的一部分？**

否，核心元件不支援`aem:afProperties`。 此屬性僅支援用於基礎元件。

## 另請參閱 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Design XML Schema for an Adaptive Form](/help/forms/adaptive-form-xml-schema-form-model.md)

-->
