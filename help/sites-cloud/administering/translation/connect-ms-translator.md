---
title: 連接到Microsoft Translator
description: 瞭解如AEM何立即連接至Microsoft Translator以自動化您的翻譯工作流程。
feature: Language Copy
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# 連接到Microsoft Translator {#connecting-to-microsoft-translator}

為[Microsoft Translator](https://hub.microsofttranslator.com)雲端服務建立組態，以使用您的Microsoft Translation帳戶來轉換頁AEM面內容或資產。

>[!NOTE]
>
>提AEM供試用版Microsoft Translation帳戶，每個月最多允許2 000 000個免費翻譯字元。 要獲得適合生產系統的帳戶訂閱，請參閱[升級Microsoft Translator試用版許可證配置](#upgrading-the-microsoft-translator-trial-license-configuration)。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選擇性）對於使用者產生的內容，顯示在翻譯文字旁的歸因，例如`Translations by Microsoft` |
| 工作區ID | （可選）您要使用的自訂Microsoft Translator引擎ID |
| 訂閱金鑰 | 您的Microsoft Translator訂閱金鑰 |

建立配置後，需要[激活它](#activating-the-translator-service-configurations)。

以下過程建立Microsoft Translator配置。

1. 在[導航面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)按一下或點選&#x200B;**工具** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 導覽至您要建立設定的位置。 通常，這位於您的網站根目錄中，或可以是全域的預設設定。
1. 點選或按一下&#x200B;**Create**&#x200B;按鈕。
1. 定義您的設定。
   1. 在下拉清單中選擇&#x200B;**Microsoft Translator**。
   1. 輸入您設定的標題。 此標題可識別Cloud Services控制台和頁面屬性下拉式清單中的設定。
   1. （可選）鍵入用於儲存配置的儲存庫節點的名稱。

   ![建立翻譯配置](../assets/create-translation-config.png)

1. 按一下&#x200B;**建立**。
1. 在&#x200B;**編輯配置**&#x200B;窗口中，提供上表中所述的翻譯服務值。

   ![編輯翻譯配置](../assets/edit-translation-config.png)

1. 點選或按一下&#x200B;**Connect**&#x200B;以驗證連接。
1. 點選或按一下「儲存並關閉」**。**

## 升級Microsoft Translator試用版許可證配置{#upgrading-the-microsoft-translator-trial-license-configuration}

「Microsoft翻譯」配置頁提供了指向Microsoft網站的方便連結，以便獲得適合生產系統的帳戶訂閱。

1. 在[導航面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)點選或按一下&#x200B;**工具** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下「編輯&#x200B;**」。**
1. 在&#x200B;**編輯配置**&#x200B;窗口中，按一下或按一下&#x200B;**升級訂閱**。 隨即開啟Microsoft網頁，其中包含服務的詳細資訊。

## 自定義Microsoft Translator引擎{#customizing-your-microsoft-translator-engine}

「Microsoft翻譯配置」頁提供了指向Microsoft網站的方便連結，用於自定義Microsoft Translator引擎。

1. 在[導航面板中，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps)點選或按一下&#x200B;**工具** -> **Cloud Services** -> **翻譯Cloud Services**。
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下「編輯&#x200B;**」。**
1. 在&#x200B;**編輯配置**&#x200B;窗口中，按一下或按一下&#x200B;**自定義轉換器**。 使用開啟的Microsoft網頁自訂您的服務。

## 激活Translator服務配置{#activating-the-translator-service-configurations}

您需要啟用雲端服務設定，以支援複製至發佈例項的翻譯內容。 使用[發佈樹](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法激活儲存Microsoft Translator配置的儲存庫節點。 節點位於以下父節點下：

* `/libs/settings/cloudconfigs/translation/msft-translation`
