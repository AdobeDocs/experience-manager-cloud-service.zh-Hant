---
title: AEM Forms Edge Delivery Service概述
description: AEM Forms Edge Delivery Service專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 34ba430ae9b40fc3bc675af20bbee2534c44a0c3
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service是一項Adobe提供的可組合服務，可讓您建立並傳遞高影響力、快速績效的網路表單。 此可撰寫的服務與Adobe Experience Manager (AEM)緊密整合，可讓您透過直覺式有效的工作流程，設計、建置及部署高影響力、快如閃電的Web表單。

AEM Forms Edge Delivery Service可幫助您：

* **製作令人驚豔的視覺表單**：摒棄平淡無奇、小眾化的設計，透過反映您品牌身分的動態現代表單來吸引使用者。 運用預先建立的元件或建立您自己的自訂元件，輕鬆快速地實現您的願景。

* **使用完美的Lighthouse分數建置表單**：建立可快速載入和轉譯的表單，即使在網際網路連線速度緩慢時也是如此。 載入速度更快，使用者體驗最佳化，有助於提高表單完成率和轉換率。

* **簡化撰寫和提交作業**：使用熟悉的工具(如Microsoft Excel或Google Sheets)建立表單，而非使用傳統的撰寫環境。 直接將表單提交至您的Microsoft Excel或Google工作表，並使用其生態系統來輕鬆處理提交的資料。

## 從基礎知識開始

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="使用EDS表單建立表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">建立表單</b>
        </a>
        <p>建立可快速載入及轉譯的表單，並在行動裝置上自動重新整理。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="新增驗證至表單欄位" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">套用欄位驗證</b>
        </a>
        <p>檢查表單輸入是否為正確格式，以減少錯誤和挫折。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="在EDS表單中使用表單片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">建立表單片段</b>
        </a>
        <p>在多個表單中重複使用預先設定的片段。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="翻譯EDS表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">翻譯表單</b>
        </a>
        <p>在控制成本的同時，擴大表單的覆蓋面。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="將樣式或主題套用至EDS表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">自訂主題</b>
        </a>
        <p>跨表單套用相同主題，建立一致的品牌影像。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="將可重複的區段新增至EDS表單" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">新增可重複區段</b>
        </a>
        <p>輕鬆建立可重複區段並新增至表單。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="使用標準JavaScript和CSS建立自訂表單元件"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">建立自訂元件</b>
        </a>
        <p>使用標準JavaScript和CSS來建立元件和主題。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="在EDS表單中使用reCAPTCHA" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用reCAPTCHA</b>
        </a>
        <p>使用OOTB reCAPTCHA整合功能，提供強大的垃圾郵件和機器人保護。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="提交表單" alt="在EDS表單中使用表單片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">提交表單至試算表</b>
        </a>
        <p>直接將表單提交至您的Microsoft Excel或Google工作表。</p>
    </div>
</div>


</br>









