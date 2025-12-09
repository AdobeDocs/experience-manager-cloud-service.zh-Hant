---
title: 建立互動式通訊
description: 建立個人化、資料導向的通訊。 透過指南和教學課程，探索主要功能、上線步驟和真實使用案例。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: c23145c9-078d-4b03-a8f4-2d835cdd1592
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 11%

---


# 建立互動式通訊

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的提示、範例和最佳做法可能會有所變更。

互動式通訊可讓您建立、管理和提供個人化和互動式通訊，包括客戶服務、帳單、入門檔案、優惠信函、帳戶更新等。 其設計可支援動態、使用者特定內容可提升各產業通訊體驗的任何案例。

假設您需要將銀行對帳單、保單或公用程式帳單傳送給數千名客戶。 每一個都具有相同的配置，但個人化資料。 互動式通訊(IC)讓這成為可能。

![尋找IC檔案](/help/forms/interactive-communication/assets/introduction.png)

手動製作這些檔案可能很耗時，而且經常會導致不一致，尤其是在需要個人化和資料整合時。 使用互動式通訊編輯器，使用者可以簡化建立互動式通訊的程式。

## 必備條件

* [確定作者是forms-users群組的成員](/help/forms/setup-forms-cloud-service.md#configure-users)

## 建立互動式通訊

根據所需的重複使用和資料整合等級，從不同的情境中選擇建立互動式通訊：

+++ 建立空白的互動式通訊

建立空白的互動式通訊可讓您從頭開始，最適合您要完整控制版面、結構和邏輯的情況。
要遵循的步驟：

1. 開啟您的&#x200B;**Adobe Experience Manager (AEM) Forms as a Cloud Service執行個體**。
1. 導覽至&#x200B;**Forms > Forms與檔案**。
1. 按一下&#x200B;**建立>互動式通訊**。

   ![尋找IC檔案](/help/forms/interactive-communication/assets/comm.png)

1. 在建立畫面中，將&#x200B;**範本**&#x200B;欄位保留空白。

   ![尋找IC檔案](/help/forms/interactive-communication/assets/create-ic-document.png)

1. 填寫其他詳細資訊，如標題、名稱、作者等。
1. 按一下&#x200B;**建立**&#x200B;進入互動式通訊編輯器UI並開始設計。
1. 它會開啟IC編輯器，您可以在其中開始設計通訊。
+++

+++ 建立範本式互動式通訊

使用範本可重複使用一致的版面配置元素（例如頁首、頁尾、標誌或標準格式），有助於加速設計。
範本可確保品牌一致性，並節省常用通訊型別的時間。 執行以下步驟：

1. 開啟AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**Forms > Forms &amp; Documents**，按一下&#x200B;**建立>互動式通訊**。
1. 在建立表單中，從下拉式清單中&#x200B;**選取**&#x200B;已啟用的範本。
1. 填寫其他詳細資訊，如標題、名稱、作者等。
1. 按一下[建立]&#x200B;**來設計您與所選範本結構的通訊。**
1. 它會開啟IC編輯器，您可以在其中開始設計通訊。
+++

+++ 建立資料互動式通訊

資料互動式通訊會使用後端資料自動個人化內容。
適用於結構不變，但資料依收件者而異，對帳單、發票或通知的理想選擇。 要遵循的步驟：

1. 開啟AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**Forms > Forms &amp; Documents**，按一下&#x200B;**建立>互動式通訊**。
1. 在&#x200B;**表單資料模型**&#x200B;欄位中，連結您預先定義的&#x200B;**FDM （表單資料模型）**。
1. 填寫其他詳細資訊，如標題、名稱、作者等。
1. 在編輯器內使用&#x200B;**資料模型**，將欄位繫結到動態資料（例如客戶名稱、餘額、帳號）。
1. 使用&#x200B;**內容區域、子表單**&#x200B;和&#x200B;**片段**&#x200B;來建構並視需要重複資料。
1. 使用&#x200B;**PDF預覽**&#x200B;預覽，並完成傳遞的通訊。
1. 它會開啟IC編輯器，您可以在其中開始設計通訊。

![尋找IC檔案](/help/forms/interactive-communication/assets/ic-ui.png)
+++

開始建立互動式通訊，以簡化工作流程，並提供有影響力的使用者特定體驗。

## 後續步驟

[建立互動式通訊範本](/help/forms/interactive-communication/create-interactive-communication-template.md)
[建立互動式通訊片段](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
