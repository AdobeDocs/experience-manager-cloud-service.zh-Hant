---
title: 使用AEM建立Campaign電子報
description: 了解如何使用AEMas a Cloud Service建立可與Adobe Campaign Classic一併傳送的電子報。
feature: Authoring
role: User
exl-id: 60a6a9d0-f5e6-424f-b320-dd4943c55d45
source-git-commit: 6196f3fc67dbcfe03a71bb6a0796dd5d1d0f8546
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---


# 使用AEM建立Campaign電子報 {#creating-newsletters}

在本檔案中，您將學習如何使用AEM as a Cloud Service建立可與Adobe Campaign Classic一併傳送的電子報。

運用AEM as a Cloud Service與Adobe Campaign Classic之間的整合，您就可以使用AEM功能強大的製作工具來建立電子報。 當您準備好傳送電子報時，可以使用Campaign的收件者管理和發佈功能來傳送。

## 必備條件 {#prerequisites}

您必須先透過AEM建立電子報並透過Campaign傳送，才能 [整合Adobe Campaign Classic和AEMas a Cloud Service。](/help/sites-cloud/integrating/integrating-campaign-classic.md)

## 建立電子報結構 {#create-structure}

電子報內容在AEM中的管理方式與您管理網站內容的方式相同。 首先，您需建立「網站」以保留內容。 在此「網站」中，您可以依品牌收集電子報。

1. 登入您的AEM製作例項。

1. 從主導覽頁面，開啟 **網站** 控制台。

1. 在標準的AEM安裝中，會有現有 **行銷活動** 檔案夾。 選取它，然後按一下 **建立** 按鈕，然後 **頁面**.

   ![建立頁面](assets/create-page.png)

1. 選擇 **品牌** 作為網站範本，請按一下 **下一個**.

   ![建立品牌](assets/create-brand.png)

1. 輸入 **標題** 按一下 **建立** 然後 **完成**.

   ![提供品牌詳細資訊](assets/create-brand-page.png)

您現在擁有基本的內容結構可建立您的行銷活動。

![內容結構](assets/content-structure.png)

## 建立行銷活動 {#create-campaign}

現在，您已有行銷活動的基本內容結構，您可以建立行銷活動本身。 促銷活動將用來組織可能多份電子報。

1. 使用 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在sites console中，選取您先前建立的品牌(在此例中為 **WKND Escapes**)，然後選取 **主區域**，系統會自動為您建立，然後按一下 **建立** 按鈕，然後 **頁面**.

   ![建立促銷活動頁面](assets/create-campaign-page.png)

1. 選擇 **行銷活動** 作為範本，然後按一下 **下一個** 和 **完成**.

   ![選擇促銷活動範本](assets/select-campaign-template.png)

1. 輸入 **標題** 促銷活動，然後按一下 **建立** 和 **完成**.

   ![行銷活動標題](assets/campaign-title.png)

您現在有一個行銷活動，可以在其中建立商務通訊。

![行銷活動結構](assets/campaign-structure.png)

## 選取促銷活動設定 {#campaign-configuration}

AEM可支援多個整合設定。 對於您的新促銷活動，您必須定義用於傳送電子報內容的設定。

1. 使用 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在sites console中，尋找您先前建立的促銷活動(在此例中， **WKND逃生夏季運動**)，然後使用核取方塊選取，然後按一下 **屬性** 按鈕。

   ![選擇促銷活動](assets/select-campaign.png)

1. 在 **屬性** ，選擇 **Cloud Service** 標籤來定義要與此促銷活動搭配使用的整合。

   * 選擇 **Adobe Campaign** 從 **Cloud Service配置** 下拉式清單。
   * 從中選取所需的Adobe Campaign整合設定 **Adobe Campaign** 下拉式清單。
   * 按一下&#x200B;**「儲存並關閉」**。

   ![促銷活動設定屬性](assets/campaign-configuration-properties.png)

您的促銷活動現在已連結至Adobe Campaign整合。 您已準備好在AEM中建立電子報，並與Adobe Campaign一併傳送。

## 建立電子報 {#create-newsletter}

您可以在已建立和設定的促銷活動內容結構下，建立和管理電子報。

1. 使用 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在sites console中，尋找您先前設定的促銷活動(在此例中， **WKND逃生夏季運動**)，選取它，然後按一下 **建立** 按鈕，然後 **頁面**.

   ![建立電子報](assets/create-newsletter.png)

1. 在建立頁面精靈中，選取 **Adobe Campaign電子郵件(AC 6.1)** 範本，按一下 **下一個**.

   ![選取行銷活動電子郵件範本](assets/adobe-campaign-email-template.png)

1. 若 **屬性** 在精靈的步驟中，輸入 **標題** 若為電子報，請按一下 **建立** 和 **開啟**.

   ![電子報標題](assets/create-newsletter-wizard-properties.png)

1. 編輯電子報頁面，如同編輯任何其他AEM內容頁面，以符合您的需求。

您現在已有電子報可隨Adobe Campaign傳送。

## 發佈電子報 {#publishing-newsletter}

您必須發佈電子報，才能供Adobe Campaign傳送。

1. 使用 [欄檢視](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在sites console中，尋找您先前建立的電子報(在此例中為 **WKND逃生夏季活動首份快訊**)，選取它，然後按一下 **頁面資訊** 按鈕，然後按一下 **發佈頁面**.

1. 選取應發佈頁面的設定，然後按一下 **發佈**.

   ![發佈頁面](assets/publish.png)

電子報頁面現在已發佈至AEM發佈執行個體，且會顯示在Adobe Campaign Classic中。 若要在Adobe Campaign中選取，必須獲得核准。

1. 按一下 **頁面資訊** 按鈕，再次選擇 **開始工作流程**.

1. 選擇 **核准Adobe Campaign** 作為工作流模型（可選），然後按一下 **開始工作流程** 按鈕。

   ![開始工作流程](assets/start-workflow.png)

1. 電子報頁面編輯器頂端會顯示橫幅，提供核准程式中的後續步驟。 按一下 **完成**.

   ![核准工作流程](assets/approve-workflow.png)

1. 在 **完成工作項** 對話框，選擇 **新聞稿審閱（管理員）** 在 **下一步** 下拉式清單，然後按一下 **確定** 按鈕。

   ![電子報審核](assets/newsletter-review.png)

1. 在電子報頁面編輯器頂端顯示的橫幅中，再按一下 **完成**.

1. 在 **完成工作項** 對話框，選擇 **電子報核准** 在 **下一步** 下拉式清單，然後按一下 **確定** 按鈕。

   ![電子報核准](assets/newsletter-approval.png)

1. 對話方塊關閉時，出現在電子報頁面編輯器頂端的橫幅會消失，因為核准工作流程已完成。

電子報現在已在AEM中發佈，且已核准在Adobe Campaign中使用。

>[!TIP]
>
>此處會簡化描述的工作流程步驟，以說明此程式。 在正常的工作流程中，建立新聞稿並核准其通常是不同的角色
>
>請參閱檔案 [使用工作流程](/help/sites-cloud/authoring/workflows/overview.md) 如需使用工作流程的詳細資訊。

## 建立收件者 {#creating-recipient}

若要傳送您在AEM中建立的電子報，您必須先在Adobe Campaign Classic中定義收件者。

1. 使用用戶端主控台登入Adobe Campaign Classic。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導覽至 **設定檔與目標** -> **收件者** 節點。

   ![收件者](assets/recipients.png)

1. 按一下 **新增** ，並提供收件者的詳細資訊。

   * 名字
   * 姓氏
   * 電子郵件地址

1. 按一下「**儲存**」。

您現在有收件者，可以透過Adobe Campaign Classic傳送電子報。

## 建立電子郵件傳送 {#create-delivery}

最後一步是將您在AEM中建立的電子報傳送給您在Adobe Campaign Classic中新增的收件者。

1. 使用用戶端主控台登入Adobe Campaign Classic。

1. 選擇 **工具** -> **瀏覽器** 的上界。

1. 在瀏覽器中，導覽至 **Campaign Management** -> **傳遞** 節點，按一下 **新增**.

   ![AEM內容傳送](assets/delivery-aem-content.png)

1. 在 **傳送** 對話框，選擇 **使用AEM內容傳送電子郵件** 作為 **傳遞範本** 從下拉式清單中，按一下 **繼續**.

   ![AEM內容傳送](assets/aem-content-delivery.png)

1. 在 **電子郵件參數** 區段，按一下 **從** 連結並輸入發件人的資訊，然後按一下 **確定**.

   * 寄件者地址
   * 從欄位

   ![從欄位定義](assets/delivery-from.png)

1. 在 **電子郵件參數** 區段，按一下 **結束日期** 連結以開啟 **選擇目標** 對話方塊，然後按一下 **新增**.

   ![選擇目標](assets/select-target.png)

1. 在 **選取目標元素** 對話框，選擇 **收件者** 按一下 **下一個**.

   ![選取目標元素](assets/select-target-element.png)

1. 使用篩選器，選取您的收件者 [建立先前](#creating-recipient) 按一下 **完成**.

   ![選擇收件者](assets/select-target-element-recipient.png)

1. 回到 **選擇目標** 對話框，按一下 **確定**.

1. 在傳送視窗中，按一下 **同步**.

   ![同步](assets/synchronize.png)

1. 在 **與AEM內容同步** 對話方塊，從清單中選取您先前建立的電子報，按一下 **確定**.

1. Adobe Campaign的電子郵件內容會與您在AEM中建立的電子報內容同步。

   * 按一下 **重新整理內容** 如果內容未自動載入。

1. 按一下 **傳送** 以傳送電子郵件。

1. 在 **傳送至主要傳送目標** 對話框，選擇 **盡快交付** 然後按一下 **分析**.

   ![傳遞分析](assets/delivery-analysis.png)

1. 分析步驟會建立傳遞，將內容與收件者結合。 現在已建立傳送，請按一下 **確認傳送** 傳送電子郵件。 按一下 **是** 確認。

1. 傳送已開始。 按一下&#x200B;**關閉**。

   ![傳送](assets/delivering.png)

1. 按一下 **儲存** 以儲存傳送。

已發送您的電子報！

>[!TIP]
>
>此範例說明如何簡化傳送電子報給單一收件者的程式。 當然，一般的傳送會包含許多不同的收件者，而Adobe Campaign可讓您輕鬆管理這些收件者。 請參閱 [Adobe Campaign Classic檔案](https://experienceleague.adobe.com/docs/campaign-classic.html) 如需傳送和收件者管理的詳細資訊。
