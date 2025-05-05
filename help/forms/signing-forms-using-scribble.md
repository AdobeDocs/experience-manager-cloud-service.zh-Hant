---
title: 如何使用手寫簽名將電子簽章套用至表單？
description: 瞭解如何使用手寫簽名將電子簽章套用至表單。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 2%

---

# 使用手寫簽名對表單進行電子簽章{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

>[!NOTE]
>
> Adobe建議針對[建立新的Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md)或[將Adaptive Forms新增至AEM Sites頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)，使用現代且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文說明使用基礎元件製作最適化Forms的舊方法。

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |


您可以使用&#x200B;**手寫簽章**&#x200B;元件，在最適化表單上繪製（手寫的）簽章。<!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![手寫簽名對話方塊](assets/scribble-signature.png)

## 簽章視窗中可用的各種選項

* **A：**&#x200B;按一下&#x200B;**繪圖筆刷**&#x200B;圖示，在畫布上繪製您的簽名。
* **B：**&#x200B;按一下&#x200B;**清除**&#x200B;圖示以清除畫布上的簽章。
* **C：**&#x200B;按一下&#x200B;**地理位置**&#x200B;圖示以新增地理位置以及簽章。
* **D：**&#x200B;按一下&#x200B;**鍵盤**&#x200B;圖示，在畫布上輸入您的名稱。

一旦您在「草寫簽名」視窗中選取「完成![aem_forms_save](assets/aem_forms_save.png)」圖示，便無法編輯簽名。 如果想要編輯簽名，則必須忽略目前的簽名，並使用上面的「繪圖筆刷/鍵盤」選項重新簽名。

您可以選取&#x200B;**設定** ![設定圖示](assets/configure.png)圖示來設定手寫簽名畫布的外觀比例。
* 當「草寫簽名」畫布的外觀比例小於1時，地理位置資訊會新增至「草寫簽名」畫布底部。


* 當Scribble Signature畫布的外觀比例大於1時，地理位置資訊會新增到Scribble Signature畫布的右側。


![手寫簽章 — 底部](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>簽名一律以PNG格式儲存。
>

## 設定最適化表單以使用草寫簽名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 以編輯模式開啟最適化表單。
1. 將&#x200B;**手寫簽章**&#x200B;元件從元件瀏覽器拖放至最適化表單。
1. 選取&#x200B;**設定** ![設定](assets/configure.png)圖示。 它會開啟屬性瀏覽器並顯示草寫簽名元件的屬性。 [設定草寫簽章的屬性](#properties-of-scribble-signature-component)，如下節所述。

   ![草寫簽名](/help/forms/assets/scribblesig.png)

1. 選取「完成![aem_forms_save](assets/aem_forms_save.png)」圖示以儲存變更。 已成功設定簽章。

## 設定手寫簽名元件的屬性

您可以透過「設定」對話方塊輕鬆自訂訪客的手寫簽名元件。

### 基本標籤

![基本索引標籤](/help/forms/assets/scribblesig-basic.png)

* **名稱** — 您可以在表單和規則編輯器中輕鬆識別具有唯一名稱的表單元件，但名稱不得包含空格或特殊字元。

* **標題** — 您可以使用其Title輕鬆識別表單中的元件，預設情況下，標題會顯示在元件上方。 如果您未新增標題，則會顯示元件的名稱而非標題文字。

* **允許標題使用RTF格式** — 此功能可讓使用者格式化純文字標題，並整合如粗體、斜體、底線文字、各種字型、字型大小、顏色等功能以及可增強視覺呈現和自訂的其他選項。 它提供更大的彈性和創意控制，讓標題在檔案、網站或應用程式中脫穎而出。\
  選取&#x200B;**允許標題為RTF格式**&#x200B;的核取方塊後，即可看到格式化選項，以設定元件標題的樣式。 若要存取所有可用的格式選項，您可以按一下![全熒幕圖示](/help/forms/assets/fullscreen-icon.png)標籤。

  ![RTF支援](/help/forms/assets/richtext-support-title.png)

* **隱藏標題** — 選取隱藏元件標題的選項。
* **必要欄位** — 選取選項，讓欄位成為必要欄位。
* **必要欄位訊息** - **必要欄位訊息**&#x200B;是當使用者嘗試提交表單而未填寫必要欄位時，顯示給使用者的可自訂訊息。
* **資料模型繫結參考** — 繫結參考是儲存在外部資料來源中，並在表單中使用的資料元素的參考。 繫結參考可讓您將資料動態繫結至表單欄位，讓表單可顯示資料來源的最新資料。 例如，繫結參考可用於根據在表單中輸入的客戶ID在表單中顯示客戶名稱和地址。 繫結參考也可用來使用輸入到表單中的資料更新資料來源。 透過這種方式，AEM Forms可讓您建立與外部資料來源互動的表單，提供順暢的使用者體驗來收集和管理資料。
* **隱藏物件** — 選取選項，以隱藏表單中的元件。 元件仍可於其他用途存取，例如將其用於規則編輯器中的計算。 當您需要儲存不需要由使用者看到或直接變更的資訊時，這將很有用。
* **停用物件** — 選取選項以停用元件。 一般使用者無法啟動或編輯已停用的元件。 使用者可以看到欄位的值，但無法修改它。 元件仍可於其他用途存取，例如將其用於規則編輯器中的計算。
* **長寬比** — 手寫簽名元件的長寬比定義了寬度和高度之間的比例關係。
* **欄位配置** - **欄位配置**&#x200B;選項決定表單元素(包括標籤（標題）和錯誤訊息)相對於元件的放置方式。 **標題和錯誤位於Widget**&#x200B;頂端，將欄位的標題（標籤）和錯誤訊息放置在元件上方。 **繼承自最適化表單設定**&#x200B;使用最適化表單設定中指定的預設欄位配置設定。
* **CSS類別** - **CSS類別**&#x200B;可讓您指派樣式表中定義的一或多個CSS類別，將自訂樣式套用至元件。 它可讓您在最適化表單中自訂一致的樣式和版面。

### 說明內容

![說明內容標籤](/help/forms/assets/scribblesig-help.png)

* **簡短說明** — 簡短說明是簡短文字說明，提供特定表單欄位用途的其他資訊或說明。 它可協助使用者瞭解應在欄位中輸入哪種資料型別，並可提供指引或範例，以協助確保輸入的資訊有效並符合所需條件。 依預設，簡短說明會維持隱藏狀態。 啟用&#x200B;**永遠顯示簡短描述**&#x200B;選項，以在元件下方顯示它。

* **永遠顯示簡短描述** — 啟用選項以在元件下方顯示簡短描述。

* **完整說明** — 它參考提供給使用者的其他資訊或指引，以協助使用者正確填寫表單欄位。 當使用者按一下放置於元件旁的說明圖示(i)時，就會出現此選項。 它提供比表單欄位的標籤或預留位置文字更詳細的資訊，旨在協助使用者瞭解欄位的需求或限制。 它也可以提供建議或範例，讓填寫表單更容易、更準確。

### 協助工具標籤 {#accessibility}

![協助工具標籤](/help/forms/assets/scribblesig-acc.png)

在&#x200B;**協助工具**&#x200B;標籤上，設定元件的[ARIA協助工具](https://www.w3.org/WAI/standards-guidelines/aria/)標籤的值。 熒幕助讀程式的文字有多種可用選項：

* **熒幕Reader優先順序** — 熒幕Reader優先順序是指視覺障礙人士使用的輔助技術（例如熒幕閱讀程式）特別要閱讀的其他文字。 此文字提供表單欄位用途的音訊說明，並可包含欄位標題、說明、名稱和任何相關訊息（自訂文字）的相關資訊。 熒幕助讀程式文字可協助確保表單可供所有使用者存取，包括視覺障礙的使用者，並提供他們對表單欄位及其要求的完整瞭解。

   * **自訂文字**：選取此選項即可使用ARIA協助工具標籤的自訂文字。 選取此選項會顯示「自訂文字」對話方塊。 您可以在「自訂文字」對話方塊中新增相關資訊。
   * **簡短說明**：選取此選項即可使用ARIA協助工具標籤的說明。
   * **標題**：選取此選項即可使用ARIA協助工具標籤的標題。
   * **名稱**：選取此選項即可使用ARIA協助工具標籤的名稱。
   * **無**：如果您不想新增ARIA協助工具標籤，請選取此選項。

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## 另請參閱 {#see-also}

{{see-also}}