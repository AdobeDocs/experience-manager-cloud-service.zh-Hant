---
title: 連接到Microsoft Translator
description: 了解如何將AEM連接至Microsoft Translator的現成可用功能，以自動執行翻譯工作流程。
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# 連接到Microsoft Translator {#connecting-to-microsoft-translator}

為[Microsoft Translator](https://hub.microsofttranslator.com)雲服務建立配置，以使用您的Microsoft翻譯帳戶來轉譯AEM頁面內容或資產。

>[!TIP]
>
>如果您是翻譯內容的新手，請參閱我們的[網站翻譯歷程](/help/journey-sites/translation/overview.md)，該路徑是使用AEM功能強大的翻譯工具來翻譯您的AEM Sites內容的引導路徑，最適合沒有AEM或翻譯經驗的人。

>[!NOTE]
>
>AEM提供試用版Microsoft翻譯帳戶，每月最多可允許2 000 000個免費翻譯字元。 要獲取適合生產系統的帳戶訂閱，請參閱[升級Microsoft Translator試用許可證配置](#upgrading-the-microsoft-translator-trial-license-configuration)。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選用）針對使用者產生的內容，顯示在翻譯文字旁的歸因，例如`Translations by Microsoft` |
| 工作區ID | （可選）要使用的自定義Microsoft Translator引擎的ID |
| 訂閱金鑰 | Microsoft Translator的Microsoft訂閱密鑰 |

建立設定後，您需要[啟動它](#activating-the-translator-service-configurations)。

以下過程將建立Microsoft Translator配置。

1. 在[導覽面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)按一下或點選&#x200B;**Tools** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 導覽至您要建立設定的位置。 這通常位於您的網站根目錄中，或可以是全域的預設設定。
1. 點選或按一下&#x200B;**Create**&#x200B;按鈕。
1. 定義您的設定。
   1. 在下拉清單中選擇&#x200B;**Microsoft Translator**。
   1. 輸入您設定的標題。 標題會在「Cloud Services」主控台以及頁面屬性下拉式清單中識別設定。
   1. （可選）鍵入用於儲存配置的儲存庫節點的名稱。

   ![建立翻譯配置](../assets/create-translation-config.png)

1. 按一下&#x200B;**建立**。
1. 在&#x200B;**編輯配置**&#x200B;窗口中，提供上表中描述的翻譯服務的值。

   ![編輯翻譯配置](../assets/edit-translation-config.png)

1. 點選或按一下&#x200B;**連線**&#x200B;以驗證連線。
1. 點選或按一下「**儲存並關閉**」。

## 升級Microsoft Translator試用許可證配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft翻譯配置頁提供了指向Microsoft網站的便利連結，以便獲得適用於生產系統的帳戶訂閱。

1. 在[導覽面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)點選或按一下&#x200B;**Tools** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 點選或按一下您現有的Microsoft Translator配置。
1. 點選或按一下「**編輯**」。
1. 在&#x200B;**Edit Configuration**&#x200B;視窗中，點選或按一下&#x200B;**Upgrade Subscription**。 隨即開啟Microsoft網頁，其中包含有關該服務的更多詳細資訊。

## 自定義Microsoft Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft翻譯配置頁提供了指向Microsoft網站的便利連結，用於自定義您的Microsoft翻譯引擎。

1. 在[導覽面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)點選或按一下&#x200B;**Tools** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 點選或按一下您現有的Microsoft Translator配置。
1. 點選或按一下「**編輯**」。
1. 在&#x200B;**編輯配置**&#x200B;窗口中，點選或按一下&#x200B;**自定義轉換器**。 使用開啟的Microsoft網頁自定義您的服務。

## 激活轉換器服務配置 {#activating-the-translator-service-configurations}

您需要啟動雲端服務設定，以支援複製到發佈執行個體的翻譯內容。 使用[發佈樹](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法激活儲存Microsoft Translator配置的儲存庫節點。 節點位於以下父節點下：

* `/libs/settings/cloudconfigs/translation/msft-translation`
