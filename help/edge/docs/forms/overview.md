---
title: AEM Forms Edge Delivery Service 概觀
description: AEM Forms Edge Delivery Service 旨在為實現最佳效而建置，讓您能夠暢想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 26%

---


# AEM Forms Edge Delivery Service

透過Adobe的AEM Forms Edge Delivery Service簡化表單建立作業，並提高完成率。 這項功能強大、可撰寫的服務可讓您建立具有卓越效能和視覺吸引力的企業級表單。 AEM會同時優先考慮使用者體驗和業務目標，確保超快的載入時間並增加表單完成次數。

您可以使用此服務來：

* **使用令人驚豔的表單Captivate使用者**：使用預先建立的元件庫輕鬆建立複雜且吸引人的表單。 輕鬆整合reCAPTCHA、直接將表單提交至電子郵件，並允許順暢的檔案上傳至Sharepoint、Azure Storage和Amazon S3等安全儲存解決方案。 甚至可建立您自己的自訂表單元件，將您獨特的視覺效果生動呈現。

* **使用您選擇的工具建立數位註冊體驗**：透過分離內容來源來提高編寫效率。 開箱即用地使用檔案式編寫(Microsoft 365和Google Workspace)和AEM編寫(AEM編輯器)。 因此，您可以在相同網站上使用多個內容來源，並使用您偏好的編寫工具，例如Microsoft Excel、Google Sheets或Adaptive Forms Editor。

* **使用完美的Lighthouse分數建置表單**：建立可快速載入和轉譯的表單，即使在網際網路連線速度緩慢時也是如此。 更快的載入時間和最佳化使用者體驗有助於提高表單完成率和轉換率。

  <div>
    <style>
    .image-container {
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container 
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms主要功能">
    </div>


</div>

<!--

<!--

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
    >[!NOTE]
    >[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 主要功能

* **以HTML5為基礎的表單欄位元件**： AEM Forms Edge Delivery Service可讓您使用以HTML5為基礎的表單元件，建立使用者易記且互動式的表單 [輸入型別](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文字區域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選取</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">欄位集</a>  元素。 這些元件適用於不同型別的資料收集，並可輕鬆自訂以符合您的特定需求。

* **協助工具**：可存取表單區塊中的欄位。 每個標籤都與其各自的輸入元素連結，而且會自動產生ID以供連結。 與欄位相關的說明是透過aria-descripted by屬性連結。 支援使用標準Tab/Shift + Tab鍵的鍵盤導覽。

* **樣式**：每個表單欄位都有固定的HTML結構，可以輕鬆使用自訂CSS或JavaScript檔案進行裝飾。 CSS和JS中目標欄位的選取器是根據型別和名稱而提供。 您可以因標準化結構而輕鬆建立新的選取器。

* **規則**：輕鬆建立邏輯，以根據使用者輸入或預先定義的條件調整欄位可見度、驗證和行為。 規則提供靈活且直覺的方式為您的表單新增智慧，確保它們能根據使用者輸入順暢地調整。

* **驗證**：提交前，系統會驗證表單，無效欄位會適當地標示為使用者顯示的錯誤訊息。 有各種模式可用來顯示這些錯誤。

有幾個進階功能可應要求提供：

* **檔案上傳**：您可以將檔案附件功能新增至表單。 無論您需要向使用者收集檔案、影像或其他檔案，檔案上傳功能都能讓您輕鬆上手。 透過可用的自訂處理選項，您可以量身打造檔案上傳程式，以符合您的特定需求。

* **reCAPTCHA**：透過我們的開箱即用(OOTB)支援，將Google reCAPTCHA無縫整合至您的表單中，受益匪淺。 保護您的表單免受詐騙活動、垃圾郵件和濫用，同時保持順暢且無中斷的使用者體驗。

* **在表單提交時傳送電子郵件通知**：消除手動後續追蹤的麻煩，並確保利用我們內建的表單提交電子郵件自動化進行及時通訊。 此整合式解決方案可讓您在有人填寫您網站上的表單時，輕鬆通知相關人員，包括傳送表單資料。 無需複雜的設定或其他工具，開箱即用。


## 工作流程

![檔案式撰寫生態系統](/help/edge/assets/document-based-authoring-workflow.png)

## 開始建立表單

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="使用 eds Forms 建立表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用Google工作表或Microsoft Excel建立表單</b>
        </a>
        <p>建立可在行動裝置上快速載入和呈現並自動重排的表單。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="提交表單" alt="使用 EDS Form 中的表單片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">將表單提交到試算表</b>
        </a>
        <p>直接將表單提交到您的 Microsoft Excel 或 Google Sheets。</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="將樣式或主題套用至 eds Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">自訂主題</b>
        </a>
        <p>在不同形式中套用相同的主題，建立一致的品牌形象。</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="新增驗證至表單欄位" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">套用欄位驗證</b>
        </a>
        <p>檢查表單輸入的格式是否正確，以減少錯誤和挫折感。</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="使用規則將動態行為新增至表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用規則將動態行為新增至表單</b>
        </a>
        <p>跨多種表單重複使用預先設定的片段。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="翻譯 EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">翻譯表單</b>
        </a>
        <p>擴展表單的範圍，同時控制檢查成本。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="新增可重複區段至 EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">新增可重複區段</b>
        </a>
        <p>輕鬆建立可重複區段並新增至表單。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="使用標準 JavaScript 和 CSS 建立自訂表單元件"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">建立自訂元件</b>
        </a>
        <p>使用標準 JavaScript 和 CSS 建立元件和主題。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="使用 EDS Form 中的 reCAPTCHA" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用 reCAPTCHA</b>
        </a>
        <p>使用 OOTB reCAPTCHA 整合，防止大量垃圾郵件和機器人。</p>
    </div>


</div>


</br>









