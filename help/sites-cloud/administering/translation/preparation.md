---
title: 準備翻譯內容
description: 瞭解在開發多語言網站時如何準備翻譯內容。
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# 準備翻譯內容 {#preparing-content-for-translation}

多語言網站通常以多種語言提供一定數量的內容。 網站是以一種語言撰寫，然後翻譯成其他語言。 通常，多語言網站是由頁面分支組成，每個分支都包含不同語言的網站頁面。

>[!TIP]
>
>如果不熟悉如何翻譯內容，請參閱[網站翻譯歷程](/help/journey-sites/translation/overview.md)，此歷程將引導您使用AEM強大的翻譯工具來翻譯您的AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

[WKND教學課程網站](/help/implementing/developing/introduction/develop-wknd-tutorial.md)包含數個語言分支，並使用下列結構：

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

您最初為其創作網站內容的語言副本是語言主要版本。 語言母版是翻譯成其他語言的來源。

網站的每個語言分支都稱為語言副本。 語言副本的根頁面（稱為語言根）可識別語言副本中的內容語言。 例如，`/content/wknd/fr`是法語副本的語言根。 語言副本必須使用[正確設定的語言根](preparation.md#creating-a-language-root)，以便在翻譯來源網站時鎖定正確的語言。

使用下列步驟來準備您的網站以進行翻譯：

1. 建立語言主版的語言根。 例如，英文WKND示範網站的語言根為`/content/wknd/language-masters/en`。 請確定已根據[建立語言根](preparation.md#creating-a-language-root)中的資訊正確設定語言根。
1. 編寫語言主版的內容。
1. 建立網站每個語言副本的語言根。 例如，WKND範例網站的法文復本為`/content/wknd/language-masters/fr`。

準備要翻譯的內容後，您可以在語言副本和相關翻譯專案中自動建立遺失的頁面。 （請參閱[建立翻譯專案](managing-projects.md)。）如需AEM內容翻譯程式的概述，請參閱[翻譯多語言網站的內容](overview.md)。

## 建立語言根目錄 {#creating-a-language-root}

建立語言根作為識別內容語言的語言副本的根頁面。 建立語言根之後，您可以建立包含語言副本的翻譯專案。

若要建立語言根，請建立頁面，並使用ISO語言代碼作為&#x200B;**Name**&#x200B;屬性的值。 語言程式碼必須是下列其中一種格式：

* `<language-code>` — 支援的語言程式碼是由ISO-639-1定義的雙字母程式碼，例如`en`。
* `<language-code>_<country-code>`或`<language-code>-<country-code>` — 支援的國家代碼是ISO 3166定義的小寫或大寫兩字母代碼，例如，`en_US`、`en_us`、`en_GB`、`en-gb`。

根據您為全域網站選擇的結構，您可以使用任一格式。 例如，WKND網站法文副本的根頁面有`fr`做為&#x200B;**Name**&#x200B;屬性。 **Name**&#x200B;屬性是做為存放庫中頁面節點的名稱，因此會決定頁面的路徑(`http://<host>:<4502>/content/wknd/language-masters/fr.html`)。

1. 導覽至網站。
1. 選取您要建立語言副本的網站。
1. 選取&#x200B;**建立**，然後選取&#x200B;**頁面**。

   ![建立頁面](../assets/create-page.png)

1. 選取頁面範本，然後選取&#x200B;**下一步**。
1. 在&#x200B;**名稱**&#x200B;欄位中，以`<language-code>`或`<language-code>_<country-code>`的格式輸入國家/地區代碼，例如，`en`，`en_US`，`en_us`，`en_GB`，`en_gb`。 輸入頁面的標題。

   ![建立語言根頁面](../assets/create-language-root.png)

1. 選擇 **建立**。在確認對話方塊中，選取&#x200B;**完成**&#x200B;以返回Sites主控台，或選取&#x200B;**開啟**&#x200B;以開啟語言副本。

## 檢視語言根的狀態 {#seeing-the-status-of-language-roots}

AEM提供&#x200B;**參考**&#x200B;邊欄，顯示已建立的語言根清單。

![語言根](../assets/language-roots.png)

請使用[邊欄選取器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)來檢視頁面的語言復本，步驟如下。

1. 在網站主控台上，選取網站的頁面，然後選取&#x200B;**參照**。

   ![開啟參考邊欄](../assets/opening-references-rail.png)

1. 在參考邊欄中，選取&#x200B;**語言副本**。 邊欄會顯示網站的語言副本。

## 多個層級的語言副本 {#multiple-levels}

語言根也可以在節點下分組（例如，按區域），同時仍被識別為語言副本的根。

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
>只允許一個層級。 例如，下列專案不允許`es`頁面解析為語言副本：
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> 將不會偵測到此`es`語言副本，因為它與`en`節點相差2個層級(`americas/central-america`)。

>[!TIP]
>
>在此類設定中，語言根可以有任何頁面名稱，而不僅僅是語言的ISO程式碼。 AEM一律會先檢查路徑和名稱，但如果頁面名稱未識別語言，AEM會檢查頁面的`cq:language`屬性以取得語言識別。
