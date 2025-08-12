---
title: 在最適化表單中建立及新增自訂函式
description: AEM Forms支援自訂函式，可讓使用者在規則編輯器中建立並使用自己的函式。
keywords: 新增自訂函式、使用自訂函式、建立自訂函式，以及在規則編輯器中使用自訂函式。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 5%

---

# 建立以核心元件為主之最適化表單的自訂函數

以核心元件為基礎的最適化Forms會根據使用者輸入調整內容和行為，以提供動態使用者體驗。 自訂函式可讓開發人員擴充功能，確保表單符合特定需求。 透過整合自訂函式，開發人員可以實作複雜的邏輯、自動化流程，並匯入符合特定業務需求或使用者期望的獨特互動。 這可確保表單不僅適應各種條件，還可為各種使用案例提供更精確有效的解決方案。
本文會逐步引導您使用核心元件，針對Adaptive Forms建立自訂函式。

## 考量事項

* `parameter type`和`return type`不支援`None`。

* 自訂函式清單中不支援的函式包括：
   * 產生器函式
   * 非同步/等待函式
   * 方法定義
   * 類別方法
   * 預設引數
   * Rest引數

## 建立自訂函式的先決條件

開始將自訂函式新增至最適化Forms之前，請確定您具備下列條件：

**軟體：**

* **純文字編輯器(IDE)**：雖然任何純文字編輯器都可以運作，但Microsoft Visual Studio Code之類的整合式開發環境(IDE)可提供進階功能，讓編輯更輕鬆。

* **Git：**&#x200B;管理程式碼變更需要此版本控制系統。 如果您尚未安裝，請從https://git-scm.com下載。


## 建立自訂函數

建立使用者端程式庫以呼叫規則編輯器中的自訂函式。 如需詳細資訊，請參閱[使用使用者端資料庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=zh-Hant#developing)。

建立自訂函式的步驟如下：

1. [建立使用者端資源庫](#create-client-library)
1. [將使用者端程式庫新增至最適化表單](#use-custom-function)

### 建立使用者端資源庫 {#create-client-library}

您可以透過新增使用者端資料庫來新增自訂函式。 若要建立使用者端程式庫，請執行下列步驟：

**複製存放庫**

複製您的[AEM Forms as a Cloud Service存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#accessing-git)：

1. 開啟命令列或終端機視窗。

1. 導覽至您電腦上要儲存存放庫的位置。

1. 執行以下命令以複製存放庫：

   `git clone [Git Repository URL]`

這個命令會下載存放庫並在您的電腦上建立複製存放庫的本機資料夾。 在本指南中，我們將此資料夾稱為[AEMaaCS專案目錄]。

**新增使用者端資料庫資料夾**

若要將新的使用者端程式庫資料夾新增至[AEMaaCS專案目錄]，請遵循下列步驟：

1. 在編輯器中開啟[AEMaaCS專案目錄]。

   ![自訂函式資料夾結構](/help/forms/assets/custom-library-folder-structure.png)

1. 找到`ui.apps`。
1. 新增資料夾。 例如，新增名為`experience-league`的資料夾。
1. 導覽至`/experience-league/`資料夾並新增`ClientLibraryFolder`。 例如，建立名為`customclientlibs`的使用者端資料庫資料夾。

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**新增檔案和資料夾至使用者端資料庫資料夾**

將下列專案新增至新增的使用者端程式庫資料夾：

* .content.xml檔案
* js.txt檔案
* js資料夾

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在`.content.xml`中新增下列幾行程式碼：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以為`client library folder`和`categories`屬性選擇任何名稱。

1. 在`js.txt`中新增下列幾行程式碼：

   ```javascript
         #base=js
       function.js
   ```

1. 在`js`資料夾中，將JavaScript檔案新增為`function.js`，其中包含自訂函式：

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```

1. 儲存檔案。

![自訂函式資料夾結構](/help/forms/assets/custom-function-added-files.png)

**在filter.xml中包含新資料夾**：

1. 導覽至`/ui.apps/src/main/content/META-INF/vault/filter.xml`AEMaaCS專案目錄[中的]檔案。

1. 開啟檔案，並在結尾新增下列行：

   `<filter root="/apps/experience-league" />`
1. 儲存檔案。

![自訂函式篩選器xml](/help/forms/assets/custom-function-filterxml.png)

**將新建立的使用者端資料庫資料夾部署至您的AEM環境**

將AEM as a Cloud Service [AEMaaCS專案目錄]部署至您的Cloud Service環境。 若要部署至您的Cloud Service環境：

1. 提交變更

   1. 使用以下命令在存放庫中新增、提交和推播變更：

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. 部署更新的程式碼：

   1. 透過現有的完整棧疊管道觸發計畫碼部署。 這會自動建置及部署更新的程式碼。

如果您尚未設定管道，請參閱[上的指南以瞭解如何設定AEM Forms as a Cloud Service的管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=zh-Hant#setup-pipeline)。

管道執行成功後，新增到使用者端資料庫中的自訂函式便可在[最適化表單規則編輯器](/help/forms/rule-editor-core-components.md)中使用。

### 將使用者端程式庫新增至最適化表單{#use-custom-function}

將使用者端程式庫部署到Forms CS環境後，請在最適化表單中使用其功能。 若要在最適化表單中新增使用者端程式庫

1. 在編輯模式中開啟您的表單。 若要以編輯模式開啟表單，請選取表單並選取&#x200B;**[!UICONTROL 編輯]**。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤，並從下拉式清單中選取&#x200B;**[!UICONTROL 使用者端程式庫類別]**&#x200B;的名稱（在此案例中選取`customfunctionscategory`）。

   ![正在新增自訂函式使用者端程式庫](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 在&#x200B;**[!UICONTROL 使用者端資料庫類別]**&#x200B;欄位中指定逗號分隔的清單，可新增多個類別。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

您可以使用[JavaScript註解](/help/forms/rule-editor-core-components.md)，在最適化表單[的](##js-annotations)規則編輯器中使用自訂函式。

## 在最適化表單中使用自訂函式

在最適化表單中，您可以在規則編輯器[中使用](/help/forms/rule-editor-core-components.md)自訂函式。 讓我們將下列程式碼新增至JavaScript檔案（`Function.js`檔案），以根據出生日期計算年齡(YYYY-MM-DD)。 建立自訂函式為`calculateAge()`，它以出生日期作為輸入並傳回年齡：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上述範例中，當使用者以(YYYY-MM-DD)格式輸入出生日期時，會叫用自訂函式`calculateAge`並傳回年齡。

![規則編輯器中的Calcualte Agae自訂函式](/help/forms/assets/custom-function-calculate-age.png)

讓我們預覽表單，以觀察如何透過規則編輯器實作自訂函式：

![在規則編輯器表單預覽中計算Agae自訂函式](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以參考下列[自訂函式](/help/forms/assets//customfunctions.zip)資料夾。 使用[封裝管理員](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager)下載此資料夾，並將其安裝在您的AEM執行個體中。

## 自訂函式的功能

AEM表單中的自訂函式為擴充及個人化表單功能提供強大的解決方案。 您可以使用自訂函式來符合您組織的特定需求。

這些函式支援各種功能，包括使用特定欄位、使用全域欄位和非同步操作，以及合併快取機制。 這種靈活性可確保表單能夠適應複雜的需求，並提供有效率、量身打造的使用者體驗。 運用這些進階功能，您可以增強表單互動並最佳化效能，讓您的AEM表單功能更強大，回應速度也更快。

讓我們來探討自訂函式的功能。

### 自訂函式中的非同步支援 {#support-of-async-functions}

您可以使用自訂函式，在規則編輯器中實作非同步函式。 如需如何執行此動作的指引，請參閱文章[在調適型表單中使用非同步函式](/help/forms/using-async-funct-in-rule-editor.md)。

### 自訂函式中支援的欄位和全域範圍物件 {#support-field-and-global-objects}

欄位物件是指表單中的個別元件或元素，例如文字欄位、核取方塊。 全域物件包含唯讀變數，例如表單例項、目標欄位例項，以及在自訂函式內進行表單修改的方法。

>[!NOTE]
>
> `param {scope} globals`必須是最後一個引數，且不會顯示在調適型表單的規則編輯器中。

如需範圍物件的詳細資訊，請參閱自訂函式中的[範圍物件](/help/forms/custom-function-core-component-scope-function.md)文章。

### 自訂函式中的快取支援

Adaptive Forms會在規則編輯器中擷取自訂函式清單時，實作自訂函式的快取，以增強回應時間。 在`Fetched following custom functions list from cache`檔案中會顯示訊息為`error.log`。

具有快取支援的![自訂函式](/help/forms/assets/custom-function-cache-error.png)

如果修改自訂函式，快取會失效，並加以剖析。

## 疑難排解

* 如果包含自訂函式程式碼的JavaScript檔案發生錯誤，則自訂函式不會列在最適化表單的規則編輯器中。 若要檢查自訂函式清單，您可以導覽至`error.log`檔案以找出錯誤。 發生錯誤時，自訂函式清單會顯示為空白：

  ![錯誤記錄檔](/help/forms/assets/custom-function-list-error-file.png)

  如果沒有錯誤，則會擷取自訂函式並出現在`error.log`檔案中。 在`Fetched following custom functions list`檔案中顯示為`error.log`的訊息：

  使用適當的自訂函式![錯誤記錄檔](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 下一步

現在讓我們檢視以核心元件為基礎的最適化表單的各種[自訂函式範例](/help/forms/custom-function-core-components-use-cases.md)。

## 另請參閱

{{see-also-rule-editor}}
