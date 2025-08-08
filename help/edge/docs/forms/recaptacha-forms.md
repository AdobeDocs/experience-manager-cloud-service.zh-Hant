---
title: reCAPTCHA 與 AEM Forms as a Cloud Service 適用的 Edge Delivery Services 搭配使用
description: 在 AEM Forms 適用的 Edge Delivery Services 表單中使用 Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 100%

---


# reCAPTCHA 與 AEM Forms as a Cloud Service 適用的 Edge Delivery Services 搭配使用

<!--
<span>The **reCAPTCHA** feature is under the pre-release program. To request access to the **reCAPTCHA** feature for Edge Delivery Services for AEM Forms, send an email from your work address to mailto:aem-forms-ea@adobe.com.</span>
-->

reCAPTCHA 是一種受歡迎的工具，用來保護網站免遭詐騙活動、垃圾郵件和濫用。在 Edge Delivery Services 中，最適化 Forms 區塊有新增 Google reCAPTCHA 的功能，可區分人類和機器人。此功能可讓使用者保護其網站免遭垃圾郵件和濫用。
例如，考慮一個收集資料的查詢表單，例如開始和結束旅行日期、房間預算、預估旅行成本和旅行者資訊。在這種情況下，惡意使用者可能會利用該表單來發送網路釣魚電子郵件，或使用垃圾郵件機器人將不相關或有害內容填滿表單。整合 reCAPTCHA 可驗證提交內容是否來自真實使用者，以此提供更高的安全性並有效地減少垃圾郵件。

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services 僅支援最適化表單區塊的&#x200B;**分數型 (v3)-reCAPTCHA**。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


閱讀完本文章後，您將學會：
- [為單一表單啟用 Google reCAPTCHA](#enable-google-recaptchas-for-a-single-form)
- [為網站上所有表單啟用 reCAPTCHA](#enable-recaptcha-for-all-the-forms)

## 必要條件

- 依照[使用最適化表單區塊建立表單](/help/edge/docs/forms/create-forms.md)所述步驟，開始開發 Edge Delivery Services 表單。
- 註冊您的網域請使用 [Google reCAPTCHA 並取得憑證](https://www.google.com/recaptcha/admin/create)。

## 為單一表單啟用 Google reCAPTCHA {#enable-google-recaptchas-for-a-single-form}

為單一表單啟用 Google reCAPTCHA 涉及將 Google 的 reCAPTCHA 服務整合到特定網頁表單中，以防止自動化濫用或寄送垃圾郵件。

若要為單一表單啟用 Google reCAPTCHA：

1. [在專案設定檔中設定 reCAPTCHA 祕密金鑰](#configure-secret-key)
1. [將 reCAPTCHA 網站金鑰新增至您的表單中](#add-site-key)

若要開始在 Edge Delivery Services 表單中設定 reCaptcha，請參閱下列[試算表](/help/edge/docs/forms/assets/recaptcha.xlsx)，其中包括表單的表單定義。

### 在專案設定檔中設定 reCAPTCHA 祕密金鑰 {#configure-secret-key}

將使用 Google reCAPTCHA 註冊的網域的 Site Secret 新增至專案設定檔 (`.helix/config`)，其位於 Microsoft SharePoint 或 Google Drive 上的 AEM Project 資料夾中。若要將 Site Secret 新增至設定檔：

1. 前往您儲存在 Microsoft® SharePoint 或 Google Drive 上的 AEM 專案資料夾。
1. 在 Microsoft SharePoint 網站的 AEM 專案資料夾中建立 `.helix/config.xlsx` 檔案，或在 Google Drive 的 AEM 專案資料夾中建立 `.helix/config` 檔案。

   >[!NOTE]
   >
   > 這個[專案設定檔](https://www.aem.live/docs/configuration)是試算表，位於 `/.helix/config`。如果檔案不存在，請建立檔案。

1. 開啟 `config` 檔案，並新增以下鍵值對：

   - **captcha.secret**：Google reCAPTCHA 密鑰值
   - **captcha.type**：reCAPTCHA v2

   >[!NOTE]
   >
   >  - 您可以從 [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) 擷取 reCAPTCHA 金鑰。
   >  - 您必須將 `config` 檔案中 **captcha.type** 的值指定為 **reCAPTCHA v2**。

   請參考下方專案設定檔螢幕擷圖：

   ![專案設定檔](/help/forms/assets/recaptcha-config-file.png)

1. 儲存 `config` 檔案。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈 `config` 檔案。

### 將 reCAPTCHA 網站金鑰新增至您的表單中 {#add-site-key}

使用 Google reCAPTCHA 註冊的網域的網站金鑰，將會新增到要保護的表單的試算表中。若要將網站金鑰新增至表單：

1. 前往 Microsoft® SharePoint 或 Google Drive 的 AEM 專案資料夾，並開啟您的試算表。您也可以為表單建立新的試算表。
1. 在試算表中插入一行以新增驗證碼的欄位，包括以下詳細資訊：
   - **類型**：驗證碼
   - **值**：Google reCAPTCHA 網站金鑰值

   請參閱下方螢幕擷圖，顯示新一列類型為驗證碼的試算表：

   ![Recaptcha 試算表](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  您可以從 [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) 擷取 reCAPTCHA 金鑰。

1. 儲存試算表。
1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

在表單定義中新增一列後，表單右下角會出現一個 reCAPTCHA 徽章。這樣將確保該表單現在受到保護，避免詐騙活動、垃圾郵件和濫用的影響。

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## 為網站上所有表單啟用 reCAPTCHA{#enable-recaptcha-for-all-the-forms}

若要將 Google reCAPTCHA 套用至網站上使用自適應表單區塊的所有表單，請略過先前步驟並將 `sitekey` 值直接嵌入 `recaptcha.js` 檔案。若要將網站金鑰值加入 `recaptcha.js` 檔案：

1. [更新 recaptcha.js 檔案中的 Google reCAPTCHA 網站金鑰](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [部署檔案並建置專案](#2-deploy-the-file-and-build-the-project)
1. [使用 AEM Sidekick 預覽網站](#3-preview-the-site-using-the-aem-sidekick)

### 更新 recaptcha.js 檔案中的 Google reCAPTCHA 網站金鑰

1. 在本機電腦上開啟對應的 GitHub 存放庫。
1. 前往 `[../Form Block/integrations]` 資料夾並開啟 `recaptcha.js` 檔案。
1. 用 Google reCAPTCHA 網站金鑰值取代 `siteKey`。

   ![Recaptcha 適用於所有表單](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  您可以從 [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin) 擷取 reCAPTCHA 金鑰。

1. 儲存 `recaptcha.js` 檔案。

### 部署檔案並建置專案

部署已更新的 `recaptcha.js` 檔案到您的 GitHub 專案，並驗證建置是否成功。

### 使用 AEM Sidekick 預覽網站

使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈網站。

您網站上的所有表單開始出現 reCAPTCHA 徽章。

