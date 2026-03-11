---
title: Forms as a Cloud Service適用性Forms中的HTML電子郵件範本
description: 瞭解如何搭配最適化表單使用電子郵件範本。
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
badgeSaas: label="AEM Forms" type="Positive" tooltip="適用於AEM Forms)。"
exl-id: 640130c0-e5d2-4af1-8ed9-c3bdde31d958
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 9%

---

# 最適化表單中的電子郵件範本

最適化Forms可讓您使用HTML和純文字電子郵件範本。 HTML 電子郵件範本讓您能夠在提交表單時發送內容豐富又有視覺吸引力的個人化電子郵件。這些電子郵件可以使用表單資料進行自訂，並運用各種電子郵件標籤 (例如影像和連結) 加強內容。透過最適化表單，您可以上傳包含 HTML 範本的檔案，或使用純文字編輯器來建立這些範本。

![HTML 電子郵件範本](/help/forms/assets/html-email.png)

本文可協助您在Adaptive Forms中設定和使用電子郵件範本。 到最後，您將能夠：

* [為最適化表單設定HTML範本](#configure-an-html-template-for-an-adaptive-form)
* [為最適化表單設定純文字電子郵件範本](#configure-a-plain-text-template-for-an-adaptive-form)
* [在電子郵件範本中使用表單資料](#use-form-data-in-your-email-templates)


以下為相關步驟的快速概觀：

1. 開啟最適化表單進行編輯。
1. 設定[傳送電子郵件](/help/forms/configure-submit-action-send-email.md)提交動作。
1. 選取或上傳HTML範本，或手動輸入電子郵件範本。
1. 測試您的電子郵件設定。

## 為最適化表單設定HTML範本

您可以使用&#x200B;[**傳送電子郵件**&#x200B;提交動作](/help/forms/configure-submit-action-send-email.md)，設定最適化表單以在提交時傳送電子郵件。 此動作提供設定HTML範本的兩種方法：

### 選項1：選取包含HTML範本的檔案

在繼續之前，請確定您已將HTML範本上傳至AEM Forms環境。

1. 開啟最適化表單進行編輯。
1. 移至&#x200B;**內容瀏覽器**，選取&#x200B;**節目表容器**，然後點選屬性圖示。 標題為`Adaptive Form Container`的對話方塊隨即顯示。
1. 移至&#x200B;**提交**&#x200B;標籤，並選取&#x200B;**傳送電子郵件**&#x200B;提交動作。

   ![傳送電子郵件提交動作](/help/forms/assets/send-email-action.png)

1. 啟用&#x200B;**使用外部範本**&#x200B;選項。
1. 啟用&#x200B;**使用HTML範本**&#x200B;選項。
1. 按一下「外部範本路徑」選項的資料夾圖示，並瀏覽以選取您的HTML範本。
1. 按一下&#x200B;**完成**&#x200B;以儲存組態。

您的HTML範本現在已針對最適化表單完成設定。

### 選項2：手動輸入或貼上HTML範本

1. 開啟最適化表單進行編輯。
1. 移至&#x200B;**內容瀏覽器**，選取&#x200B;**節目表容器**，然後點選屬性圖示。 標題為`Adaptive Form Container`的對話方塊隨即顯示。
1. 移至&#x200B;**提交**&#x200B;標籤，並選取&#x200B;**傳送電子郵件**&#x200B;提交動作。
1. 啟用&#x200B;**使用HTML範本**&#x200B;選項。
1. 在提供的&#x200B;**電子郵件範本**&#x200B;方塊中，直接輸入或貼上HTML程式碼。


## 為最適化表單設定純文字範本

您可以使用&#x200B;[**傳送電子郵件**&#x200B;提交動作](/help/forms/configure-submit-action-send-email.md)，設定最適化表單以在提交時傳送電子郵件。 此動作提供兩種設定純文字範本的方法：

### 選項1：選取包含範本的檔案

在繼續之前，請確定您已將HTML範本上傳至AEM Forms環境。

1. 開啟最適化表單進行編輯。
1. 移至&#x200B;**內容瀏覽器**，選取&#x200B;**節目表容器**，然後點選屬性圖示。 標題為`Adaptive Form Container`的對話方塊隨即顯示。
1. 移至&#x200B;**提交**&#x200B;標籤，並選取&#x200B;**傳送電子郵件**&#x200B;提交動作。
1. 啟用&#x200B;**使用外部範本**&#x200B;選項。
1. 按一下&#x200B;**外部範本路徑**&#x200B;選項的資料夾圖示，並瀏覽以選取您的純文字範本。
1. 按一下「完成」以儲存設定。

您的範本現在已設定為最適化表單。

### 選項2：手動輸入或貼上HTML範本

1. 開啟最適化表單進行編輯。
1. 移至&#x200B;**內容瀏覽器**，選取&#x200B;**節目表容器**，然後點選屬性圖示。 標題為`Adaptive Form Container`的對話方塊隨即顯示。
1. 移至&#x200B;**提交**&#x200B;標籤，並選取&#x200B;**傳送電子郵件**&#x200B;提交動作。
1. 直接在提供的&#x200B;**電子郵件範本**&#x200B;方塊中輸入或貼上您的純文字範本程式碼。

## 在電子郵件範本中使用表單資料

您可以使用預留位置將表單資料包含在電子郵件範本中。 在傳送電子郵件時，這些預留位置會動態取代為實際表單欄位值。 例如：

* ${name}：名為「name」的欄位值。
* ${email}：名為「email」的欄位值。
* ${message}：名為「message」的欄位值。

### HTML電子郵件範本範例

以下範例為使用表單資料預留位置的HTML電子郵件範本：

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### 純文字電子郵件範本範例

以下是純文字電子郵件範本的範例：

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

## HTML電子郵件範本的最佳作法

* 確保您的樣式內嵌，以便與電子郵件使用者端更相容。
* 讓您的範本快速回應，以便在行動裝置上獲得更好的體驗。
* 使用Litmus或Acid上的Email等工具，在各種電子郵件使用者端預覽您的電子郵件。
* 確定預留位置名稱與表單欄位名稱完全相符。
* 檢查HTML範本中是否有缺少或不正確的標籤。
* 確認[傳送電子郵件](/help/forms/configure-submit-action-send-email.md)提交動作已正確設定。
