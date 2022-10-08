---
title: 準備翻譯內容
description: 了解如何準備翻譯內容。
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# 準備翻譯內容 {#preparing-content-for-translation}

多語言網站通常提供多種語言的內容。 網站以一種語言編寫，然後翻譯成其他語言。 一般而言，多語言網站是由頁面的分支所組成，每個分支都包含不同語言的網站頁面。

>[!TIP]
>
>如果您是初次翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 這是使用AEM功能強大的翻譯工具來轉譯您的AEM Sites內容的引導式路徑，最適合沒有AEM或翻譯體驗的人。

此 [WKND教學課程網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 包含數個語言分支，且使用下列結構：

```text
/content
    |- wknd
        |- language-masters
            |- en
            |- de
            |- es
            |- fr
            |- it
        |- us
            |- en
            |- es
        |- ca
            |- en
            |- fr
        |- ch
            |- de
            |- fr
            |- it
        |- de
            |- de
        |- fr
            |- fr
        |- es
            |- es
        |- it
            |- it
```

您最初製作網站內容的語言副本是語言主版。 語言主版是翻譯成其他語言的源。

網站的每個語言分支都稱為語言副本。 語言副本的根頁面（稱為語言根）可識別語言副本中內容的語言。 例如， `/content/wknd/fr` 是法文語言副本的語言根。 語言副本必須使用 [正確配置的語言根](preparation.md#creating-a-language-root) 以便在執行源站點的翻譯時定位正確的語言。

使用下列步驟準備您的網站以進行翻譯：

1. 建立語言主版的語言根。 例如，英文WKND示範網站的語言根目錄為 `/content/wknd/language-masters/en`. 請根據 [建立語言根](preparation.md#creating-a-language-root).
1. 編寫您的語言主版的內容。
1. 為網站建立每個語言副本的語言根目錄。 例如， WKND示例站點的法文語言副本為 `/content/wknd/language-masters/fr`.

在準備翻譯內容後，您可以自動在語言副本和相關翻譯專案中建立遺漏的頁面。 (請參閱 [建立翻譯專案](managing-projects.md).) 如需AEM中內容翻譯程式的概觀，請參閱 [轉譯多語言網站的內容](overview.md).

## 建立語言根 {#creating-a-language-root}

建立語言根作為標識內容語言的語言副本的根頁。 建立語言根後，您可以建立包含語言副本的翻譯專案。

要建立語言根目錄，請建立頁面，並使用ISO語言代碼作為 **名稱** 屬性。 語言代碼必須為以下格式之一：

* `<language-code>`  — 支援的語言代碼是ISO-639-1所定義的雙字母代碼，例如 `en`.
* `<language-code>_<country-code>` 或 `<language-code>-<country-code>`  — 支援的國家/地區代碼是ISO 3166定義的小寫或大寫雙字母代碼，例如 `en_US`, `en_us`, `en_GB`, `en-gb`.

您可以根據您為全域網站選擇的結構，使用任一格式。 例如， WKND網站的法文語言副本的根頁面具有 `fr` 作為 **名稱** 屬性。 請注意， **名稱** 屬性會作為存放庫中頁面節點的名稱，因此會決定頁面的路徑(`http://<host>:<4502>/content/wknd/language-masters/fr.html`)。

1. 導覽至網站。
1. 按一下或點選您要建立語言副本的網站。
1. 按一下或點選 **建立**，然後按一下或點選 **頁面**.

   ![建立頁面](../assets/create-page.png)

1. 選取頁面範本，然後按一下或點選 **下一個**.
1. 在 **名稱** 欄位以 `<language-code>` 或 `<language-code>_<country-code>`，例如 `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. 輸入頁面標題。

   ![建立語言根頁面](../assets/create-language-root.png)

1. 按一下或點選 **建立**. 在確認對話方塊中，按一下或點選任一 **完成** 返回Sites控制台，或 **開啟** 以開啟語言副本。

## 看語言根的狀態 {#seeing-the-status-of-language-roots}

AEM提供 **參考** 此邊欄會顯示已建立的語言根清單。

![語言根](../assets/language-roots.png)

使用以下過程查看頁面的語言副本，使用 [邊欄選取器。](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

1. 在網站主控台上，選取網站的頁面，然後按一下或點選 **參考**.

   ![開啟參照邊欄](../assets/opening-references-rail.png)

1. 在參照邊欄中，按一下或點選 **語言副本**. 邊欄會顯示網站的語言副本。

## 多級語言副本 {#multiple-levels}

語言根也可以分組在節點下，例如按區域分組，同時仍被識別為語言副本的根。

```text
/content
    |- wknd
        |- language-masters
            |- europe
                |- de
                |- fr
                |- it
                |- es
                ]- pt
            |- americas
                |- en
                |- es
                |- fr
                |- pt
            |- asia
                |- ...
            |- africa
                |- ...
            |- oceania
                |- ...
        |- europe
        |- americas
        |- asia
        |- africa
        |- oceania            
```

>[!NOTE]
>
>只允許一個級別。 例如，下列項目不允許 `es` 頁面，以解析為語言副本：
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> 此 `es` 語言副本為2級時，將不被檢測到(`americas/central-america`)離開 `en` 節點。

>[!TIP]
>
>在此設定中，語言根可以有任何頁面名稱，而不只是語言的ISO代碼。 AEM一律會先檢查路徑和名稱，但如果頁面名稱未識別語言，AEM會檢查 `cq:language` 語言標識的頁的屬性。
