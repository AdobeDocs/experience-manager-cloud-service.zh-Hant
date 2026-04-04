---
title: 使用主題編輯器自訂最適化表單主題
description: 瞭解如何使用主題編輯器，在Adobe Experience Manager中為核心元件型最適化Forms建立和自訂視覺主題。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 4a541c11-38e9-4dbc-8464-38be6b1ee94d
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---

# 自訂表單主題 {#customizing-form-themes}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html) |
| AEM as a Cloud Service  | 本文章 |

Adobe Experience Manager (AEM) Forms中的主題編輯器是一個視覺化介面，可讓您為最適化Forms建立和自訂主題，而無需手動編寫程式碼。 主題定義表單元件和面板的外觀與風格，包括背景顏色、字型樣式、框線、尺寸與間距。 套用主題時，指定的樣式會反映在相對應的元件上，而您可以在多個Adaptive Forms中重複使用相同主題。

主題編輯器不需要專門的開發人員角色來設定基本表單樣式。 只要具備CSS的實用知識，您就能使用視覺側邊欄來設定表單樣式，或直接在編輯器中撰寫進階CSS覆寫。

## 先決條件 {#prerequisites}

* Adobe Experience Manager Forms中的作者層級許可權。
* 基本瞭解CSS樣式原則。 如需完整的CSS參考，請參閱[MDN Web Docs CSS參考](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)。

## 導覽至「佈景主題」目錄 {#navigate-to-themes}

1. 登入您的AEM作者執行個體。
1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主題]**。

   Themes目錄會顯示所有可用的主題，包括AEM Canvas提供的任何標準主題，以及您或您的組織已建立的自訂主題。

### 建立新主題 {#create-a-new-theme}

1. 在「佈景主題」目錄中，選取要儲存新佈景主題的資料夾。
1. 按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 佈景主題]**。

   ![建立新主題](/help/forms/assets/custom-theme-create.png)

1. 在&#x200B;**[!UICONTROL 建立主題]**&#x200B;對話方塊中，指定下列詳細資料：
   * **[!UICONTROL 標題]**：主題的描述性標題。
   * **[!UICONTROL 名稱]**：主題的節點名稱。
   * **[!UICONTROL 要預覽主題的調適型表單]**：對於核心元件主題，請選取核心元件型調適型表單。 **[!UICONTROL 使用預設最適化表單]**&#x200B;使用基礎最適化表單，而不是核心元件。 選取的表單會出現在主題編輯器畫布中，以便您編輯時即時預覽。
   * **[!UICONTROL 描述]** *（選擇性）*：主題的簡短描述。
   * **[!UICONTROL 設定容器]** *（選擇性）*：包含Adobe字型設定詳細資料的設定容器。
   * **[!UICONTROL 標籤]** *（選擇性）*：附加至主題的標籤，用於識別與搜尋。
1. 按一下「**[!UICONTROL 建立]**」。

   ![設定自訂佈景主題](/help/forms/assets/custom-theme-name.png)

   主題隨即建立。 您現在可以按一下&#x200B;**[!UICONTROL 編輯]**，在主題編輯器中開啟它。

### 編輯現有主題 {#edit-an-existing-theme}

1. 在&#x200B;**主題**&#x200B;目錄中，選取您要修改的主題。
1. 按一下動作列中的&#x200B;**[!UICONTROL 編輯]**，在主題編輯器中開啟主題。

   ![編輯佈景主題](/help/forms/assets/custom-theme-edit.png)

### 上傳主題 {#upload-a-theme}

您可以將主題套件（例如，從另一個環境匯出的套件）匯入到Themes目錄中：

1. 在&#x200B;**主題**&#x200B;目錄中，按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**。
1. 瀏覽以選取您電腦上的主題封裝（ZIP檔案），然後按一下[上傳]。**&#x200B;**

   ![上傳主題 — 使用檔案上傳選項建立功能表](/help/forms/assets/custom-theme-upload.png)

上傳的主題會顯示在Themes目錄中，並可像任何其他主題一樣進行編輯。

### 下載主題 {#download-a-theme}

您可以將主題匯出為套件（ZIP檔案），以在其他AEM Forms環境中重複使用或備份：

1. 在&#x200B;**佈景主題**&#x200B;目錄中，選取一或多個佈景主題（使用佈景主題卡上的核取方塊）。
1. 按一下動作列中的&#x200B;**[!UICONTROL 下載]**。 可能會出現一個對話方塊，其中包含所選主題的詳細資訊。
1. 確認或按一下對話方塊中的&#x200B;**[!UICONTROL 下載]**。 主題套件會以ZIP檔案形式下載至您的電腦。

   ![下載主題 — 選取主題並按一下[下載]](/help/forms/assets/custom-theme-download.png)

您稍後可以使用[在相同或其他環境中上傳主題](#upload-a-theme)來上傳此ZIP。

## 瞭解主題編輯器介面 {#understand-the-theme-editor}

在主題編輯器中開啟主題時，您會看到兩個主要區域：

![主題編輯器](/help/forms/assets/custom-theme-editor.png)

* **畫布** （右側）：顯示連結至主題的最適化表單預覽。 所有樣式變更都會立即反映在此處，因此您可以即時檢視編輯的影響。
* **側欄** （左側）：包含&#x200B;**選取器**&#x200B;面板，此面板以樹狀結構列出所有可設定樣式的表單元件，例如頁面、表單、欄位、按鈕、面板、影像、hCaptcha及reCaptcha。

### 畫布工具列 {#canvas-toolbar}

![主題編輯器畫布工具列，具有切換側面板、還原、重做、模擬器、編輯/預覽和主題選項](/help/forms/assets/custom-theme-toolbar-utilities.png)

工具列從左至右提供：
* **A：切換側面板**：顯示或隱藏選取器側欄。 當您想要聚焦於畫布時，使用此項來最大化表單預覽區域，或當您需要選取或樣式元件時，再次顯示側欄。
* **B：佈景主題選項** （下拉式清單）：開啟包含四個選項的功能表。 當您需要變更預覽表單、檢視CSS、管理儲存的樣式或取得編輯器內說明時，請按一下它。 當您開啟「佈景主題選項」下拉式清單時，您會看到：

  ![顯示[設定]、[檢視佈景主題]、[管理樣式]和[說明]的[佈景主題選項]下拉式清單](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL 設定]**：將畫布中顯示的表單切換為其他最適化表單。 使用此選項來檢查您的主題在其他表單上的外觀，而不離開編輯器。
     ![設定主題預覽的最適化表單](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL 檢視佈景主題CSS]**：開啟對話方塊，其中包含佈景主題的完整編譯的CSS。 若要只檢視目前選取之元件的CSS，請改用側邊欄中的&#x200B;**[!UICONTROL 檢視CSS]** （便於偵錯或複製規則）。
     ![檢視最終CSS](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL 管理樣式]**：開啟對話方塊以儲存、命名及重複使用文字和影像樣式。 已儲存的樣式可套用至其他元件；最近使用的樣式也可能出現，以快速重複使用。
   * **[!UICONTROL 說明]**：開始主題編輯器的影像引導式導覽。
* **C：還原/重做**：還原或重新套用您最後的樣式變更。 如果您嘗試某個樣式，並想要後退而不遺失其他編輯內容，則此功能相當實用。
* **D：模擬器**：選取裝置或中斷點（例如Desktop、Tablet或Mobile）以預覽該熒幕大小的表單。 表單預覽會調整大小以符合所選的中斷點。 您在選取中斷點時設定的任何樣式只會套用到該中斷點，因此您可以定義回應式樣式。 如需詳細資訊，請參閱[不同熒幕大小的樣式](#styling-for-different-screen-sizes)。
* **E：編輯/預覽**：在兩個模式之間切換。 **編輯**&#x200B;是預設值：您可以按一下畫布上的元件來選取它們，並在側邊欄中變更其樣式。 **預覽**&#x200B;以一般使用者看見表單的方式顯示，且沒有選取範圍框線、元件標籤或樣式側邊欄，因此您可以在發佈前檢查主題表單的外觀和行為。

<!--
**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).
-->

### 設定元件樣式

選取要造型的元件有兩種方式：
* **從畫布**：直接按一下表單中的元件（例如文字欄位、按鈕或下拉式清單）。 選取的元素會以邊框反白顯示，而元件標籤（例如「文字輸入Widget」）會出現在元素上方。 該元件的樣式選項會顯示在側邊欄中。

  ![從畫布編輯主題](/help/forms/assets/custom-theme-field-level.png)

* **從「選取器」面板**：使用左側邊欄中的樹狀結構來向下鑽研特定元件。 例如，展開&#x200B;**[!UICONTROL 欄位]** > **[!UICONTROL Widget]** > **[!UICONTROL 文字輸入]**&#x200B;以特別鎖定文字方塊Widget。

  ![從選擇器面板編輯主題](/help/forms/assets/custom-theme-selector.png)

#### 將樣式套用至元件 {#apply-styles-to-a-component}

選取元件後，側邊欄會顯示可組織的以下類別之可用樣式屬性：

* **[!UICONTROL 尺寸與位置]**：控制項對齊、大小、邊框間距、邊界、寬度、高度和Z索引。
* **[!UICONTROL 文字]**：設定字型系列、粗細、顏色、大小、行高、對齊、字母間距、文字裝飾和變形。 如需支援的CSS文字屬性完整清單，請參閱[MDN CSS文字檔案](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text)。
* **[!UICONTROL 背景]**：設定背景顏色、影像或漸層。 請參閱[MDN CSS背景檔案](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders)。
* **[!UICONTROL 邊框]**：定義邊框寬度、樣式、半徑和顏色。
* **[!UICONTROL 效果]**：新增不透明度、混合模式和陰影。

若要套用樣式：

1. 從畫布或「選取器」面板中選取元件。
1. 在側欄中設定所需的視覺屬性。 例如，選擇&#x200B;**[!UICONTROL 背景顏色]**&#x200B;並調整&#x200B;**[!UICONTROL 字型顏色]**。
1. 按一下核取記號圖示&#x200B;**[!UICONTROL 確定]**&#x200B;以確認屬性變更。

   ![套用樣式](/help/forms/assets/custom-theme-applying-style.png)

<!--
#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.
-->

### 表單層級樣式 {#form-level-styling}

表單層級樣式會將樣式廣泛套用至相同型別的所有元件。 例如，如果您在&#x200B;**[!UICONTROL 選取器]**&#x200B;面板中選取&#x200B;**欄位**，並將背景顏色設定為藍色，則表單中的每個欄位（文字方塊、數值方塊、日期選擇器和下拉式清單）都會繼承該藍色背景。

**範例：**&#x200B;若要在表單中的所有欄位上設定統一的背景顏色：

1. 在&#x200B;**選取器**&#x200B;面板中，選取&#x200B;**[!UICONTROL 欄位]**。
1. 在側邊欄中，將&#x200B;**[!UICONTROL 背景色彩]**&#x200B;設定為藍色。
1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

   ![表單層級樣式](/help/forms/assets/custom-theme-form-level-styling.png)

表單中的所有欄位元件現在都會顯示藍色背景。

### 元件層級樣式 {#component-level-styling}

元件層級樣式設定以特定元件型別為目標，覆寫任何較廣泛的表單層級樣式。 例如，如果您只想讓文字方塊Widget有不同的背景顏色，而其他欄位都保持藍色，您可以特別鎖定文字方塊Widget。

**範例：**&#x200B;若只要在文字方塊Widget上設定綠色背景和紫色字型：

1. 在「選取器」面板中，展開&#x200B;**[!UICONTROL 欄位]** > **[!UICONTROL Widget]** > **[!UICONTROL 文字輸入]**。
1. 將&#x200B;**[!UICONTROL 字型色彩]**&#x200B;設定為紫色。
   ![欄位層級樣式](/help/forms/assets/custom-theme-field-level-styling1.png)
1. 將&#x200B;**[!UICONTROL 背景色彩]**&#x200B;設定為綠色。
   ![欄位層級樣式](/help/forms/assets/custom-theme-field-level-styling2.png)
1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

文字方塊Widget現在會顯示帶有紫色文字的綠色背景，而所有其他欄位在表單層級樣式中仍會保持藍色。

>[!NOTE]
>
> **元件層級樣式一律優先於表單層級樣式。**&#x200B;在兩個層級定義樣式時，較明確的元件層級選取器會覆寫較廣的表單層級選取器。 這遵循標準[CSS特殊性規則](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)。 例如，如果您在所有欄位（表單層級）上設定了藍色背景，而在文字方塊Widget（元件層級）上設定了綠色背景，則文字方塊會顯示綠色背景。

## 不同熒幕大小的樣式 {#styling-for-different-screen-sizes}

您可以為不同的裝置大小定義不同的樣式，讓您的主題能夠回應。 主題編輯器工具列會顯示&#x200B;**裝置選項** （例如iPhone 5、iPad、Desktop、Tablet、Tablet、Small Screen），以預覽該熒幕大小的表單並設定其樣式。

1. 在畫布工具列中，使用&#x200B;**裝置模擬器**：按一下其中一個裝置標籤（例如，**[!UICONTROL Desktop]**、**[!UICONTROL Tablet]**、**[!UICONTROL iPad]**、**[!UICONTROL 小熒幕]**）。 表單上方的尺標會顯示所選裝置的畫素寬度。
1. 選取該裝置後，使用側邊欄來設定或調整樣式。 樣式僅適用於選取的裝置檢視。
1. 切換至其他裝置，並視需要定義其樣式。
1. 完成時，請按一下[確定] **&#x200B;**&#x200B;並儲存主題。

   ![佈景主題編輯器中的裝置模擬器 — 尺標和裝置選項（案頭、平板電腦、iPad、小熒幕）](/help/forms/assets/custom-theme-emulator.png)

因此，相同主題的每個裝置可以有不同的間距、字型大小或版面相關樣式，這符合回應式樣式的[AEM 6.5主題編輯器行為](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html)。

## 使用進階CSS覆寫 {#use-advanced-css-overrides}

對於無法透過視覺化側邊欄取得的樣式，您可以直接在編輯器中撰寫自訂CSS。

1. 選取元件。
1. 在側邊欄中，展開&#x200B;**[!UICONTROL 進階]**&#x200B;區段。
1. 在&#x200B;**[!UICONTROL CSS覆寫]**&#x200B;區域中寫入您的自訂CSS規則。 如果發生衝突，這些規則會覆寫透過視覺控制項設定的任何屬性。

如需完整的CSS屬性參考，請參閱[MDN Web Docs CSS參考](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)。

### 新增CSS虛擬元素 {#add-css-pseudo-elements}

**[!UICONTROL 進階]**&#x200B;區段也支援CSS虛擬元素，例如`::before`和`::after`。 這可讓您在不修改表單結構的情況下，在元件周圍插入內容或裝飾樣式。 例如，若要在文字方塊元件前新增視覺指示器：

1. 選取元件（例如，`CMP Textbox`）。
1. 展開&#x200B;**[!UICONTROL 進階]**&#x200B;區段。
1. 在`::before`虛擬元素欄位中，新增CSS屬性，例如：

   ```css
   color: #B10DC9;
   ```

   ![在CSS之前](/help/forms/assets/custom-theme-before-css.png)

1. 在`::after`虛擬元素欄位中，新增CSS屬性，例如：

   ```css
   color: #006400;
   ```

   在CSS之後![](/help/forms/assets/custom-theme-after-css.png)


這些虛擬元素會遵循標準CSS行為。 如需完整參考資訊，請參閱[MDN CSS Pseudo元素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)。

## 最佳做法 {#best-practices}

* **使用「選取器」面板進行精確定位**：設定巢狀元素（例如欄位標籤或完整說明）的樣式時，請使用左側的「選取器」面板，而非按一下畫布。 這可確保以適當的特定性產生正確的CSS選取器。
* **避免使用其他主題中的資產**：編輯主題時，請勿瀏覽並新增其他主題中的資產（例如影像）。 如果移動或刪除來源主題，您目前的主題會中斷。
* **請勿變更容器面板版面配置寬度**：在容器面板上指定固定寬度會讓面板保持靜態，並防止面板因應不同的熒幕大小。

## 另請參閱 {#see-also}

{{see-also}}
