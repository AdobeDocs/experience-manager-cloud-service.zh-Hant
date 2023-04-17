---
title: 如何建立最適化表單？
description: 了解如何使用 [!DNL Experience Manager Forms]. 適用性Forms是回應式HTML5表單，可簡化資訊收集和處理。 進一步了解如何根據表單資料模型和XML或JSON結構建立最適化表單。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: a4fd268cb143c1356de3db9d55b16ccb58b67d4b
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---


# 建立最適化表單（核心元件） {#creating-an-adaptive-form-core-components}

適用性Forms可讓您建立吸引人、回應式、動態且最適化的表單。 AEM Forms提供商務使用者易記精靈，可快速建立最適化Forms。 精靈提供快速的索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。

開始之前，請先了解可用的Forms元件類型：

* [適用性Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant):這些是標準化的資料捕獲元件。 這些元件為您的數位註冊體驗提供自訂功能、縮短開發時間並降低維護成本。 開發人員可輕鬆自訂和設定這些元件的樣式。 Adobe建議運用這些現代且可擴充的元件來開發最適化Forms。

* [適用性Forms Foundation元件](creating-adaptive-form.md):這些是傳統（舊）資料捕獲元件。 您可以繼續使用這些元件來編輯現有的基礎元件（以最適化表單為基礎）。 如果您要建立新表單，Adobe建議使用  [適用性Forms核心元件](creating-adaptive-form-core-components.md) 來建立適用性Forms。

![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)


## 先決條件

您需要下列項目才能建立最適化表單：

* **為您的環境啟用適用性Forms核心元件**:建立新方案時，您的環境已啟用適用性Forms核心元件。 如果您有以原型39或更舊版本為基礎的Formsas a Cloud Service環境， [為您的環境啟用適用性Forms核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 若要為您的環境啟用核心元件，請 **適用性Forms（核心元件）** 範本和畫布主題會新增至您的環境。 如果您的AEM SDK版本早於2023.02.0, [確保您 `prerelease` 在您的環境中啟用標幟](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) 因為最適化Forms核心元件是2023.02.0版之前的預先發行。

* **最適化表單範本**:範本提供基本結構並定義最適化表單的外觀（配置和樣式）。 它具有包含特定屬性和內容結構的預格式化元件。 它還提供定義主題和提交動作的選項。 主題定義外觀和風格，並定義提交動作，以便在提交最適化表單時採取動作。 例如，將收集的資料傳送至資料來源。 雲端服務提供OOTB範本，命名為空白：

   * 此 `blank` 每個全新AEM Formsas a Cloud Service計畫都包含範本。
   * 您可以透過套件管理器安裝參考套件，以新增 `blank` 範本至AEM Formsas a Cloud Service計畫。
   * 您也可以 [建立新的適用性Forms範本（核心元件）](template-editor.md) 白手起家。

* **最適化表單主題**:主題包含元件和面板的樣式詳細資料。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 應用主題時，指定的樣式會反映在相應的元件上。  此 `Canvas` 每個全新AEM Formsas a Cloud Service計畫都包含範本。

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **權限**:將使用者新增至 [!DNL forms-users] 群組。 成員 [!DNL forms-users] 群組擁有建立最適化表單的權限。 如需特定使用者群組的表單詳細清單，請參閱 [群組和權限](forms-groups-privileges-tasks.md).


## 建立最適化表單（核心元件） {#create-an-adaptive-form-core-components}

1. 登入 [!DNL Experience Manager Forms] 製作例項。 可以是雲端例項或本機開發例項。

1. 在Experience Manager登入頁面上輸入您的憑證。 登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]**  > **[!UICONTROL 適用性Forms]**. 精靈隨即開啟。 在源頁簽中，選擇模板：

   ![核心元件範本](/help/forms/assets/core-components-template.png)

   選取範本時，會自動選取範本中指定的主題和提交動作，並 **[!UICONTROL 建立]** 按鈕。 您可以前往 **[!UICONTROL 樣式]** 或 **[!UICONTROL 提交]** 頁簽，以選擇不同的主題或提交操作。 如果所選模板未指定主題，則建立按鈕將保持禁用狀態。 您可以前往 **[!UICONTROL 樣式]** 頁簽，手動選擇主題。

   >[!NOTE]
   >
   >
   > 如果你沒有， **適用性Forms（核心元件）** 範本， [為您的環境啟用適用性Forms核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). 若要為您的環境啟用核心元件，請 **適用性Forms（核心元件）** 範本已新增至您的環境。

1. 在 **[!UICONTROL 樣式]** 頁簽，選擇主題：

   * 當所選模板指定主題時，該主題將在嚮導中自動選中。 您也可以從「樣式」索引標籤中選擇不同的主題。

   * 如果所選模板未指定主題，則可以使用「樣式」頁簽選擇主題。 此 **[!UICONTROL 建立]** 按鈕僅在選取主題後啟用。

1. （可選）在「資料」索引標籤中，選取資料模型：

   * **表單資料模型**:A [表單資料模型](data-integration.md) 可讓您將不同資料來源的實體和服務整合至最適化表單。 如果您建立的適用性表單涉及從多個資料來源擷取資料並將其寫入多個資料來源，請選擇「表單資料模型」。

   * **JSON結構**: [JSON結構](adaptive-form-json-schema-form-model.md) 我們以核心元件為基礎的適用性表單能提供關聯JSON結構（代表所產生或使用的資料結構）的功能，與貴組織的後端系統順暢整合。 此關聯可讓作者使用結構的元素，以動態方式將內容新增至最適化表單。 在製作過程中，可在內容瀏覽器的「資料模型對象」頁簽中輕鬆訪問架構的元素，所有欄位都會自動添加到任何新建的適用性表單中。

   依預設，會自動選取相關JSON結構描述的所有欄位，並轉換為對應的最適化表單元件，簡化製作程式。 精靈提供額外的便利，可讓您透過使用核取方塊，選擇性地選擇應包含在適用性表單中的欄位。

1. 在 **[!UICONTROL 提交]** 頁簽，選擇提交操作：

   * 選取範本時，會自動選取範本中指定的提交動作。 您可以從「提交」頁簽中選擇不同的提交操作。 此 **[!UICONTROL 提交]** 標籤顯示所有可用的提交操作。

   * 當選取的範本未指定提交動作時，您可以使用 **[!UICONTROL 提交]** 頁簽以選擇提交操作

1. （選用）在 **[!UICONTROL 傳送]** 索引標籤，您可以指定「適用性表單」的發佈或取消發佈日期。

1. 點選 **[!UICONTROL 建立]**. 此時會出現一個對話方塊，用於指定標題、名稱和儲存最適化表單的位置：

   * **[!UICONTROL 標題]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 路徑：]** 指定最適化表單的儲存位置。 您可以直接在 `/content/dam/formsanddocuments` 或建立資料夾，例如 `/content/dam/formsanddocuments/adaptiveforms` 以儲存最適化表單。 在路徑中使用資料夾之前，請確定已建立該資料夾。 此 **[!UICONTROL 路徑]** 欄位不會自動建立資料夾。

1. 點選 **[!UICONTROL 建立]**. 適用性表單會建立並在適用性Forms編輯器中開啟。 編輯器會顯示範本中的可用內容。  根據最適化表單的類型，關聯 <!--XFA form template, XML schema or --> JSON結構描述或表單資料模型會顯示在 **[!UICONTROL 資料模型物件]** 的 **[!UICONTROL 內容瀏覽器]** 欄。 您也可以拖放這些元素來建立最適化表單。

現在，您可以拖放適用性Forms核心元件至適用性Forms容器，以設計和建立表單。

## 可用適用性Forms核心元件

適用性Forms核心元件是標準化的資料擷取元件。 這些元件提供自訂功能，有助於縮短開發時間，並降低數位註冊體驗的維護成本。 [適用性Forms核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant) 有詳細的可用元件清單，以及每個元件功能的詳細資訊。 您也可以造訪 [https://aemcomponents.dev/](https://aemcomponents.dev/) 檢視可用的核心元件。

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

1. 選取「最適化表單」並點選 ![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 開啟屬性]**. 「表單屬性」頁面隨即開啟。

1. 前往 **[!UICONTROL 表單模型]** 頁簽，然後選擇表單模型。 如果適用性表單沒有表單模型，您可以自由選擇JSON結構描述或表單資料模型。 另一方面，如果適用性表單已基於表單模型，則您可以選擇切換至相同類型的其他表單模型。 例如，如果表單使用JSON結構，您可以輕鬆切換至其他JSON結構，同樣地，如果表單使用表單資料模型，您也可以切換至其他表單資料模型。

1. 點選 **[!UICONTROL 儲存]** 以儲存屬性。
