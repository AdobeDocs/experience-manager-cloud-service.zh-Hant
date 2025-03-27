---
title: 連結檢查程式
description: 瞭解Link Checker如何協助作者，方法是在連結新增至內容時驗證連結，以及提供哪些設定選項。
feature: Operations
role: Admin
source-git-commit: cc8e242715faaef5cda25b428c315947ec3d7e06
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# 連結檢查程式 {#link-checker}

瞭解Link Checker如何協助作者，方法是在連結新增至內容時驗證連結，以及提供哪些設定選項。

## 概觀 {#overview}

內容作者不必擔心要驗證自己包含在內容中的每個連結。 連結檢查器會自動執行，以協助內容作者使用其連結，包括：

* 在新增至內容時驗證連結
* 顯示內容中所有外部連結的清單
* 執行連結轉換

連結檢查器有數個[組態選項](#configuring)，例如定義內部連結的驗證、允許驗證中省略某些連結或連結模式，以及定義連結重寫規則。

連結檢查器會驗證[內部連結](#internal)和[外部連結。](#external)

>[!NOTE]
>
>由於「連結檢查器」會檢查每個內容頁面的連結，因此「連結檢查器」可能會影響大型存放庫的效能。 在這種情況下，您可能需要[設定連結檢查器執行的頻率](#configuring)或[停用它。](#disabling)

## 內部連結檢查 {#internal}

內部連結是指向AEM存放庫中其他內容的連結。 您可以使用路徑選擇器、RTF編輯器或自訂元件來新增內部連結。 例如：

* 您建立頁面`/content/wknd/us/en/adventures/ski-touring`
* 該頁面包含[文字元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/text)中`/content/wknd/us/en/adventures/extreme-ironing`的連結。

內容作者在頁面中新增內部連結後，就會驗證該連結。 如果連結失效：

* 它會從發佈者中移除。
   * 連結本身即會被移除。
   * 連結的文字會保留。
* 它會在編寫介面中顯示為中斷連結。

![連結檢查器正在檢查內部連結](assets/link-checker-internal.png)

## 外部連結檢查 {#external}

外部連結是指AEM存放庫外部內容的連結。 可以使用RTF編輯器或使用自訂元件來新增外部連結。 例如：

* 您建立頁面`/content/wknd/us/en/adventures/ski-touring`
* 該頁面包含[文字元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/text)中`https://bunwarmerthermalunderwear.com`的連結。

系統會驗證外部連結的語法，並檢查其可用性。 此檢查會以可設定的間隔非同步完成。 如果連結檢查器發現外部連結無效：

* 它會從發佈者中移除。
   * 連結本身即會被移除。
   * 連結的文字會保留。
* 它會在編寫介面中顯示為中斷連結。

![連結檢查器正在檢查外部連結](assets/link-checker-external.png)

### 外部連結檢查器的運作方式 {#external-details}

外部連結檢查器依賴數個服務，瞭解這些服務如何運作，可協助您瞭解如何[設定連結檢查器以符合您的需求。](#configuring)

1. 每當內容作者儲存任何頁面的連結時，就會觸發事件處理常式。
1. 事件處理常式會遍歷`/content`下的所有內容，檢查新的或更新連結，並將它們新增至連結檢查器的快取。
1. **Day CQ Link Checker Service**&#x200B;會定期執行，以檢查快取中的專案是否為有效語法。
1. 然後，語法驗證的連結會出現在[外部連結檢查器視窗中。](#external-using)但是它們會處於&#x200B;**擱置中**&#x200B;狀態。
1. 然後會定期執行&#x200B;**Day CQ連結檢查器工作**，藉由進行GET呼叫來驗證連結。
1. **天CQ連結檢查器工作**&#x200B;接著會以GET呼叫的結果更新[外部連結檢查器視窗](#external-using)中的專案。

### 使用外部連結檢查程式 {#external-using}

外部連結檢查器是一個主控台，可提供AEM內容中所有外部連結的概觀。 使用外部連結檢查程式：

1. 從全域導覽中選取&#x200B;**工具** -> **網站**。
1. 選取「**外部連結檢查器**」並顯示所有外部連結的清單。

![外部連結檢查程式](assets/external-link-checker.png)

表格中的每個專案都代表Link Checker服務偵測到的外部連結。 會顯示下列欄：

* **狀態** — 連結的驗證狀態，可能是下列其中一項：
   * **有效** — 連結檢查器可存取外部連結。
   * **擱置中** — 外部連結已新增至網站內容，但尚未由連結檢查器驗證。
   * **無效** — 連結檢查器無法存取外部連結。
* **URL** — 外部連結
* **反向連結** — 包含外部連結的內容頁面
   * 若已設定，則僅填入[。](#configuring)
* **上次檢查時間** — 連結檢查器上次驗證外部連結的時間
   * 可設定檢查連結的頻率[。](#configuring)
* **上次狀態** — 連結檢查上次檢查外部連結時傳回的最後一個HTML狀態代碼
* **上次可用** — 連結檢查器上次使用連結後的時間
* **上次存取** — 自上次在編寫介面中存取含有外部連結的頁面以來的時間

您可以使用連結清單頂端的兩個按鈕來控制視窗的內容：

* **重新整理** — 重新整理清單的內容
* **檢查** — 檢查清單中選取的個別外部連結

「外部連結檢查器」視窗中的所有其他圖示皆為非作用中。

## 設定連結檢查器 {#configuring}

「連結檢查器」可在AEM中自動使用並立即可用。 不過，有數個OSGi設定可以修改以變更其行為：

* **天CQ連結檢查器資訊儲存服務** — 此服務會定義存放庫中連結檢查器快取的大小。
* **Day CQ Link Checker Service** — 此服務會執行外部連結語法的非同步檢查。
   * 您可以定義檢查期間，以及檢查器會略過哪些型別的連結，還有其他選項。
* **天CQ連結檢查器工作** — 此服務會執行外部連結的GET驗證。
   * 它允許間隔的單獨定義，以檢查其他選項中的壞連結和好連結。
* **天CQ連結檢查器轉換器** — 此服務會根據使用者定義的規則集轉換連結。

如需有關如何變更OSGi設定的詳細資訊，請參閱檔案[設定OSGi](/help/implementing/deploying/configuring-osgi.md)。

## 停用連結檢查器 {#disabling}

您可以選擇完全停用連結檢查器。 若要這麼做：

1. 開啟OSGi主控台。
1. 編輯&#x200B;**天CQ連結檢查器轉換器**
1. 勾選您要停用的選項：
   * **停用檢查** — 停用連結驗證
   * **停用重新寫入** — 停用連結轉換
