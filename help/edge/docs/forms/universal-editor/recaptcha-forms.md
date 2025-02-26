---
title: reCAPTCHA 與 AEM Forms as a Cloud Service 適用的 Edge Delivery Services 搭配使用
description: 在 AEM Forms 適用的 Edge Delivery Services 表單中使用 Google reCAPTCHA
feature: Edge Delivery Services
keywords: 表單中的 reCAPTCHA，在通用編輯器中使用 reCAPTCHA，在表單中新增 reCAPTCHA
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 96%

---


# 在 WYSIWYG 製作中使用 reCAPTCHA

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請從您的正式地址傳送電子郵件至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub組織名稱和存放庫名稱。 例如，如果存放庫URL是https://github.com/adobe/abc，組織名稱是adobe，存放庫名稱是abc。</span>


CAPTCHA (用於區分電腦和人類的完全自動化公開圖靈測試) 是流行的工具，用於保護網站免於詐騙活動、垃圾郵件和濫用。

例如，考慮一個根據其他扣除額和稅率計算稅額的表單。在這種情況下，惡意使用者可能會利用該表單來發送網路釣魚電子郵件，或使用垃圾郵件機器人將不相關或有害內容填滿表單。整合 CAPTCHA 可驗證提交內容是否來自真實使用者，從而提高安全性並有效地減少垃圾郵件。

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

在 Edge Delivery Services 表單中，表單區塊讓您可使用 **Captcha(Invisible)** 元件[將 Google reCAPTCHA 與表單連結](#connect-forms-with-recaptcha-service-by-google)，以區分人類和機器人。此功能可協助作者保護其表單免於垃圾郵件和濫用。

## 將表單與 Google 所提供的 reCAPTCHA 服務連結

您可以編寫 Edge Delivery Services 表單來實作 Google 所提供的 reCAPTCHA 服務。根據您的需要，您可以為您的 Edge Delivery Services 表單設定以下其中一種 reCAPTCHA 服務：

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> 如需有關 reCAPTCHA 運作方式的詳細資訊，請參閱 [Google reCAPTCHA](https://developers.google.com/recaptcha/)。

### 設定 reCAPTCHA Enterprise

reCAPTCHA Enterprise 是進階版、由 Google 所提供的企業級詐欺偵測和預防服務。其建置在 reCAPTCHA (分數型) 的基礎上，但可提供更多功能、擴充性和自訂功能，以滿足企業的複雜需求。

#### 開始之前

在為 Edge Delivery Services 表單設定 Google reCAPTCHA Enterprise 之前，請確保已完成下列步驟：

1. 建立或選取 [Google Cloud 專案](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)，並擷取[專案 ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)。

1. 為您的 Google Cloud 專案[啟用 reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)，並[建立 API 金鑰](https://console.cloud.google.com/apis/credentials)。

1. 建立[適用於您的 Google Cloud 專案的網站金鑰](https://console.cloud.google.com/security/recaptcha)，並複製該網站金鑰。

取得這些認證後，您即可繼續為您的表單設定 reCAPTCHA Enterprise：

1. [建立雲端設定容器](#1-create-cloud-configuration-container)
1. [為 reCAPTCHA Enterprise 建立雲端服務設定](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. 建立雲端設定容器

若要建立雲端設定容器，請執行下列步驟：

1. 登入您的作者執行個體。
1. 前往「**[!UICONTROL 工具]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。

   ![雲端設定容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，瀏覽至您的表單並選取「**[!UICONTROL 屬性]**」。

   ![雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在「**[!UICONTROL 設定屬性]**」對話框中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

1. 選取「**[!UICONTROL 儲存並關閉]**」，即可儲存設定並退出對話框。

   ![啟用雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
建立雲端設定容器後，將其發佈。

   ![發佈雲端設定](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. 為 reCAPTCHA Enterprise 建立雲端服務設定

若要為 reCAPTCHA Enterprise 建立雲端服務設定，請執行下列步驟：

1. 登入您的作者執行個體。
1. 瀏覽至「**[!UICONTROL 工具]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL reCAPTCHA]**」。

   ![Recaptcha 雲端設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   「**設定**」對話框隨即開啟。

1. 瀏覽到您的表單並選取「**[!UICONTROL 建立]**」。

   ![驗證碼設定](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   「**[!UICONTROL 建立 reCAPTCHA 設定]**」對話框隨即開啟。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 選取 [!DNL ReCAPTCHA Enterprise] 版本並指定標題、名稱、專案 ID、網站金鑰和 API 金鑰。

   >[!NOTE]
   >
   > 您可以從 reCAPTCHA Enterprise 的「[開始之前](#before-you-start)」區段取得專案 ID、網站金鑰和 API 金鑰。

1. 選取「**[!UICONTROL 金鑰類型]**」作為&#x200B;**分數型網站金鑰**。
1. 指定 [0 到 1 範圍內的閥值分數](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores)。大於或等於閾值分數的分數會識別為人類互動，否則會被視為機器人互動。
1. 選取「**[!UICONTROL 建立]**」，以建立雲端服務設定。

   建立 reCAPTCHA 雲端設定後，將其發佈。

   ![發佈 reCAPTCHA 設定](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您現在可以建立或編輯表單並使用 WYSIWYG 型製作新增 reCAPTCHA 元件。如需有關如何將 Google reCAPTCHA 整合到表單的詳細說明，請參閱「[在表單中使用 reCAPTCHA](#use-recaptcha-in-your-form)」。

## 設定 reCAPTCHA

reCAPTCHA 是 Google 所提供的免費服務，可協助網站偵測和防止流量濫用，包括機器人和垃圾郵件。其可支援分數型版本，該版本會在背景中運作並為每個使用者互動指派一個風險分數 (範圍從 0.0 到 1.0)。大於或等於閾值分數的分數會識別為人類互動，否則會被視為機器人互動。

#### 開始之前

在為 Edge Delivery Services 表單設定 Google reCAPTCHA 之前，請擷取[來自 Google 主控台的 reCAPTCHA API 金鑰組](https://www.google.com/recaptcha/admin)。該組會包括一個網站金鑰和一個秘密金鑰。

>[!NOTE]
>
> * Edge Delivery Services 表單僅支援 **reCAPTCHA 分數型**&#x200B;版本。

有了 API 金鑰組之後，您即可繼續為您的表單設定 reCAPTCHA：

1. [建立雲端設定容器](#1-create-cloud-configuration-container-1)
1. [為 reCAPTCHA 建立雲端服務設定](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. 建立雲端設定容器

若要建立雲端設定容器，請執行下列步驟：

1. 登入您的作者執行個體。
1. 前往「**[!UICONTROL 工具]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。

   ![雲端設定容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，瀏覽至您的表單並選取「**[!UICONTROL 屬性]**」。

   ![雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在「**[!UICONTROL 設定屬性]**」對話框中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

1. 選取「**[!UICONTROL 儲存並關閉]**」，即可儲存設定並退出對話框。

   ![啟用雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   建立雲端設定容器後，將其發佈。

   ![發佈雲端設定](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. 為 reCAPTCHA 建立雲端服務設定

若要為 reCAPTCHA 建立雲端服務設定，請執行下列步驟：

1. 登入您的作者執行個體。
1. 瀏覽至「**[!UICONTROL 工具]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL reCAPTCHA]**」。

   ![Recaptcha 雲端設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   「**設定**」對話框隨即開啟。

1. 瀏覽到您的表單並選取「**[!UICONTROL 建立]**」。

   ![驗證碼設定](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   「**[!UICONTROL 建立 reCAPTCHA 設定]**」對話框隨即開啟。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 選取 [!DNL ReCAPTCHA v2] 版本並指定標題和名稱。
1. 指定網站金鑰和秘密金鑰。

   >[!NOTE]
   >
   > 您可以從 reCAPTCHA 的「[開始之前](#before-you-begin)」區段取得網站金鑰和秘密金鑰。

1. 選取「**[!UICONTROL 建立]**」，以建立雲端服務設定。

   建立 reCAPTCHA 雲端設定後，將其發佈。

   ![發佈 reCAPTCHA 設定](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您現在可以建立和編輯表單並使用 WYSIWYG 型製作新增 reCAPTCHA 元件。如需有關如何將 Google reCAPTCHA 整合到表單的詳細說明，請參閱「[在表單中使用 reCAPTCHA](#use-recaptcha-in-your-form)」。

### 使用您的表單中的 reCAPTCHA

若要編寫表單並新增 reCAPTCHA (不可見) 元件，請執行下列步驟：

1. 在通用編輯器中開啟表單以進行編輯。
1. 瀏覽至內容樹中已新增的最適化表單區段。
1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增&#x200B;**[!UICONTROL 驗證碼 (不可見)]** 元件。

   ![新增 reCaptcha 元件](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   您也可以拖放所需的最適化表單元件，因為通用編輯器可提供直覺式拖放功能。

1. 按一下「**發佈**」，以在新增&#x200B;**[!UICONTROL 驗證碼 (不可見)]** 元件後再次發佈表單。

   ![重新發佈表單](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

您現在可以在以下 URL 使用 reCAPTCHA 服務來檢視表單：`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![reCAPTCHA 的表單](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 常見問題

* **如果使用者未建立 reCAPTCHA 雲端設定，會發生什麼情況？**

  **答**：如果使用者未建立 reCAPTCHA 雲端設定，AEM 伺服器會在全域設定容器中搜尋 reCAPTCHA 雲端設定。如果全域設定容器中不存在任何設定，則 AEM 伺服器會拋出錯誤。

* **如果使用者建立多個 reCAPTCHA 雲端設定，會發生什麼情況？**
  **答**：如果使用者建立多個 reCAPTCHA 雲端設定，系統會自動選取第一個建立的 reCAPTCHA 設定。

* **為什麼在已發佈的 URL 上看不到修改或變更？** 如果在已發佈的 URL 上看不到修改或變更，則需確保將表單重新發佈，以套用更新。

* **Edge Delivery Services 表單可支援哪種 reCAPTCHA 服務？**
  **答**：Edge Delivery Services 表單僅支援 Google 所提供的分數型 reCAPTCHA 服務。


## 另請參閱

{{universal-editor-see-also}}

