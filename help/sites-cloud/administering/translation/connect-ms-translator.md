---
title: 連接到Microsoft Translator
description: 了解如何將AEM立即連線至Microsoft Translator，以自動執行翻譯工作流程。
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 連接到Microsoft Translator {#connecting-to-microsoft-translator}

為 [Microsoft翻譯](https://www.microsoft.com/en-us/translator/business/) 雲端服務，以使用您的Microsoft翻譯帳戶來轉譯AEM頁面內容或資產。

>[!TIP]
>
>如果您是初次翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 這是使用AEM功能強大的翻譯工具來轉譯您的AEM Sites內容的引導式路徑，最適合沒有AEM或翻譯體驗的人。

>[!NOTE]
>
>AEM提供試用的Microsoft翻譯帳戶，每月最多可允許2 000 000個免費翻譯字元。 若要取得適用於生產系統的帳戶訂閱，請參閱 [升級Microsoft Translator試用版許可證配置](#upgrading-the-microsoft-translator-trial-license-configuration).

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選用）針對使用者產生的內容，例如顯示在翻譯文字旁的歸因 `Translations by Microsoft` |
| 工作區ID | （選用）您要使用的自訂Microsoft轉譯器引擎ID |
| 訂閱金鑰 | 您的Microsoft TranslatorMicrosoft訂閱密鑰 |

建立設定後，您需要 [啟動](#activating-the-translator-service-configurations).

以下過程將建立Microsoft Translator配置。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 按一下或點選 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 導覽至您要建立設定的位置。 這通常位於您的網站根目錄中，或可以是全域的預設設定。
1. 點選或按一下 **建立** 按鈕。
1. 定義您的設定。
   1. 選擇 **Microsoft翻譯** 中。
   1. 輸入您設定的標題。 標題會在「Cloud Services」主控台以及頁面屬性下拉式清單中識別設定。
   1. （可選）鍵入用於儲存配置的儲存庫節點的名稱。

   ![建立翻譯配置](../assets/create-translation-config.png)

1. 按一下&#x200B;**建立**。
1. 在 **編輯配置** 窗口，提供上表中所述的轉換服務的值。

   ![編輯翻譯配置](../assets/edit-translation-config.png)

1. 點選或按一下 **Connect** 來驗證連接。
1. 點選或按一下 **儲存並關閉**.

## 升級Microsoft Translator試用版許可證配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，以取得適用於生產系統的帳戶訂閱。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 點選或按一下 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下 **編輯**.
1. 在 **編輯配置** 視窗，點選或按一下 **升級訂閱**. 隨即開啟Microsoft網頁，內含服務的詳細資訊。

## 自訂您的Microsoft Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，可自訂您的Microsoft翻譯引擎。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 點選或按一下 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下 **編輯**.
1. 在 **編輯配置** 視窗，點選或按一下 **自定義翻譯器**. 使用開啟的Microsoft網頁來自訂您的服務。

## 激活轉換器服務配置 {#activating-the-translator-service-configurations}

您需要啟動雲端服務設定，以支援複製到發佈執行個體的翻譯內容。 使用 [發佈樹](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) 激活儲存Microsoft Translator配置的儲存庫節點。 節點位於以下父節點下：

* `/libs/settings/cloudconfigs/translation/msft-translation`
