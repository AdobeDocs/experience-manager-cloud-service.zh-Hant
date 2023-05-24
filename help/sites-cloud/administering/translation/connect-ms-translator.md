---
title: 連線到 Microsoft Translator
description: 瞭解如何將AEM連線至現成的Microsoft Translator，以自動化您的翻譯工作流程。
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 11%

---

# 連線到 Microsoft Translator {#connecting-to-microsoft-translator}

建立「 」的設定 [Microsoft Translator](https://www.microsoft.com/en-us/translator/business/) 雲端服務，使用您的Microsoft翻譯帳戶來翻譯AEM頁面內容或資產。

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱我們的 [Sites 翻譯歷程](/help/journey-sites/translation/overview.md)，此路徑會逐步引導您了解如何使用 AEM 強大的翻譯工具翻譯 AEM Sites 內容，非常適合那些沒有 AEM 或翻譯經驗的使用者。

>[!NOTE]
>
>AEM提供試用的Microsoft翻譯帳戶，每月最多允許2,000,000個免費翻譯的字元。 若要取得足以用於生產系統的帳戶訂閱，請參閱 [升級Microsoft Translator試用授權設定](#upgrading-the-microsoft-translator-trial-license-configuration).

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱 |
| 翻譯歸因 | （選用）對於使用者產生的內容，為已翻譯文字旁邊顯示的屬性，例如 `Translations by Microsoft` |
| 工作區ID | （選用）要使用的自訂Microsoft Translator引擎ID |
| 訂閱金鑰 | 您的Microsoft Translator Microsoft訂閱金鑰 |

建立設定後，您需要 [啟動它](#activating-the-translator-service-configurations).

下列程式會建立Microsoft Translator設定。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 按一下或點選 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 導覽至您要建立設定的位置。 這通常位於您的網站根目錄中，或是全域預設設定。
1. 點選或按一下 **建立** 按鈕。
1. 定義您的設定。
   1. 選取 **Microsoft Translator** 下拉式清單中的。
   1. 輸入設定的標題。 標題會識別Cloud Services控制檯以及頁面屬性下拉式清單中的設定。
   1. 或者，輸入儲存組態的存放庫節點的名稱。

   ![建立翻譯設定](../assets/create-translation-config.png)

1. 按一下&#x200B;**建立**。
1. 在 **編輯設定** 視窗中，提供上表所述之翻譯服務的值。

   ![編輯翻譯設定](../assets/edit-translation-config.png)

1. 點選或按一下 **Connect** 以驗證連線。
1. 點選或按一下&#x200B;**儲存並關閉**。

## 升級Microsoft Translator試用授權設定 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft翻譯設定頁面提供指向Microsoft網站的便利連結，以取得足以用於生產系統的帳戶訂閱。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 點選或按一下 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下 **編輯**.
1. 在 **編輯設定** 視窗，點選或按一下 **升級訂閱**. 隨即開啟Microsoft網頁，其中包含有關服務的更多詳細資料。

## 自訂Microsoft Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，以便自訂Microsoft Translator引擎。

1. 在 [導覽面板，](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) 點選或按一下 **工具** -> **Cloud Services** -> **翻譯Cloud Services**.
1. 點選或按一下您現有的Microsoft Translator設定。
1. 點選或按一下 **編輯**.
1. 在 **編輯設定** 視窗，點選或按一下 **自訂翻譯工具**. 使用開啟的Microsoft網頁來自訂您的服務。

## 啟用翻譯人員服務設定 {#activating-the-translator-service-configurations}

您需要啟動雲端服務設定，以支援復寫至發佈執行個體的翻譯內容。 使用方法 [發佈樹狀結構](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) 以啟動儲存Microsoft Translator設定的存放庫節點。 節點位於下列父節點下方：

* `/libs/settings/cloudconfigs/translation/msft-translation`
