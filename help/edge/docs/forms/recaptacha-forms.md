---
title: reCAPTCHA 與 Edge Delivery Services for AEM Forms as a Cloud Service 搭配使用
description: 在 EDS Form 中使用 Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: fe45123b3aefddaf02bc8584283941db168ba174
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 24%

---


# reCAPTCHA 與 Edge Delivery Services for AEM Forms as a Cloud Service 搭配使用

<span> **reCAPTCHA**&#x200B;功能在發行前程式中。 若要要求AEM FormsEdge Delivery Services的&#x200B;**reCAPTCHA**&#x200B;功能存取權，請從您的工作地址傳送電子郵件至mailto:aem-forms-ea@adobe.com。</span>

reCAPTCHA 是一種受歡迎的工具，用來保護網站免遭詐騙活動、垃圾郵件和濫用。在 Edge Delivery Services 中，最適化表單區塊有新增 Google reCAPTCHA 的功能，可區分人類和機器人。此功能可讓使用者保護其網站免遭垃圾郵件和濫用。
例如，考慮一個收集資料的查詢表單，例如開始和結束旅行日期、房間預算、預估旅行成本和旅行者資訊。在這種情況下，惡意使用者可能會利用該表單來發送網路釣魚電子郵件，或使用垃圾郵件機器人將不相關或有害內容填滿表單。整合 reCAPTCHA 可驗證提交內容是否來自真實使用者，以此提供更高的安全性並有效地減少垃圾郵件。

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services僅支援最適化表單區塊的&#x200B;**Score based(v3)-reCAPTCHA**。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


閱讀完本文章後，您將學會：
* [為單一表單啟用Google reCAPTCHA](#enable-google-recaptchas-for-a-single-form)
* [對網站上的所有表單啟用reCAPTCHA](#enable-recaptcha-for-all-the-forms)

## 必要條件

* 依照[使用最適化Forms區塊建立表單](/help/edge/docs/forms/create-forms.md)中說明的步驟開始開發Edge Delivery Services Forms。
* 使用[Google reCAPTCHA註冊您的網域並取得認證](https://www.google.com/recaptcha/admin/create)。

## 為單一表單啟用Google reCAPTCHA {#enable-google-recaptchas-for-a-single-form}

為單一表單啟用Google reCAPTCHA時，需要將Google的reCAPTCHA服務整合至特定網路表單，以防止自動濫用或垃圾訊息提交。

若要為單一表單啟用Google reCAPTCHA：
1. [在專案組態檔中設定reCAPTCHA秘密金鑰](#configure-secret-key)
1. [將reCAPTCHA網站金鑰新增至您的表單](#add-site-key)

若要開始在Edge Delivery Services Forms中設定reCaptcha，請參閱下列[試算表](/help/edge/docs/forms/assets/recaptcha.xlsx)，其中包含表單的表單定義。

### 在專案組態檔中設定reCAPTCHA秘密金鑰 {#configure-secret-key}

已在Google reCAPTCHA註冊之網域的網站密碼已新增至專案組態檔(`.helix/config`)，位於Microsoft SharePoint或Google Drive的AEM專案資料夾中。 若要將網站密碼新增至設定檔：

1. 前往Microsoft®SharePoint或Google Drive上的AEM專案資料夾。
1. 在Microsoft SharePoint網站的AEM專案資料夾中建立`.helix/config.xlsx`檔案，或在Google磁碟機的AEM專案資料夾中建立`.helix/config`檔案。

   >[!NOTE]
   >
   > [專案組態檔](https://www.aem.live/docs/configuration)是位於`/.helix/config`的試算表。 如果檔案不存在，請建立檔案。

1. 開啟`config`檔案並新增下列索引鍵和值配對：

   * **captcha.secret**： Google reCAPTCHA秘密金鑰值
   * **captcha.type**： reCAPTCHA v2

   >[!NOTE]
   >
   >  * 您可以從[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)擷取reCAPTCHA金鑰。
   >  * 您必須在`config`檔案中將&#x200B;**captcha.type**&#x200B;的值指定為&#x200B;**reCAPTCHA v2**。

   請參閱下列專案設定檔案的熒幕擷圖：

   ![專案組態檔](/help/forms/assets/recaptcha-config-file.png)

1. 儲存 `config` 檔案。

1. 使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)預覽並發佈`config`檔案。

### 將reCAPTCHA網站金鑰新增至您的表單 {#add-site-key}

透過Google reCAPTCHA註冊之網域的網站金鑰會新增至要保護之表單的試算表中。 若要將網站金鑰新增至表單：

1. 前往 Microsoft® SharePoint 或 Google Drive 的 AEM 專案資料夾，並開啟您的試算表。您也可以為表單建立新的試算表。
1. 在試算表中插入一列，以將新欄位新增為驗證碼，包括下列詳細資訊：
   * **型別**：驗證碼
   * **value**： Google reCAPTCHA網站金鑰值

   請參閱下列熒幕擷圖，將具有新列型別的試算表描述為CAPTCHA：

   ![Recaptcha試算表](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  您可以從[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)擷取reCAPTCHA金鑰。

1. 儲存試算表。
1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

在表單定義中新增列後，reCAPTCHA徽章會出現在表單的右下角。 這可確保表單現在不受詐騙活動、垃圾郵件和濫用的影響。

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## 對網站上的所有表單啟用reCAPTCHA{#enable-recaptcha-for-all-the-forms}

若要將Google reCAPTCHA套用至網站上使用Adaptive Forms Block的所有表單，請略過先前的步驟，直接將`sitekey`值內嵌至`recaptcha.js`檔案。 若要在`recaptcha.js`檔案中包含網站金鑰值：

1. [更新recaptcha.js檔案中的Google reCAPTCHA網站金鑰](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [部署檔案並建置專案](#2-deploy-the-file-and-build-the-project)
1. [使用AEM Sidekick預覽網站](#3-preview-the-site-using-the-aem-sidekick)

### 更新recaptcha.js檔案中的Google reCAPTCHA網站金鑰

1. 在本機電腦上開啟對應的GitHub存放庫。
1. 瀏覽至`[../Form Block/integrations]`資料夾並開啟`recaptcha.js`檔案。
1. 以Google reCAPTCHA網站金鑰值取代`siteKey`。

   ![Recaptcha套用至所有表單](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  您可以從[Google reCAPTCHAAdmin Console](https://www.google.com/recaptcha/admin)擷取reCAPTCHA金鑰。

1. 儲存 `recaptcha.js` 檔案。

### 部署檔案並建置專案

將更新的`recaptcha.js`檔案部署至您的GitHub專案，並確認建置成功。

### 使用AEM Sidekick預覽網站

使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)預覽及發佈網站。

reCAPTCHA徽章開始出現在您網站上的所有表單中。

## 另請參閱

{{see-more-forms-eds}}

