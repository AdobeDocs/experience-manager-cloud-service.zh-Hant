---
title: reCAPTCHA 與 AEM Forms as a Cloud Service 適用的 Edge Delivery Services 搭配使用
description: 在 AEM Forms 適用的 Edge Delivery Services 表單中使用 Google reCAPTCHA
feature: Edge Delivery Services
keywords: 在表單中使用reCAPTCHA，在通用編輯器中新增reCAPTCHA
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 320ab86bc73e874705d985b927e90eec3cad1cf9
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 6%

---


# 在WYSIWYG製作中使用reCAPTCHA

驗證碼（Completly Automated Public Turing Test，用於區分電腦和人體）是一種常用的工具，用於保護網站免受欺詐活動、垃圾郵件和濫用。

例如，考慮根據額外扣除額與稅率計算稅捐的表單。 在這種情況下，惡意使用者可能會利用該表單來發送網路釣魚電子郵件，或使用垃圾郵件機器人將不相關或有害內容填滿表單。整合驗證碼透過驗證來自正版使用者的提交內容，有效減少垃圾郵件專案，進一步提升安全性。

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

在Edge Delivery Services Forms中，表單區塊可讓您使用&#x200B;**Captcha（隱藏）**&#x200B;元件[連線Google reCAPTCHA與表單](#connect-forms-with-recaptcha-service-by-google)，以區分人類和機器人。 此功能可協助作者保護表單免受垃圾郵件和濫用。

## 透過Google連線Forms與reCAPTCHA服務

您可以編寫Edge Delivery Services Forms以實作Google提供的reCAPTCHA服務。 您可以視需要為Edge Delivery Services Forms設定下列reCAPTCHA服務之一：

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> 如需reCAPTCHA運作方式的詳細資訊，請參閱[Google reCAPTCHA](https://developers.google.com/recaptcha/)。

### 設定reCAPTCHA Enterprise

reCAPTCHA Enterprise是Google提供的一項優質、企業級詐騙偵測與預防服務。 它以reCAPTCHA （以分數為基礎）為基礎，但提供額外功能、擴充能力及自訂功能，以符合複雜的業務需求。

#### 在您開始之前

在針對Edge Delivery Services Forms設定Google reCAPTCHA Enterprise之前，請確定您已完成下列步驟：

1. 建立或選取[Google Cloud專案](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin)，並擷取[專案ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)。

1. [為您的Google Cloud專案啟用reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)，並[建立API金鑰](https://console.cloud.google.com/apis/credentials)。

1. 為您的Google Cloud專案](https://console.cloud.google.com/security/recaptcha)建立[網站金鑰，並複製網站金鑰。

取得這些認證後，您可以繼續為表單設定reCAPTCHA Enterprise：

1. [建立雲端設定容器](#1-create-cloud-configuration-container)
1. [為reCAPTCHA Enterprise建立雲端服務設定](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1.建立雲端設定容器

若要建立雲端設定容器，請執行以下步驟：

1. 登入您的作者執行個體。
1. 移至&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。

   ![雲端設定容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，瀏覽至您的表單並選取&#x200B;**[!UICONTROL 屬性]**。

   ![雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 設定屬性]**&#x200B;對話方塊中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

   ![啟用雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
『
建立雲端設定容器後，請將其發佈。

   ![發佈雲端設定](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2.建立reCAPTCHA Enterprise的雲端服務組態

若要建立reCAPTCHA Enterprise的雲端服務組態，請執行下列步驟：

1. 登入您的作者執行個體。
1. 導覽至&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL reCAPTCHA]**。

   ![Recaptcha雲端設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **組態**&#x200B;對話方塊開啟。

1. 導覽至您的表單，並選取&#x200B;**[!UICONTROL 建立]**。

   ![驗證碼組態](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL 建立reCAPTCHA組態]**&#x200B;對話方塊開啟。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 選取版本為[!DNL ReCAPTCHA Enterprise]，並指定標題、名稱、專案ID、網站金鑰和API金鑰。

   >[!NOTE]
   >
   > 您可以從reCAPTCHA Enterprise的[開始之前](#before-you-start)區段取得專案識別碼、網站金鑰和API金鑰。

1. 選取&#x200B;**[!UICONTROL 金鑰型別]**&#x200B;做為&#x200B;**以分數為基礎的網站金鑰**。
1. 指定0到1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores)範圍內的[臨界值分數。 分數大於或等於臨界值分數會識別人類互動，否則會視為機器人互動。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立雲端服務組態。

   建立reCAPTCHA雲端設定後，請發佈。

   ![發佈Recaptcha組態](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您現在可以建立或編輯表單，並使用WYSIWYG式編寫來新增reCAPTCHA元件。 如需將Google reCAPTCHA整合至表單的詳細指示，請參閱[在您的表單中使用reCAPTCHA](#use-recaptcha-in-your-form)。

## 設定reCAPTCHA

reCAPTCHA是Google提供的免費服務，可協助網站偵測及防止濫用的流量，包括機器人和垃圾訊息。 它支援在背景操作的以分數為基礎的版本，並為每個使用者互動指派風險分數（範圍從0.0到1.0）。 分數大於或等於臨界值分數會識別人類互動，否則會視為機器人互動。

#### 開始之前

在為Edge Delivery Services Forms設定Google reCAPTCHA之前，請從Google主控台](https://www.google.com/recaptcha/admin)擷取[reCAPTCHA API金鑰組。 此配對包含網站金鑰和秘密金鑰。

>[!NOTE]
>
> * Edge Delivery Services Forms僅支援&#x200B;**reCAPTCHA分數型**&#x200B;版本。

取得API金鑰組後，您就可以繼續為表單設定reCAPTCHA：

1. [建立雲端設定容器](#1-create-cloud-configuration-container-1)
1. [建立reCAPTCHA的雲端服務設定](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1.建立雲端設定容器

若要建立雲端設定容器，請執行以下步驟：

1. 登入您的作者執行個體。
1. 移至&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。

   ![雲端設定容器](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，瀏覽至您的表單並選取&#x200B;**[!UICONTROL 屬性]**。

   ![雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. 在&#x200B;**[!UICONTROL 設定屬性]**&#x200B;對話方塊中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

   ![啟用雲端設定屬性](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   建立雲端設定容器後，請將其發佈。

   ![發佈雲端設定](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2.建立reCAPTCHA的雲端服務設定

若要建立reCAPTCHA的雲端服務設定，請執行以下步驟：

1. 登入您的作者執行個體。
1. 導覽至&#x200B;**[!UICONTROL 工具]** ![工具–1](/help/forms/assets/tools-1.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL reCAPTCHA]**。

   ![Recaptcha雲端設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   **組態**&#x200B;對話方塊開啟。

1. 導覽至您的表單，並選取&#x200B;**[!UICONTROL 建立]**。

   ![驗證碼組態](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   **[!UICONTROL 建立reCAPTCHA組態]**&#x200B;對話方塊開啟。

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 選取版本為[!DNL ReCAPTCHA v2]並指定標題和名稱。
1. 指定網站金鑰和秘密金鑰。

   >[!NOTE]
   >
   > 您可以從[Before You Begin](#before-you-begin)區段取得reCAPTCHA的網站金鑰和秘密金鑰。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立雲端服務組態。

   建立reCAPTCHA雲端設定後，請發佈。

   ![發佈Recaptcha組態](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

您現在可以建立和編輯表單，並使用WYSIWYG式編寫來新增reCAPTCHA元件。 如需將Google reCAPTCHA整合至表單的詳細指示，請參閱[在您的表單中使用reCAPTCHA](#use-recaptcha-in-your-form)。

### 在您的表單中使用reCAPTCHA

若要製作表單並新增reCAPTCHA （隱藏）元件，請執行以下步驟：

1. 在通用編輯器中開啟表單以進行編輯。
1. 導覽至內容樹中已新增的最適化表單區段。
1. 按一下&#x200B;**[!UICONTROL 新增]**&#x200B;圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增&#x200B;**[!UICONTROL 驗證碼（無）]**&#x200B;元件。

   ![新增reCaptcha元件](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   您也可以拖放所需的調適型Forms元件，因為Universal Editor提供直覺式的拖放功能。

1. 新增&#x200B;**[!UICONTROL Captcha (Invisible)]**&#x200B;元件後，按一下&#x200B;**發佈**&#x200B;以再次發佈表單。

   ![重新發佈表單](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

您現在可以在下列URL檢視含有reCAPTCHA服務的表單：
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`。

![含reCAPTCHA的表單](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 常見問題

* **如果使用者未建立reCAPTCHA雲端設定，會發生什麼事？**

  **A**：如果使用者未建立reCAPTCHA雲端設定，則AEM伺服器會在全域設定容器中搜尋reCAPTCHA雲端設定。 如果全域設定容器中沒有設定，AEM伺服器會擲回錯誤。

* **如果使用者建立多個reCAPTCHA雲端設定，會發生什麼事？**
  **A**：如果使用者建立多個reCAPTCHA雲端組態，系統會自動選取第一個建立的reCAPTCHA組態。

* **為何在發佈的URL中看不到修改或變更？**
如果在已發佈的URL看不到修改或變更，請確保已重新發佈表單以套用更新。

* **Edge Delivery Services Forms支援哪種reCAPTCHA服務？**
  **A**： Edge Delivery Services Forms僅支援Google提供的以分數為基礎的reCAPTCHA服務。


## 另請參閱

{{see-more-forms-eds}}
