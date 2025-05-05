---
title: 管理活動
description: 「活動」主控台可讓您建立、組織和管理品牌的行銷活動
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 15%

---

# 管理活動 {#managing-activities}

「活動」主控台可讓您建立、組織和管理您品牌的行銷[活動](/help/sites-cloud/authoring/personalization/overview.md#activities)：

* 新增品牌
* 針對每個品牌，新增並設定活動
* 管理活動

>[!TIP]
>
>如果您使用Adobe Target作為目標定位引擎，您也可以[檢視活動的效能資料](#viewing-performance-and-converting-winning-experiences-a-b-test)。 如果您使用A/B測試，您可以[轉換優勝者](#viewing-performance-and-converting-winning-experiences-a-b-test)。

在「活動」主控台上，活動會依品牌組織。 您可以使用品牌和資料夾來建構活動的組織。 您可以點選/按一下「**Personalization**」以及點選/按一下「**活動**」，導覽至「活動」主控台。

在鎖定目標模式中，活動可用於[製作鎖定目標內容](/help/sites-cloud/authoring/personalization/targeted-content.md)，您也可以在此建立活動。 您在「鎖定目標」模式中建立的活動會顯示在「活動」主控台中。

活動會以標籤顯示，說明已定義的活動型別：

* XT - Adobe Target體驗鎖定目標
* A/B - Adobe Target A/B測試
* AEM - Adobe Experience Manager目標定位（即ContextHub導向）

![活動型別](/help/sites-cloud/authoring/assets/activities-types.png)

>[!NOTE]
>
>可用的活動型別由以下因素決定：
>
>* 如果 `xt_only` 在AEM端使用的Adobe Target租用戶(clientcode)上啟用此選項以連線至Adobe Target，則您只能在 **AEM中建立** XT活動。
>
>* 如果 `xt_only` Adobe Target租 **用戶** (clientcode)上未啟用選項，您可以在AEM中建立 **XT** 和A/B活動。
>
>**&#x200B;** 其他附註：選 `xt_only` 項是套用於特定Target租用戶(clientcode)的設定，且只能在Adobe target中直接修改。您無法在AEM中啟用或停用此選項。

>[!CAUTION]
>
>您必須保護發佈執行個體上的活動設定節點`cq:ActivitySettings`，使其無法正常使用者存取。 活動設定節點應該只能由處理與Adobe Target的活動同步的服務存取。
>
>如需詳細資訊，請參閱與Adobe Target整合的先決條件。
<!--
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.
-->

## 使用「活動」主控台建立品牌 {#creating-a-brand-using-the-activities-console}

建立您要管理行銷活動的品牌。

當您使用「活動」主控台建立品牌時，它也會出現在「[選件」主控台](/help/sites-cloud/authoring/personalization/offers.md)中，您可以在此處建立活動體驗的選件。

1. 在導覽主控台中，選取&#x200B;**Personalization**。 選取&#x200B;**活動**。

   ![瀏覽至活動](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. 在「活動」主控台中，選取&#x200B;**「建立**」然後&#x200B;**「建立品牌**」。
1. 選取品牌範本並選取&#x200B;**下一步**。
1. 輸入您希望品牌在「活動」和「選件」主控台中顯示的標題。 或者，輸入或選取一或多個要與品牌關聯的標籤。
1. 選擇 **建立**。您的品牌會顯示在「活動」主控台中。

## 使用「活動」主控台新增/編輯活動 {#adding-editing-an-activity-using-the-activities-console}

新增活動或編輯現有活動，以將您的行銷工作聚焦於特定對象。 建立/編輯活動時，請指定下列資訊：

* **&#x200B;**&#x200B;名稱：活動的名稱。
* **&#x200B;**&#x200B;定位引擎：AEM [&#128279;](/help/sites-cloud/authoring/personalization/overview.md#aem) 或 [Adobe Target](/help/sites-cloud/authoring/personalization/overview.md#adobe-target) ，做為目標內容的引擎。
* **&#x200B;**&#x200B;選擇目標配置： (僅限Adobe Target) 此活動應用來連線至Adobe Target的雲端設定。只有在為「定位引擎」選取Adobe Target時，才會顯示此選項。
* **活動型別**：活動型別 — A/B測試或體驗鎖定目標
* **&#x200B;**&#x200B;目標：(可選) 活動的說明。
* **&#x200B;**&#x200B;體驗：對象名稱與您所定位之行銷區段之間的對應。
* **&#x200B;**&#x200B;流量百分比：如果選取A/B測試，您可以變更每個體驗的流量 (百分比)。
* **&#x200B;**&#x200B;持續時間：套用活動的時段。
* **&#x200B;**&#x200B;優先順序：活動的相對優先順序。當活動提供相同使用者區段的內容時，優先順序較高的活動優先。
* **&#x200B;**&#x200B;目標量度：如果選取Adobe target作為定位引擎，您可以將成功度量新增至活動。需要一個成功度量。

>[!NOTE]
>
>若要能夠&#x200B;**選取Target設定**，您必須是&#x200B;**Target活動作者**&#x200B;群組。

>[!NOTE]
>
>新的Adobe target活動必須在目 *標內容編輯器中建立* ，而不是在 **Activity** Console中，因為與Adobe target的同步將會失敗。
>
>不過，您可以在主控台中編輯現有的Adobe Target活動。

若要新增活動：

1. 選取您要建立活動的品牌，然後選取&#x200B;**建立**、**建立活動**。 如果編輯，請在「主版區域」畫面中選取活動，然後按一下或點選「編 **輯活動」**。
1. 提供下列資訊，然後選取&#x200B;**下一步**：
   * 活動的名稱。
   * 要使用的定位引擎。 預設會選取ContextHub (AEM)。 如果您需要使用Adobe Target，請在目標內容編輯器中建立活動。
   * 如果您已選取Adobe Target作為定位引擎，請選取/編輯用來連線至Adobe Target的雲端設定。 （請注意，您不會選取針對雲端設定建立的架構）。
   * （選用）活動的目標或說明。
   * 選取活動型別。
1. 新增一或多個體驗至活動。選取&#x200B;**新增體驗**。
1. 如果您使用AEM鎖定目標或Adobe Target體驗鎖定目標：
   1. 選取&#x200B;**選取對象**&#x200B;並選取您的體驗鎖定目標區段。
   1. 選取&#x200B;**新增體驗**，輸入名稱，然後選取&#x200B;**確定**。
   1. 選取&#x200B;**下一步**。
如果您使用Adobe Target A/B測試：
   1. 在「對象」方塊中選取鉛筆，以選取對象。
   1. 選取&#x200B;**新增體驗**，輸入名稱，然後選取&#x200B;**確定**。
   1. 輸入顯示每個體驗的流量百分比。
   1. 選取&#x200B;**「下一步」**。
1. 若要指定活動何時開始，請使用&#x200B;**開始**&#x200B;下拉式功能表來選取下列其中一個值：
   * **啟動時：**&#x200B;活動會在包含目標內容的頁面啟動時開始。
   * **指定的日期和時間：**&#x200B;特定時間。 選取此選項時，請選取日曆圖示，選取日期，並指定活動開始的時間。
1. 若要指定活動結束的時間，請使用「結束」下拉式功能表來選取下列其中一個值：
   * **停用時**：活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**：特定時間。 選取此選項時，請選取日曆圖示，選取日期，並指定活動結束時間。
1. 若要指定活動的優先順序，請使用滑桿來選取&#x200B;**低**、**正常**&#x200B;或&#x200B;**高**。
1. 如果您使用Adobe Target作為目標定位引擎，請選取您要透過此活動測量的內容。 請參閱[設定活動和設定目標](/help/sites-cloud/authoring/personalization/targeted-content.md)，以取得有關可用成功量度的詳細資訊。 請至少選取一個目標。
1. 選取「**儲存**」。

   >[!NOTE]
   >
   >建立活動後，您需要發佈活動才能使用。

## 發佈和取消發佈活動 {#publishing-and-unpublishing-activities}

您需要發佈活動才能使其可用。 相反地，您可能想要透過取消發佈來讓活動無法使用。

>[!NOTE]
>
>取消發佈活動時，除非您重新整理頁面，否則活動的狀態不會變更。

若要發佈或取消發佈活動：

1. 選取品牌，然後選取包含您要發佈或取消發佈之活動的區域。
1. 選取您要發佈或取消發佈的一或多個活動旁的圖示。

   ![從活動主控台發佈](/help/sites-cloud/authoring/assets/activities-console.png)

1. 若要發佈，請選取&#x200B;**Publish**。 若要取消發佈，請選取&#x200B;**取消發佈**。 您的活動已發佈或取消發佈，且狀態在活動主控台中變更（可能需要重新整理）。

## 作者和Publish例項上的活動 {#activities-on-author-and-publish-instances}

當使用Adobe Target目標定位引擎的活動啟動時，會在發佈執行個體上建立第二個活動：

* 製作執行個體上的活動會追蹤製作執行個體上的活動，且對於模擬訪客體驗非常有用。 為此活動記錄的分析僅反映作者執行個體上發生的情況。
* 發佈執行個體上的活動會反映和回應發佈伺服器上的活動。 此活動會在公用網站上執行。 只有發佈活動與追蹤和分析實際公共網站的使用情況相關。

## 檢視效能並轉換成功體驗（A/B測試） {#viewing-performance-and-converting-winning-experiences-a-b-test}

您可以檢視任何Adobe Target活動（XT或A/B）的效能。 如果您使用A/B測試，也可以轉換成功體驗，這會成為預設體驗。

若要檢視活動效能並轉換成功體驗：

1. 在&#x200B;**Personalization**&#x200B;中，選取&#x200B;**活動**&#x200B;以瀏覽至&#x200B;**活動**&#x200B;主控台。
1. 選取您要檢視其活動的品牌。
1. 選取活動並選取&#x200B;**檢視屬性**，然後按一下&#x200B;**報表**&#x200B;索引標籤，並選取您要檢視成功體驗之效能/轉換成功體驗的活動。 將顯示效能資料。

   ![正在檢查活動績效](/help/sites-cloud/authoring/assets/activities-performance.png)

1. 選取&#x200B;**推播贏家**&#x200B;連結，將該體驗推播為預設體驗。

   轉換成功者會執行下列動作：

   * 它會停用目前的活動
   * 修改所有頁面，並以成功體驗的實際內容取代目標內容。 成功體驗的內容會成為一般頁面&#x200B;**的一部分，而沒有**&#x200B;鎖定目標。

   ![正在轉換獲勝者](/help/sites-cloud/authoring/assets/activities-reports.png)

   成功體驗是根據轉換率，在報表中產生更多提升度的體驗。

1. 選取「**是**」以確認您要轉換獲勝者，停用目前的體驗並將其取代為獲勝者體驗的內容。

## 與Adobe Target同步活動 {#synchronizing-activities-with-adobe-target}

使用Adobe Target目標定位引擎的活動會與Adobe Target行銷活動同步。 當符合下列條件時，活動會自動同步至Adobe Target：

* 活動至少包含一個體驗。
* 至少一個體驗包含對應的區段和一個選件。
* 活動中的每個體驗都必須有相同數量的選件。

這些條件適用於作者和發佈執行個體上的活動。

同步活動時，會在Adobe Target中建立對應的行銷活動：

* 發佈執行個體上的活動與對應的Adobe Target行銷活動具有相同名稱。
* 作者執行個體上的活動與具有相同名稱且尾碼為`_author`的Target行銷活動相對應。

![與Adobe Target同步](/help/sites-cloud/authoring/assets/activities-synch.png)

修改活動時，會立即同步處理作者活動。 立即同步可讓您使用ContextHub來模擬活動。

當活動發佈至AEM發佈執行個體時，會同步Publish活動。

## 疑難排解活動同步 {#troubleshooting-activity-synchronization}

AEM與Adobe Target同步活動時，AEM會包含名為`thirdPartyId`之活動的屬性。 此屬性的值根據AEM存放庫中的活動路徑。 Adobe Target中的兩個行銷活動不能具有`thirdPartyId`屬性的相同值。 因此，如果Adobe Target中的現有行銷活動（屬於不同型別AB、XT）對`thirdPartyId`使用相同的值，則活動將無法同步。

此情況可能在以下情況下發生：

1. 活動會建立並與Adobe Target同步。
1. 在其他AEM執行個體上，活動會在相同品牌下使用相同名稱建立。 嘗試同步此活動時失敗。

此情況也可能發生在以下情況中：

1. 活動會建立並與Adobe Target同步。 活動接著會在AEM上刪除。
1. 會在相同品牌下建立活動，並使用與已刪除活動相同的名稱。 嘗試同步此活動時失敗。

為了避免同步問題，請一律對活動使用唯一的名稱。 如果活動同步失敗，您可以刪除Adobe Target中相同名稱的促銷活動（若未使用該促銷活動）。

>[!NOTE]
>
>當您在Adobe Target中建立行銷活動時，會指派名為`thirdPartyId`的屬性給每個行銷活動。 當您在Adobe Target中刪除行銷活動時，不會刪除`thirdPartyId`。 您無法對不同型別(AB、XT)的行銷活動重複使用`thirdPartyId`，也無法手動移除它。 為避免此問題，請為每個行銷活動命名一個唯一的名稱；行銷活動名稱不能在不同行銷活動型別中重複使用。
>
>如果在相同的行銷活動型別中使用相同的名稱，則會覆寫現有的行銷活動。
>
>如果在同步處理時，您遇到「要求失敗」錯誤。 `thirdPartyId`已存在」，請變更行銷活動的名稱，然後重新進行同步。
