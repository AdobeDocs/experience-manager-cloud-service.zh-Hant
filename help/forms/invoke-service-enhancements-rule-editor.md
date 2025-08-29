---
title: 針對以核心元件為基礎的表單，Invoke service VRE有哪些增強功能？
description: 增強規則編輯器的Invoke服務
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: 在VRE中叫用服務增強功能，使用叫用服務填入下拉式選項，使用叫用服務的輸出設定可重複面板，使用叫用服務的輸出設定面板，使用叫用服務的輸出引數驗證其他欄位。
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 4aecf84672ea60ad9688a974330a62be0a5fde86
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 1%

---

# 針對以核心元件為基礎的表單，在視覺化規則編輯器中使用叫用服務

最適化表單中的視覺化規則編輯器支援&#x200B;**叫用服務**&#x200B;功能，可讓您從針對執行個體設定的表單資料模型(FDM)清單中選取服務。 您可以將表單欄位直接對應到服務的輸入引數。 若要將表單欄位對應到輸出引數，請使用指定表單資料模型服務的事件裝載選項。 此外，視覺化規則編輯器可讓您根據輸出回應，為&#x200B;**Invoke Service**&#x200B;作業建立成功和失敗處理常式的規則。 成功處理常式管理&#x200B;**啟動服務**&#x200B;作業的成功執行，而失敗處理常式處理所有發生的錯誤。

## 在表單的規則編輯器中使用「叫用服務」的優勢

在自適應表單的規則編輯器中使用「叫用服務」作業的優點如下：

* **簡化整合**：視覺規則編輯器簡化了將外部服務或API整合至最適化Forms的程式。 透過&#x200B;**啟動服務**，您可以輕鬆地將表單連線到各種資料來源和服務，而不需要複雜的程式碼，讓表單整合更有效率。

* **動態回應處理**：您可以根據&#x200B;**叫用服務**&#x200B;的輸出回應來管理成功和錯誤回應，讓表單能夠動態回應不同的情境。 它可確保表單適當地處理各種條件，提高彈性和控制能力。

* **增強的使用者互動**：在規則編輯器中使用&#x200B;**Invoke Service**&#x200B;可啟用表單中的即時驗證，提供更佳的使用者體驗。 此外，還可確保資料在伺服器端通過精確驗證，減少錯誤並提升表單可靠性。

## 啟動服務處理常式以取得成功和失敗回應

>[!NOTE]
>
> 您只能對以核心元件為基礎的表單使用&#x200B;**啟動服務**&#x200B;成功和失敗處理常式。 以基礎元件為基礎的Forms不支援&#x200B;**叫用服務**&#x200B;成功和失敗處理常式。

視覺化規則編輯器可讓您根據輸出回應，為&#x200B;**Invoke Service**&#x200B;作業建立成功和失敗處理常式的規則。 下圖描繪了最適化表單的視覺化規則編輯器中的&#x200B;**叫用服務**：

![啟動服務處理常式](/help/forms/assets/invoke-service-rule-editor.png)

若要新增成功或失敗處理常式，請分別按一下&#x200B;**[!UICONTROL 新增成功處理常式]**&#x200B;或&#x200B;**[!UICONTROL 新增失敗處理常式]**。

當您按一下&#x200B;**[!UICONTROL 新增成功處理常式]**&#x200B;時，會出現&#x200B;**[!UICONTROL 叫用服務成功處理常式]**&#x200B;規則編輯器，可讓您指定規則或邏輯，在作業成功時管理&#x200B;**叫用服務**&#x200B;輸出回應。 即使不定義條件，您也可以指定規則；不過，您可以按一下&#x200B;**[!UICONTROL 新增條件]**&#x200B;選項，為成功處理常式新增條件。

![啟動服務成功處理程式](/help/forms/assets/invoke-service-success-handler.png)

您可以新增多個規則來處理&#x200B;**啟動服務**&#x200B;作業的成功回應：

![多個成功處理常式](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

同樣地，您可以新增規則，以便在作業失敗時處理&#x200B;**叫用服務**&#x200B;輸出回應。 下圖顯示&#x200B;**[!UICONTROL 啟動服務失敗處理常式]**&#x200B;規則編輯器：

![啟動服務失敗處理常式](/help/forms/assets/invoke-service-failue-handler.png)

您也可以新增多個規則來處理來自&#x200B;**叫用服務**&#x200B;作業的不成功回應。

伺服器&#x200B;**上的**&#x200B;啟用錯誤驗證功能允許作者在設計要在伺服器上執行的Adaptive Form時新增驗證。

## 在規則編輯器中使用叫用服務的先決條件

在規則編輯器中使用&#x200B;**叫用服務**&#x200B;之前，您必須滿足下列必要條件：

* 請確定您已設定資料來源。 如需設定資料來源的指示，[請按一下這裡](/help/forms/configure-data-sources.md)。
* 使用已設定的資料來源建立表單資料模型。 如需建立表單資料模型的相關指引，[請按一下這裡](/help/forms/create-form-data-models.md)。
* 確認您的環境已啟用核心元件。 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。

## 透過不同的使用案例探索啟動服務

視覺規則編輯器的&#x200B;**Invoke Service**&#x200B;可讓您執行數個有用的作業。 您可以使用它來填入下拉式清單選項、設定可重複或簡單的面板，以及驗證表單欄位，全都依據&#x200B;**叫用服務**&#x200B;的輸出回應。 因此，可增強表單的彈性和互動性。

下表說明幾個可使用&#x200B;**叫用服務**&#x200B;的情況：

| **使用案例** | **說明** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **使用叫用服務的輸出填入下拉式清單選項** | 會根據從叫用服務輸出擷取的資料，動態填入下拉式清單選項。 [按一下這裡](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service)，檢視實作。 |
| **使用Invoke Service的輸出設定可重複的面板** | 使用叫用服務輸出的資料來設定可重複的面板，允許動態面板。 [按一下這裡](#use-case-2-set-repeatable-panel-using-output-of-invoke-service)，檢視實作。 |
| **使用Invoke Service的輸出設定面板** | 使用叫用服務輸出中的特定值來設定面板的內容或可見度。 [按一下這裡](#use-case-3-set-panel-using-output-of-invoke-service)，檢視實作。 |
| **使用叫用服務的輸出引數來驗證其他欄位** | 使用來自叫用服務的特定輸出引數來驗證表單欄位。 [按一下這裡](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields)，檢視實作。 |

建立根據`Get Information`文字方塊中輸入之輸入擷取值的`Pet ID`表單。 底下熒幕擷圖顯示以下使用案例中所使用的表單：

![取得資訊表單](/help/forms/assets/get-information-form.png)

**表單欄位**

新增下列欄位至表單：
* **輸入Pet ID**： Textbox
* **選取像片URL**：下拉式清單
* **標籤**：面板
   * 名稱：文字方塊
   * ID：文字方塊
* **類別**：面板
   * 名稱：文字方塊
* **提交**：提交按鈕

>[!NOTE]
>
> 在表單欄位的&#x200B;**屬性**&#x200B;對話方塊中的&#x200B;**繫結參考**&#x200B;欄位中，選取![foldersearch_18](assets/folder-search-icon.svg)，並導覽以選取您在表單資料模型(FDM)中新增的二進位屬性。

**設定面板**

將面板設定為具有下列限制的重複面板：
* 最小值： 1
* 最大值： 4

您可以調整重複式面板的值，以符合您的需求。

**資料來源**

在此範例中，[Swagger Petstore](https://petstore.swagger.io/) API是用來設定資料來源。 已針對[getPetById](/help/forms/create-form-data-models.md)服務設定[表單資料模型](https://petstore.swagger.io/#/pet/getPetById)，該服務會根據輸入的ID擷取pet詳細資料。

讓我們使用[Swagger Petstore](https://petstore.swagger.io/#/pet/addPet) API中的[addPet](https://petstore.swagger.io/)服務發佈下列JSON：

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```


規則和邏輯是使用&#x200B;**文字方塊上的規則編輯器中的**&#x200B;叫用服務`Pet ID`動作實作，以示範提及的使用案例。

現在，讓我們詳細探討每個使用案例的實作。

### 使用案例1：使用叫用服務的輸出填入下拉式清單值

此使用案例示範如何根據`Invoke Service`的輸出動態填入下拉式選項。

#### 實施

若要達成此目的，請在`Pet ID`文字方塊上建立規則以叫用`getPetById`服務。 在規則中，將`enum`新增成功處理常式`photo-url`中`photoUrls`下拉式清單的&#x200B;**[!UICONTROL 屬性設定為]**。

![設定下拉式清單值](/help/forms/assets/set-dropdownoption.png)

#### 輸出

在`101`文字方塊中輸入`Pet ID`，以根據輸入的值動態填入下拉式清單選項。

![結果](/help/forms/assets/output1.png)

### 使用案例2：使用叫用服務的輸出設定可重複面板

此使用案例示範如何根據&#x200B;**叫用服務**&#x200B;的輸出動態填入可重複面板。

#### 考量事項

* 確定可重複面板的名稱符合您要為其設定面板的&#x200B;**Invoke Service**&#x200B;的引數。
* 面板會針對對應的&#x200B;**Invoke Service**&#x200B;欄位傳回的值數重複執行。

#### 實施

在`Pet ID`文字方塊上建立規則以叫用`getPetById`服務。 在&#x200B;**[!UICONTROL 新增成功處理常式]**&#x200B;中，新增另一個成功處理常式回應。 在規則中將`tags`面板的值設定為`tags`。

![建立可重複面板的規則](/help/forms/assets/create-rule-repeatable-panel.png)

#### 輸出

在`101`文字方塊中輸入`Pet ID`，以根據輸入值動態填入可重複面板。

![輸出](/help/forms/assets/output2.png)

### 使用案例3：使用叫用服務的輸出設定面板

此使用案例示範如何根據&#x200B;**啟動服務**&#x200B;的輸出動態設定面板的值。

#### 考量事項

* 確定面板的名稱符合您要設定面板的&#x200B;**啟動服務**&#x200B;的引數。
* 面板會針對對應的「啟動服務」欄位傳回的值數重複執行。

#### 實施

在`Pet ID`文字方塊上建立規則以叫用`getPetById`服務。 在&#x200B;**[!UICONTROL 新增成功處理常式]**&#x200B;中，新增另一個成功處理常式回應。 在規則中將`categoryname`文字方塊的值設定為`category.name`。

![建立可重複面板的規則](/help/forms/assets/set-panel-values.png)

#### 輸出

在`101`文字方塊中輸入`Pet ID`，以根據輸入值動態填入面板。

![輸出](/help/forms/assets/output3.png)

### 使用案例4：使用叫用服務的輸出引數來驗證其他欄位

此使用案例示範如何使用&#x200B;**叫用服務**&#x200B;的輸出來動態驗證其他表單欄位。

#### 實施

在`Pet ID`文字方塊上建立規則以叫用`getPetById`服務。 在&#x200B;**[!UICONTROL 新增失敗處理常式]**&#x200B;中，新增失敗處理常式回應。 如果輸入的&#x200B;**不正確，請隱藏**&#x200B;提交`Pet ID`按鈕。

![失敗處理常式](/help/forms/assets/create-rule-failure-handler.png)

#### 輸出

在`102`文字方塊中輸入`Pet ID`，並隱藏&#x200B;**提交**&#x200B;按鈕。

![輸出](/help/forms/assets/output4.png)

>[!NOTE]
>
> 您也可以[直接在規則編輯器介面中整合API](/help/forms/api-integration-in-rule-editor.md)，而不使用預先定義的表單資料模型。

## 常見問題

**問：如果我使用Invoke Service建立規則，然後升級至核心元件的最新版本，會發生什麼事？**

**A：**&#x200B;當您升級至最新版本的核心元件時，**叫用服務**&#x200B;規則會自動更新至最新的使用者介面，因為它可回溯相容。

**問：我可以新增多個規則來處理Invoke Service作業的成功或失敗回應嗎？**

**A：**&#x200B;是，您可以新增多個規則來處理&#x200B;**啟動服務**&#x200B;作業的成功或失敗回應。

## 相關的文章

* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型(FDM)](create-form-data-models.md)
* [使用表單資料模型(FDM)](work-with-form-data-model.md)
* [使用表單資料模型(FDM)](using-form-data-model.md)


## 其他資源

{{see-also-rule-editor}}
