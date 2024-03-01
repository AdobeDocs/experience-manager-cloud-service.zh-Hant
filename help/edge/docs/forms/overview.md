---
title: AEM Forms Edge Delivery Service 概觀
description: AEM Forms Edge Delivery Service 旨在為實現最佳效而建置，讓您能夠暢想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1c6e44fd6652d93ba73bc2eb3604cd08eae7a33c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 43%

---


# AEM Forms Edge Delivery Service

使用 Adobe Systems 的 AEM Forms 邊緣交付服務簡化表單創建並推動更高的完成率。 這項功能強大、可組合的服務使您能夠版本編號具有卓越性能和視覺吸引力的企業級表單。 AEM優先考慮使用者體驗和您的業務目標，確保閃電般的載入時間和更高的表單完成率。

您可將該服務用於：

* **以令人驚歎的表單吸引使用者：使用預先建立元件資料庫輕鬆構建複雜且引人入勝的表單**。 輕鬆集成 reCAPTCHA，將表單直接提交到電子郵件，並允許無縫上傳檔，以保護 Sharepoint、Azure 存儲和 Amazon S3 按讚儲存解決方案。 甚至可以創建您自己的自定義表單元件，將您的獨特願景變為現實。

* **使用您選擇的**&#x200B;工具建立數字註冊體驗：通過分離內容源來提高創作效率。 開箱即用，您可以使用基於文件的創作（Microsoft 365 和 Google 工作環境）和AEM創作（AEM編輯器）。 因此，您可以在同一網站上使用多個內容源，並使用首選的創作工具，例如 Microsoft Excel、Google 表格或自適應Forms编辑器。

* **構建具有完美燈塔分數**&#x200B;的表單：構建快速載入和渲染的表單，平均在緩慢的互聯網連接下。 更快的載入時間和最佳化使用者體驗有助於提高表單完成率和轉換率。

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 70%; /* Set image width to 70% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms 主要功能">
    </div>


</div>
&lt;!-- &gt;
* **用令人驚歎的表單吸引使用者**：
使用預先建立元件資料庫輕鬆構建複雜且引人入勝的表單。 輕鬆集成 reCAPTCHA，將表單直接提交到電子郵件，並允許無縫上傳檔，以保護 Sharepoint、Azure 存儲和 Amazon S3 按讚儲存解決方案。 甚至可以創建您自己的自定義表單元件，將您的獨特願景變為現實。

    ![報名錶]（/help/edge/資產/enrollment-form.png）

* **建立擁有 Lighthouse 分數的表單**：建立能快速載入和呈現的表單，即使網路連線慢也可行。更快的載入時間和最佳化使用者體驗有助於提高表單完成率和轉換率。

  ![為您的表格提供完美的燈塔分數](/help/edge/assets/lighthouse-forms.png)

* **使用您選擇的**&#x200B;工具建立數字註冊體驗：通過分離內容源來提高創作效率。 您可以一開啟即使用 AEM 編寫和文件型編寫。因此，您可以在同一網站上使用多個內容源，並使用首選的創作工具，例如 Microsoft Excel、Google 表格或 AEM 编辑器。

  ![邊緣交付表單創作工具](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 開始建立窗體

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="使用 eds Forms 建立表單" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">使用Google表格或 Microsoft Excel 建立表單
            </b>
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
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="使用規則向表單添加動態行為" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">使用規則向表單添加動態行為
            </b>
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









