---
title: 建立產品體驗
description: 瞭解如何建立隨後可用於各種管道的產品內容，以打造沈浸式購物體驗。
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# 建立產品體驗 {#building-experiences}

瞭解如何管理產品體驗。

## 目前進度 {#story-so-far}

在Adobe Experience Manager (AEM)內容和Commerce歷程的上一份檔案[管理分階段產品目錄體驗](staged-catalog.md)中，您已瞭解如何管理分階段產品目錄體驗。

## 目標 {#objective}

本檔案可協助您瞭解如何建置產品內容和體驗。

## 產品體驗管理 {#management}

產品體驗管理是一門學科，用於在AEM中將產品資料（由PIM或商務解決方案擁有）與行銷內容一起裝飾。 然後，這些包含內容的豐富產品資料可用於各種頻道，以建立沈浸式購物體驗。

在AEM中，您可以建立各種型別的內容，並將其連結至產品目錄。 可以輕鬆探索及使用相關內容，進而提高生產力。

### Assets {#assets}

基本上，有兩種型別的資產與產品有關：產品與行銷。 產品資產由商戶管理，並專注於顯示產品（大多在中性背景前）。 資產可在商務解決方案或AEM Assets中管理(透過Assets與商務/pim解決方案的整合)。

行銷資產與促銷及使用行銷所擁有的產品有關。 例如，顯示特定內容（「戶外秋季系列」）中的多種產品（「商店外觀」）或操作說明檔案。 CIF可讓您輕鬆將任何AEM資產與產品目錄物件連結。

開啟資產屬性並切換至&#x200B;**Commerce**&#x200B;標籤。 此索引標籤可讓您管理與產品的關聯。 選取器下方的表格提供連結物件的其他資訊（只顯示選取專案）。 按一下詳細資訊圖示，您就能取得產品駕駛艙的完整檢視。 若要關聯新物件，請按一下產品選擇器圖示（資料夾圖示）、選取物件並關閉選擇器。

![pem資產](assets/pem-assets.png)

### 體驗片段 {#experience-fragments}

體驗片段是大規模建立可重複使用或個別產品內容的絕佳方式。 關聯的運作方式與資產類似。 開啟屬性並切換至&#x200B;**Commerce**&#x200B;標籤。 此索引標籤可讓您管理與產品和類別的關聯。 選取器下方的表格會提供連結物件的其他資訊（只有選取專案才可見）。 按一下詳細資訊圖示，您就能取得產品駕駛艙的完整檢視。 若要關聯新物件，請按一下產品選擇器圖示（資料夾圖示）、選取物件並關閉選擇器。

![pem xf](assets/pem-xf.png)

### 內容片段 {#content-fragments}

內容片段是任何結構化內容的最佳內容型別。 這可用來使用其他行銷資料來增強外部產品資料，或以Headless方式建立內容。 內容片段與產品目錄物件的關聯是透過內容片段模式編輯器中的產品或類別參考型別進行。 只需在模型上拖放正確的參考型別並設定欄位即可。 這些型別支援單一或多重選取。

![pem cf模型](assets/pem-cf-model.png)

如果您根據此模型建立內容片段，這些參考型別會為您提供使用各自選擇器來選取正確物件的簡單方法。

![pem cf](assets/pem-cf.png)

### 產品駕駛艙 {#product-cockpit}

您已在先前的其中一個模組中瞭解產品駕駛艙（或主控台）。 駕駛艙不僅可讓您輕鬆瀏覽產品目錄，還可讓您在一個位置檢視所有相關的AEM內容。 前往產品主控台，並開啟具有關聯內容之產品的屬性。 切換至個別標籤以檢視相關聯的內容。

![pem駕駛艙](assets/pem-cockpit.png)

按一下動作圖示即可在新的瀏覽器標籤中開啟該內容片段。

## 豐富個別產品和類別頁面 {#enrich}

在前面的單元中，您已瞭解如何使用多個產品目錄範本。 使用多個範本是建立不同範本的好方法，但通常不需要。 通常，個別內容的預留位置可搭配使用相同的範本。 CIF支援內容片段和體驗片段的預留位置。

讓我們從體驗片段預留位置開始。 在AEM編輯器中開啟產品範本。 將&#x200B;**Commerce體驗片段**&#x200B;元件拖放到範本上，然後開啟設定對話方塊。

![pem預留位置](assets/pem-placeholder.png)

開啟元件的對話方塊，並輸入此預留位置的名稱。 需要預留位置名稱，可讓您視需要新增任意數量的預留位置。

![pem XF對話方塊](assets/pem-dialog-xf.png)

開啟您在上一步中與產品相關聯的體驗片段。 開啟屬性並切換至商務標籤。 在&#x200B;**目錄預留位置位置**&#x200B;下輸入相同的預留位置名稱。

![pem xf](assets/pem-xf.png)

現在將&#x200B;**Commerce內容片段**&#x200B;元件拖放到範本上，並開啟設定對話方塊。

![pem CF對話方塊](assets/pem-dialog-cf.png)

此對話方塊會重複使用核心元件內容片段對話方塊。 如需詳細資訊，請參閱其他資源。 唯一的差異是&#x200B;**Link Element**&#x200B;屬性，它設定了內容片段模型中識別碼欄位(產品SKU或類別UID)。

現在預覽具有關聯內容片段和/或體驗片段的產品頁面。 AEM轉譯頁面時，會根據型別（內容或體驗片段）、識別碼和體驗片段的預留位置名稱來查詢每個預留位置。 AEM會使用URL解析器來取得識別碼(SKU適用於產品，UID適用於類別)。 如果傳回體驗或內容片段，則會呈現至預留位置位置，否則會忽略預留位置。

![pem結果](assets/pem-result.png)

## 讓內容可供購買 {#making-shoppable}

也可以透過新增商務元件讓一般AEM頁面可供購買。 在AEM中建立內容頁面，並在編輯器中開啟空白頁面。

![pem空白頁面](assets/pem-page-empty.png)

首先，將產品詳細資料元件拖放到頁面上。 然後切換至Assets側邊欄，切換至產品並選取產品。 將該產品拖放到產品元件上。 這會在內容頁面上顯示一般產品元件。

![pem產品頁面](assets/pem-page-product.png)

如果您已為該產品建立關聯內容，請在Assets側邊欄中切換為&#x200B;**關聯的Commerce內容**。 此索引標籤會顯示與此產品相關聯的所有AEM內容。 這可讓您現在使用任何關聯內容來快速修飾頁面。

![pem擴充頁面](assets/pem-page-enriched.png)

## 歷程結尾？ {#end-of-journey}

恭喜！您已完成AEM內容和Commerce開發人員歷程！ 您現在應該：

* 瞭解如何將任何AEM內容與產品目錄物件建立關聯
* 使用預留位置來個別豐富產品和類別頁面
* 瞭解如何讓內容可供購買，並使用關聯內容標籤

您現在已準備好使用AEM內容和Commerce來管理產品體驗。 不過AEM內容和Commerce有許多其他可用選項。 檢視[其他資源區段](#additional-resources)中提供的其他資源，瞭解更多關於您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [編寫Commerce體驗](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [產品駕駛艙](/help/commerce-cloud/authoring/product-cockpit.md)
* [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
