---
title: 如何建立自適應窗體
description: 瞭解如何使用 [!DNL Experience Manager Forms]。 自適應Forms是可以簡化資訊收集和處理的響應性HTML5表。 更深入地瞭解如何基於表單資料模型和XML或JSON架構建立自適應表單。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 1%

---

# 建立自適應窗體（核心元件） {#creating-an-adaptive-form-core-components}

自適應Forms讓你建立具有吸引力、響應性、動態性和適應性的表單。 AEM Forms提供了業務用戶友好嚮導，可快速建立自適應Forms。 該嚮導具有快速頁籤導航功能，可以輕鬆選擇預配置的模板、樣式、欄位和提交選項以建立自適應表單。

在開始之前，請瞭解可供您使用的Forms元件類型：

* [自適應Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant):這些是標準化的資料捕獲元件。 這些元件為您的數字註冊體驗提供了定制功能、縮短了開發時間並降低了維護成本。 開發人員可以輕鬆定制和設計這些元件。 Adobe建議利用這些現代和可擴展的元件開發自適應Forms。

* [自適應Forms基金會元件](creating-adaptive-form.md):這些是經典（舊）資料捕獲元件。 您可以繼續使用這些元件來編輯基於自適應表單的現有基礎元件。 如果要建立新表單，Adobe建議使用  [自適應Forms核心元件](creating-adaptive-form-core-components.md) 建立自適應Forms。

![用於建立自適應表單的嚮導](/help/release-notes/assets/wizard.png)


## 先決條件

您需要使用以下命令建立「自適應表單」：

* **為您的環境啟用自適應Forms核心元件**:建立新程式時，已為您的環境啟用了自適應Forms核心元件。 如果你有一個基於原型39或更早的Formsas a Cloud Service環境， [為您的環境啟用自適應Forms核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。 在為您的環境啟用核心元件時， **自適應Forms（核心元件）** 模板和畫布主題將添加到您的環境中。 如果AEMSDK版本早於2023.02.0, [確保 `prerelease` 在您的環境中啟用的標誌](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) 因為自適應Forms核心元件是發佈前預租2023.02.0的一部分。

* **自適應表單模板**:模板提供基本結構並定義自適應表單的外觀（佈局和樣式）。 它具有預格式化的元件，包含某些屬性和內容結構。 它還提供了定義主題和提交操作的選項。 該主題定義外觀和提交操作，並定義在提交自適應表單時要採取的操作。 例如，將收集的資料發送到資料源。 雲服務提供OOTB模板，名為blank:

   * 的 `blank` 模板包含在每個新的AEM Formsas a Cloud Service計畫中。
   * 可以通過包管理器安裝引用包，以添加 `blank` 模板到您的AEM Formsas a Cloud Service程式。
   * 您也可以 [建立新的自適應Forms模板（核心元件）](template-editor.md) 從頭開始。

* **自適應窗體主題**:主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。  的 `Canvas` 模板包含在每個新的AEM Formsas a Cloud Service計畫中。

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **權限**:將用戶添加到 [!DNL forms-users] 組。 成員 [!DNL forms-users] 組具有建立自適應表單的權限。 有關特定用戶組的表單的詳細清單，請參見 [組和權限](forms-groups-privileges-tasks.md)。


## 建立自適應窗體（核心元件） {#create-an-adaptive-form-core-components}

1. 登錄到 [!DNL Experience Manager Forms] 作者實例。 它可以是雲實例或本地開發實例。

1. 在Experience Manager登錄頁上輸入憑據。 登錄後，在左上角，點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。

1. 點擊 **[!UICONTROL 建立]**  > **[!UICONTROL 自適應Forms]**。 將開啟嚮導。 在「源」頁籤中，選擇模板：

   ![核心元件模板](/help/forms/assets/core-components-template.png)

   選擇模板時，將自動選擇模板中指定的主題和提交操作， **[!UICONTROL 建立]** 按鈕。 您可以 **[!UICONTROL 樣式]** 或 **[!UICONTROL 提交]** 頁籤，以選擇其他主題或提交操作。 如果所選模板未指定主題，則「建立」按鈕仍處於禁用狀態。 您可以 **[!UICONTROL 樣式]** 的子菜單。

   >[!NOTE]
   >
   >
   > 如果你沒有， **自適應Forms（核心元件）** 在您的環境中， [為您的環境啟用自適應Forms核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。 在為您的環境啟用核心元件時， **自適應Forms（核心元件）** 模板將添加到您的環境中。

1. 在 **[!UICONTROL 樣式]** 頁籤，選擇主題：

   * 當所選模板指定主題時，將在嚮導中自動選擇主題。 您也可以從「樣式」頁籤中選擇其他主題。

   * 如果所選模板未指定主題，則可以使用「樣式」頁籤選擇主題。 的 **[!UICONTROL 建立]** 選項。

1. （可選）在「資料」頁籤中，選擇一個資料模型：

   * **窗體資料模型**:A [窗體資料模型](data-integration.md) 允許您將不同資料源中的實體和服務整合到自適應表單。 如果要建立的自適應表單涉及從多個資料源讀取和寫入資料，請選擇「表單資料模型」。

   * **JSON架構**: [JSON架構](adaptive-form-json-schema-form-model.md) 我們基於核心元件的自適應表單通過提供關聯JSON架構（表示正在生成或使用的資料的結構）的能力，允許與組織的後端系統無縫整合。 此關聯使作者能夠使用模式的元素動態地將內容添加到自適應表單。 在創作過程中，可以在內容瀏覽器的「資料模型對象」頁籤中輕鬆訪問架構的元素，並且所有欄位都會自動添加到任何新建立的自適應表單中。

   預設情況下，關聯的JSON架構的所有欄位都會自動選擇並轉換為相應的Adaptive Form元件，從而簡化創作過程。 該嚮導提供了額外的便利性，允許您通過使用複選框有選擇地選擇應包括在自適應表單中的欄位。

1. 在 **[!UICONTROL 提交]** 頁籤，選擇提交操作：

   * 選擇模板時，將自動選擇在模板中指定的提交操作。 您可以從「提交」標籤中選擇其他提交操作。 的 **[!UICONTROL 提交]** 頁籤顯示所有可用的提交操作。

   * 當所選模板未指定提交操作時，您可以使用 **[!UICONTROL 提交]** 頁籤以選擇提交操作

1. （可選）在 **[!UICONTROL 交貨]** 頁籤中，您可以為自適應表單指定發佈或取消發佈日期。

1. 點擊 **[!UICONTROL 建立]**。 此時將顯示一個對話框，用於指定保存「自適應表單」的標題、名稱和位置：

   * **[!UICONTROL 標題]** 指定窗體的顯示名稱。 標題可幫助您在 [!DNL Experience Manager Forms] 用戶介面。
   * **[!UICONTROL 名稱：]** 指定窗體的名稱。 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。
   * **[!UICONTROL 路徑：]** 指定保存自適應表單的位置。 您可以直接在以下位置保存自適應表單 `/content/dam/formsanddocuments` 或建立資料夾，如 `/content/dam/formsanddocuments/adaptiveforms` 的子菜單。 確保在路徑中使用資料夾之前先建立該資料夾。 的 **[!UICONTROL 路徑]** 欄位不會自動建立資料夾。

1. 點擊 **[!UICONTROL 建立]**。 將建立一個自適應表單，並在自適應Forms編輯器中開啟。 編輯器顯示模板中的可用內容。  根據「自適應表單」的類型，在關聯的 <!--XFA form template, XML schema or --> JSON架構或表單資料模型顯示在 **[!UICONTROL 資料模型對象]** 頁籤 **[!UICONTROL 內容瀏覽器]** 欄。 也可以拖放這些元素來構建自適應表單。

現在，您可以將自適應Forms核心元件拖放到自適應Forms容器中，以設計和建立表單。

## 可用的自適應Forms核心元件

自適應Forms核心元件是標準化的資料捕獲元件。 這些元件提供定制功能，幫助縮短開發時間，並降低數字註冊體驗的維護成本。 [自適應Forms核心元件文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant) 包含可用元件的詳細清單以及有關每個元件功能的詳細資訊。 您還可以 [https://aemcomponents.dev/](https://aemcomponents.dev/) 查看可用的核心元件。

## 編輯自適應表單的表單模型屬性 {#edit-form-model}

1. 選擇「自適應表單」並點擊 ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 開啟屬性]**。 將開啟「表單屬性」頁。

1. 轉到 **[!UICONTROL 窗體模型]** 的子菜單。 如果自適應表單沒有表單模型，則您可以自由選擇JSON模式或表單資料模型。 另一方面，如果「自適應表單」已基於表單模型，則可以選擇切換到同一類型的另一個表單模型。 例如，如果表單使用JSON架構，則可以輕鬆切換到另一個JSON架構，同樣，如果表單使用表單資料模型，則可以切換到另一個表單資料模型。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。
