---
title: 使用定位模式製作目標內容
description: 鎖定目標模式和Target元件提供工具，用於建立體驗的內容
exl-id: 8d80d867-2d0f-4ddb-8a06-f9441e6d85ce
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '5342'
ht-degree: 6%

---

# 使用定位模式製作目標內容 {#authoring-targeted-content-using-targeting-mode}

使用AEM的「定位」模式製作目標內容。 鎖定目標模式和Target元件提供工具來建立體驗的內容：

* 輕鬆辨識頁面上的目標內容。 虛線會在所有目標內容周圍形成邊框。
* 選取品牌和活動以查看體驗。
* 新增體驗至活動或移除體驗。
* 執行A/B測試並轉換獲勝者(僅限Adobe Target)。
* 透過建立選件或使用資料庫中的選件來新增選件至體驗。
* 設定目標並監控效能。
* 模擬使用者體驗。
* 如需更多自訂項目，請設定Target元件。

您可以使用AEM或Adobe Target作為定位引擎(您必須具備有效的Adobe Target帳戶才能使用Adobe Target)。 如果您使用Adobe Target，必須先設定整合。 請參閱與Adobe Target整合的指示。<!--See the[instructions for integrating with Adobe Target](/help/sites-administering/target.md).-->

![目標內容](../assets/targeted-content.png)

您在Target模式中看到的活動和體驗會反映[活動主控台](/help/sites-cloud/authoring/personalization/activities.md):

* 您使用定位模式對活動和體驗所做的變更會反映在活動主控台中。
* 在「活動」控制台中所做的變更會反映在「定位」模式中。

>[!NOTE]
>
>在Adobe Target中建立促銷活動時，會將`thirdPartyId`屬性指派給每個促銷活動。 刪除Adobe Target中的促銷活動時，不會刪除thirdPartyId。 您無法針對不同類型(AB、XT)的促銷活動重新使用`thirdPartyId`，且無法手動移除。 為避免此問題，請為每個促銷活動命名一個唯一的名稱；因此，無法在不同促銷活動類型中重複使用促銷活動名稱。
>
>如果您在相同的促銷活動類型中使用相同名稱，則會覆寫現有的促銷活動。
>
>如果在同步期間，您會遇到「請求失敗」錯誤。 `thirdPartyId` 已存在，請變更促銷活動名稱並重新同步。

>[!NOTE]
>
>鎖定目標時，品牌和活動組合會保留在使用者層級，而非管道層級。

## 切換至定位模式{#switching-to-targeting-mode}

切換至Target模式，存取製作目標內容的工具。

切換到目標模式：

1. 開啟您要為其製作目標內容的頁面。
1. 在頁面頂端的工具列上，按一下或點選「模式」下拉式選單，以顯示可用的模式類型。

   ![定位模式](../assets/targeted-mode.png)

1. 按一下或點選「**目標定位**」。 定位選項會顯示在頁面頂端。

   ![定位工具列](../assets/targeted-toolbar.png)

## 使用定位模式{#adding-an-activity-using-targeting-mode}新增活動

使用鎖定目標模式將活動新增至品牌。 新增活動時，活動會包含預設體驗。 新增活動後，就會開始活動的內容鎖定目標程式。

您也可以從AEM建立和管理Adobe Target活動，並選擇目標引擎(AEM或Adobe Target)和選取活動類型（體驗鎖定目標或A/B測試）。

此外，您可以管理所有Adobe Target活動的目標和量度，並管理您的Adobe Target對象。 也包含Adobe Target活動報表，包括轉換A/B測試的獲勝者。

新增活動時，它也會出現在[活動主控台](/help/sites-cloud/authoring/personalization/activities.md)中。

若要新增活動：

1. 使用&#x200B;**Brand**&#x200B;下拉式功能表，選取您要建立活動的品牌。

   >[!NOTE]
   >
   >建議您透過活動控制台](/help/sites-cloud/authoring/personalization/activities.md#creating-a-brand-using-the-activities-console)建立品牌。[
   >
   >
   >如果您以其他方式建立品牌，請確定節點`/campaigns/<brand>/master`存在，或嘗試建立活動時會產生錯誤。

1. 按一下或點選&#x200B;**活動**&#x200B;下拉式選單旁的+。
1. 輸入活動的名稱。

   >[!NOTE]
   >
   >當您建立新活動並將Adobe Target雲端設定附加至頁面或其其中一個上層時，AEM會自動假設Adobe Target為引擎。

1. 在&#x200B;**定位**&#x200B;引擎下拉式選單中，選取您的定位引擎。

   * 如果您選取&#x200B;**ContextHub AEM**，其餘欄位將呈現灰色且無法使用。 按一下或點選&#x200B;**建立**。

   * 如果您選取&#x200B;**Adobe Target**，則可以選取設定（依預設，這是您在設定帳戶時提供的設定）和活動類型。<!--If you select **Adobe Target**, you can select a configuration (by default, it is the configuration you provided when you [configured the account](/help/sites-administering/opt-in.md)) and Activity Type.-->

1. 在「活動」功能表中，選取&#x200B;**體驗鎖定目標**&#x200B;或&#x200B;**A/B測試**。

   * 體驗鎖定目標 — 從AEM管理Adobe Target活動。
   * A/B測試 — 從AEM在Adobe Target中建立/管理A/B測試活動。

## 定位程式：建立、定位、目標與設定{#the-targeting-process-create-target-and-goals-settings}

定位模式可讓您設定活動的數個方面。 使用下列三個步驟程式來建立品牌活動的目標內容：

1. [建立](#create-authoring-the-experiences):新增或移除體驗，以及為每個體驗新增選件。
1. [目標](#target-configuring-the-audiences):指定每個體驗鎖定的對象。您可以鎖定特定對象，如果使用A/B測試決定要將多少百分比的流量傳至哪個體驗。
1. [目標與設定](#goals-settings-configuring-the-activity-and-setting-goals):排程活動並設定優先順序。您也可以設定成功量度目標。

請依照下列程式，開始活動的內容定位程式。

>[!NOTE]
>
>若要使用定位程式，您必須是Target活動作者使用者群組的成員。

若要新增活動：

1. 在&#x200B;**Brand**&#x200B;下拉式功能表中，選取包含您正在使用之活動的品牌。
1. 在&#x200B;**Activity**&#x200B;下拉式選單中，選取您要為其編寫目標內容的活動。
1. 若要顯示引導您完成定位程式的控制項，請按一下或點選&#x200B;**開始定位**。

   ![開始定位](../assets/targeted-start-targeting.png)

   >[!NOTE]
   >
   >若要變更您正在使用的活動，請按一下或點選&#x200B;**Back**。

## 建立：編寫體驗{#create-authoring-the-experiences}

內容鎖定目標的建立步驟涉及建立體驗。 在此步驟中，您可以建立或刪除活動的體驗，並新增選件至每個體驗。

### 在定位模式{#seeing-experience-offers-in-targeting-mode}中查看體驗選件

在您[開始定位程式](#the-targeting-process-create-target-and-goals-settings)後，選取體驗以查看為該體驗提供的選件。 當您選取體驗時，頁面上的目標元件會變更，以顯示該體驗的選件。

>[!CAUTION]
>
>停用已在製作例項中定位之元件的定位時請務必小心。 也會自動從發佈例項中刪除個別的活動。

>[!NOTE]
>
>選件是目標元件的內容。

體驗會顯示在「對象」窗格中。在下列範例中，體驗包 **括Default**、 **Femole**、 **Femole 30歲以上，******&#x200B;以及Femole 30歲以下。此範例顯示目標影像元件的「預設 **」選件** 。

![目標影像元件](../assets/targeted-image-component.png)

選取不同體驗時，影像元件會顯示該體驗的選件。

![已變更目標影像元件](../assets/targeted-image-different.png)

當選取體驗且目標元件不包含該體驗的選件時，元件會顯示疊加在半透明預設選件上的「新增選件 **** 」。當未建立任何體驗的選件時，會針對對應至 **體驗的區段顯示** 「預設」選件。

![新增選件](../assets/targeted-add-offer.png)

當訪客屬性與對應至體驗的任何區段不符時，也會顯示預設體驗。 請參閱[使用定位模式新增體驗](#adding-and-removing-experiences-using-targeting-mode)。

### 自訂選件和資料庫選件{#custom-offers-and-library-offers}

在頁面](#adding-a-custom-offer)上撰寫並用於單一體驗的選件，稱為自訂選件。 [下列影像疊加在自訂選件的內容上：

![自訂選件圖示](../assets/targeted-custom-offer-icon.png)

從選件資料庫](#adding-an-offer-from-an-offer-library)新增的選件會與下列影像重疊：[

![程式庫選件圖示](../assets/targeted-library-offer-icon.png)

如果您決定要重複使用自訂選件，可將自訂選件儲存至選件資料庫。 如果您想要修改體驗的內容，也可以將程式庫選件轉換為自訂選件。 編輯後，您可以再次將選件儲存回程式庫。

### 使用定位模式{#adding-and-removing-experiences-using-targeting-mode}新增和移除體驗

使用[目標定位程式](#the-targeting-process-create-target-and-goals-settings)的建立步驟，您可以新增和移除體驗。 此外，您可以複製體驗並重新命名。

#### 使用定位模式{#adding-experiences-using-targeting-mode}新增體驗

若要新增體驗：

1. 若要新增體驗，請按一下或點選「**+** **新增體驗鎖定目標**」，顯示於「**對象**」窗格中現有體驗下方。
1. 選取和對象。 依預設，該名稱為體驗的名稱。 您可以視需要輸入其他名稱。 按一下或點選&#x200B;**確定**。

#### 使用定位模式{#removing-experiences-using-targeting-mode}移除體驗

若要刪除體驗：

1. 按一下或點選體驗名稱旁的箭頭。

   ![刪除和體驗](../assets/targeted-delete-experiene.png)

1. 按一下&#x200B;**Delete**。

#### 使用定位模式重新命名體驗{#renaming-experiences-using-targeting-mode}

若要使用定位模式重新命名體驗：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一下「**重新命名體驗**」 ，然後輸入新名稱。
1. 按一下或點選畫面上的其他位置，以儲存變更。

#### 使用定位模式{#editing-audiences-using-targeting-mode}編輯對象

若要使用鎖定模式編輯對象：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一下「**編輯對象**」並選取新對象。
1. 按一下&#x200B;**「確定」**。

#### 使用定位模式複製體驗{#duplicating-experiences-using-targeting-mode}

若要使用定位模式複製體驗：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一下「**複製**」並選擇對象。
1. 視需要重新命名體驗，然後按一下&#x200B;**確定**。

### 使用定位模式{#creating-offers-using-targeting-mode}建立選件

定位元件以建立體驗的選件。 目標元件提供用作體驗選件的內容。

* [定位現有元件](#creating-a-default-offer-by-targeting-an-existing-component)。內容會變成預設體驗的選件。
* [新增Target元件](#creating-an-offer-by-adding-a-target-component)，然後新增內容至元件。

將元件定位後，您就可以為每個體驗新增選件：

* [新增自訂選件](#adding-a-custom-offer)。
* [從資料庫新增選件](#adding-an-offer-from-an-offer-library)。

使用選件時可使用下列工具：

* [將自訂選件新增至選件資料庫](#adding-a-custom-offer-to-a-library)。
* [將程式庫選件轉換為自訂選件](#converting-a-library-offer-to-a-custom-library)。
* [開啟程式庫選件並編輯內容](#editing-a-library-offer)。

#### 定位現有元件{#creating-a-default-offer-by-targeting-an-existing-component}以建立預設選件

在頁面上定位元件，以用作活動的預設體驗選件。 當您定位元件時，元件會封裝在Target元件中，其內容會變成預設體驗的選件。

當您定位元件時，選件中只能使用該元件。 您無法從選件中移除元件，或將其他元件新增至選件。

在[啟動目標進程](#the-targeting-process-create-target-and-goals-settings)之後執行以下過程。

1. 按一下或點選要定位的元件。 元件的工具列隨即出現，如下列範例所示。

   ![目標元件](../assets/targeted-component.png)

1. 按一下或點選「目標」圖示。

   ![Target按鈕](../assets/targeted-target-button.png)

   元件內容是預設體驗的選件。 定位元件時，會針對每個體驗複製其預設節點。 在體驗特定製作期間編輯正確的內容節點時，需要用到此功能。 針對這些非預設體驗，請[新增自訂選件](#adding-a-custom-offer)或[新增資料庫選件](#adding-an-offer-from-an-offer-library)。

#### 新增Target元件{#creating-an-offer-by-adding-a-target-component}以建立選件

新增Target元件以建立預設體驗的選件。 Target元件是其他元件的容器，放在其中的元件會成為目標。 使用Target元件時，您可以新增數個元件以建立選件。 此外，您也可以在每個體驗中使用不同的元件，以建立不同的選件。

如需自訂此元件的詳細資訊，請參閱[設定Target元件選項](#configuring-target-component-options)。

>[!NOTE]
>
>您使用[選件控制台](/help/sites-cloud/authoring/personalization/offers.md)建立的選件也可包含數個元件。 這些選件屬於選件資料庫，可用於多個體驗。

由於Target元件是容器，因此會顯示為其他元件的拖放區域。

在「目標」模式中，Target元件有藍色邊框，而下拉目標訊息會指出目標性質。

![目標放置區](../assets/targeted-drop-target.png)

在「編輯」模式中，Target元件有一個布爾序清單徵圖。

![目標放置區的表徵圖](../assets/targeted-drop-target-icon.png)

將元件拖曳至Target元件時，元件即為目標元件。

![拖放帶目標的區域](../assets/targeted-drop-zone-populated.png)

將元件新增至Target元件時，元件會提供特定體驗的內容。 若要指定體驗，請在新增元件之前選取體驗。

您可以在編輯模式或目標模式中將Target元件新增至頁面。 您只能以「目標」模式將元件新增至「目標」元件。 Target元件屬於個人化元件群組。

如果編輯目標內容，您必須先按一下或點選「開始鎖定目標」**，才能這麼做。**

1. 將Target元件拖曳至您要顯示選件的頁面。
1. 預設情況下，未設定任何位置ID。 按一下或點選「設定齒輪」以設定位置。

   >[!NOTE]
   >
   >如果由管理員設定，則可能需要明確設定位置。
   >
   >管理員可以在`https://<host>:<port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet`決定是否需要設定此配置
   >
   >要要求用戶輸入位置，請選中「強制 **位置** 」複選框。

1. 選取您要建立選件的體驗。
1. 建立選件：

   * 針對預設體驗，將元件拖曳至目標放置區，並照常編輯元件屬性，以建立選件的內容。
   * 針對非預設體驗，請[新增自訂選件](#adding-a-custom-offer)或[新增資料庫選件](#adding-an-offer-from-an-offer-library)。

#### 新增自訂選件{#adding-a-custom-offer}

在「鎖定目標」模式中編寫目標元件的內容，以建立選件。 建立自訂選件時，會將其用作單一體驗的選件。

如果您決定可將該選件用於其他體驗，您可以建立自訂選件，然後[將其新增至資料庫](#adding-a-custom-offer-to-a-library)。 如需使用優惠方案控制台來建立可重複使用優惠方案的相關資訊，請參閱[將優惠方案新增至優惠方案程式庫](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library)。

1. 選取您要新增選件的體驗。
1. 若要顯示元件功能表，請按一下或點選您要新增選件的目標元件。

   ![新增優惠方案](../assets/targeted-component-menu.png)

1. 按一下或點選+圖示。

   預設選件的內容會作為目前體驗的選件。

1. 按一下或點選選件以顯示選件選單，然後按一下或點選編輯圖示。

   ![目標元件工具欄](../assets/targeted-offer-menu.png)

1. 編輯元件的內容。

#### 從選件資料庫{#adding-an-offer-from-an-offer-library}新增選件

將選件從[選件資料庫](/help/sites-cloud/authoring/personalization/offers.md)新增至體驗。 您可以從您目前鎖定的品牌資料庫新增任何選件。

您無法將程式庫選件新增至預設體驗。

1. 選取您要新增選件的體驗。
1. 若要顯示元件功能表，請按一下或點選您要新增選件的目標元件。

   ![目標選件](../assets/targeted-add-offer-large.png)

1. 按一下或點選資料夾圖示。

   ![資料夾圖示](../assets/targeted-folder-button.png)

1. 從資料庫中選取選件，然後按一下或點選核取標籤圖示。

   ![優惠方案庫](../assets/targeted-select-content.png)

   選件選擇器可讓您瀏覽或篩選選件。 瀏覽或篩選時，您也可能想要排序選件，並變更檢視選件的方式。 右上角的數字代表目前程式庫中有多少個可用選件。

   * 按一下或點選&#x200B;**瀏覽**&#x200B;以導覽至其他資料夾。 導覽窗格隨即開啟，您按一下箭頭即可深入檢視資料夾。 再次按一下或點選&#x200B;**瀏覽**&#x200B;以關閉導覽窗格。

   ![瀏覽內容](../assets/targeted-select-content-browse.png)

   * 按一下或點選&#x200B;**「篩選**」，以根據關鍵字或標籤來篩選選件。 您可以輸入關鍵字，並從下拉式選單中選取標籤。 再按一下或點選&#x200B;**篩選**&#x200B;以關閉篩選窗格。

   ![篩選內容](../assets/targeted-filter.png)

   * 按一下或點選&#x200B;**最新至最舊**&#x200B;旁的箭頭，變更優惠方案的排序方式。 選件可以按最新到最舊或最舊到最新排序。

   ![篩選排序順序](../assets/targeted-filter-sort.png)

   按一下或點選「以&#x200B;**檢視方式**」旁的圖示，以圖磚或清單形式檢視選件。

   ![「查看方式」按鈕](../assets/targeted-view-as-button.png)

#### 將自訂選件新增至程式庫{#adding-a-custom-offer-to-a-library}

當您想要重複使用自訂選件作為多個體驗的選件時，請將自訂選件新增至[選件資料庫](/help/sites-cloud/authoring/personalization/offers.md)。 您可以將選件新增至您所定位之目前品牌的資料庫。

如需使用優惠方案控制台來建立可重複使用優惠方案的相關資訊，請參閱[將優惠方案新增至優惠方案程式庫](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library)。

1. 選取要顯示自訂選件的體驗。
1. 按一下或點選自訂選件以顯示選件功能表，然後按一下或點選「儲存選件至選件資料庫」**圖示。**

   ![將選件儲存至選件程式庫](../assets/targeted-save-offer-library-button.png)

1. 輸入選件的名稱，然後選取您要新增選件的資料庫，然後按一下或點選核取標籤圖示。

#### 將程式庫選件轉換為自訂程式庫{#converting-a-library-offer-to-a-custom-library}

將程式庫選件轉換為自訂選件，以變更目前體驗的選件，而不變更其他體驗中的選件。

1. 選取要顯示程式庫選件的體驗。
1. 按一下或點選程式庫選件以顯示選件功能表，然後按一下或點選「轉換為內嵌選件」圖示。

   ![轉換為內嵌選件](../assets/targeted-convert-inline.png)

#### 編輯程式庫選件{#editing-a-library-offer}

在鎖定目標模式中從體驗開啟程式庫選件，以編輯選件。 您所做的變更會顯示在使用選件的所有體驗中。

1. 選取要顯示程式庫選件的體驗。
1. 將程式庫選件轉換為本機/自訂選件。 請參閱[將程式庫選件轉換為自訂程式庫](#converting-a-library-offer-to-a-custom-library)。
1. 編輯選件的內容。

1. 將其儲存回程式庫。 請參閱[將自訂選件新增至程式庫](#adding-a-custom-offer-to-a-library)。

## 目標：設定對象{#target-configuring-the-audiences}

[鎖定目標程式](#the-targeting-process-create-target-and-goals-settings)的鎖定目標步驟涉及將對象對應至您在建立步驟中使用的體驗。 Target頁面會顯示每個體驗鎖定的對象。 您可以指定或變更每個體驗的對象。 如果您使用Adobe Target，您也可以建立A/B測試，以鎖定特定體驗對象的流量百分比。

### 如果您使用AEM鎖定目標或Adobe Target（體驗鎖定目標）{#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

對象會出現在對應圖表的左側，體驗則會出現在右側。

![對應對象](../assets/targeted-diagram.png)

使用區段定義對象。 頁面的雲端設定會決定您可使用的區段。 頁面未與Adobe Target雲端設定相關聯時，可使用AEM區段來定義對象。 頁面與Adobe Target雲端設定相關聯時，您會使用Target區段。

如需定位引擎的資訊，請參閱[定位引擎](/help/sites-cloud/authoring/personalization/overview.md#targeting-engine)。

一個對象不得用於多個體驗。 當體驗對應至已對應至其他體驗的對象時，該體驗旁會顯示警告符號。

![警告圖示](../assets/targeted-warn.png)

### 將體驗與對象(AEM或Adobe Target)關聯{#associating-experiences-with-audiences-aem-or-adobe-target}

使用AEM鎖定目標(或Adobe Target體驗鎖定目標)時，請依照下列程式將體驗與對象建立關聯：

1. 按一下或點選對應至體驗之對象方塊中旁邊的下拉式箭頭。
1. （選用）按一下或點選&#x200B;**編輯**，然後輸入關鍵字以搜尋所需的區段。
1. 在對象清單中，選取對象，然後按一下或點選&#x200B;**確定**。

### 如果您使用A/B測試(Adobe Target){#if-you-are-using-a-b-testing-adobe-target}

如果您有A/B測試活動，對象在您的左側，每個體驗的檢視百分比在中間，而體驗在右側。

只要加總為100%，您就可以變更百分比。 受眾可供A/B測試中的多個體驗使用。

![A/B目標定位](../assets/targeted-ab.png)

### 將對象和流量百分比與A/B測試{#associating-audiences-and-traffic-percentages-with-a-b-testing}關聯

1. 按一下或點選對應至體驗之對象旁的下拉式方塊。
1. （選用）按一下「**編輯**」，然後輸入關鍵字以搜尋所需區段。
1. 按一下或點選「**確定」。**
1. 以百分比輸入，以設定對象流量如何路由至每個體驗。 總數必須等於100。
1. （選用）按一下體驗名稱旁的下拉式功能表，編輯體驗名稱。

## 目標與設定：設定活動和設定目標{#goals-settings-configuring-the-activity-and-setting-goals}

[定位程式](#the-targeting-process-create-target-and-goals-settings)的目標與設定步驟涉及設定品牌活動的行為。 指定活動何時開始和結束，以及活動優先順序。 此外，您也可以追蹤目標。 具體來說，您可以決定要以活動測量什麼。

目標量度只有在您使用Adobe Target作為目標引擎時才可用。 您至少必須定義一個目標量度。 如果您已設定Adobe Analytics且有A4T Analytics雲端設定，則可以選取您要讓報表來源為Adobe Target或Adobe Analytics。

目標量度只會針對已發佈的促銷活動進行測量。

如果使用AEM作為定位引擎：

![AEM作為目標引擎](../assets/targeted-goals.png)

如果使用Adobe Target作為定位引擎：

![Adobe Target作為目標引擎](../assets/targeted-engine.png)

如果使用Adobe target做為定位引擎，而您已為帳戶設定了A4T Analytics，則您會有其他的「 **Reporting Source** 」下拉式選單：

![A4T](../assets/targeted-source.png)

下列成功量度可供使用（僅用於發佈）:

| 量度 | 說明 | 選項 |
|---|---|---|
| 轉換 | 按一下所測試體驗任何部分的訪客百分比。 每個訪客或任何訪客每次完成轉換時，都可計算一次轉換。 轉換量度設為下列其中一項 | 已檢視頁面 — 您可以選取URL，然後定義URL或多個URL，或選取URL包含，然後新增路徑或關鍵字，來定義對象已檢視的頁面。 已檢視mbox — 您可以輸入mbox的名稱，以定義已檢視的mbox。 您可以按一下「新增Mbox」來輸入多個mbox。 |
| 收入 | 瀏覽產生的收入。 您可以從列出的收入量度中選擇。 對於其中任何選項，是否檢視mbox表示已達到目標。 您可以定義mbox或多個mbox。 | 每位訪客帶來的收入(RPV)、平均訂單值(AOV)、總銷售、訂購 |
| 參與 | 您可以測量三種類型的參與 | 頁面檢視、自訂分數、網站逗留時間 |

此外，進階設定可讓您判斷如何計算成功量度。 選項包括計算每次曝光的量度或每位訪客一次，以及選擇是否讓使用者留在活動中或移除這些量度。

使用進階設定來判斷使用者達到目標量度後&#x200B;**會發生什麼事。**&#x200B;下表顯示可用選項。

| 使用者達到此目標量度後…… | 選擇要進行的以下操作…… |
|---|---|
| 增加計數並讓使用者留在活動中 | 指定計數的增加方式：每個加入者一次，在每次曝光時（排除頁面重新整理），在每次曝光時 |
| 增加計數、釋出使用者並允許重新進入 | 選取訪客如果重新進入活動會看到的體驗：相同的體驗，隨機的體驗，看不見的體驗 |
| 增加計數、釋出使用者及禁止重新進入 | 決定使用者可看見的內容，而非活動內容：相同體驗，不追蹤、預設內容或其他活動內容 |

如需成功量度的詳細資訊，請參閱[Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)。

### 配置設定(AEM定位){#configuring-settings-aem-targeting}

若要在使用AEM鎖定目標時進行設定：

1. 若要指定活動何時開始，請使用&#x200B;**Start**&#x200B;下拉式功能表來選取下列其中一個值：

   * **啟動時**:活動從包含目標內容的頁面啟動時開始。
   * **指定的日期和時間**:特定時間。選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 若要指定活動結束時間，請使用&#x200B;**End**&#x200B;下拉式選單來選取下列其中一個值：

   * **停用時**:活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**:特定時間。選取此選項時，按一下或點選日曆圖示，選取日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑桿選擇&#x200B;**Low**、**Normal**&#x200B;或&#x200B;**High**。

### 設定目標與設定(Adobe Target){#configuring-goals-settings-adobe-target}

若要在使用Adobe Target時設定目標與設定：

1. 若要指定活動何時開始，請使用&#x200B;**Start**&#x200B;下拉式功能表來選取下列其中一個值：

   * **啟動時**:活動從包含目標內容的頁面啟動時開始。
   * **指定的日期和時間**:特定時間。選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 若要指定活動結束時間，請使用&#x200B;**End**&#x200B;下拉式選單來選取下列其中一個值：

   * **停用時**:活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**:特定時間。選取此選項時，按一下或點選日曆圖示，選取日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑桿選擇&#x200B;**Low**、**Normal**&#x200B;或&#x200B;**High**。
1. 如果您已使用Adobe target帳戶設定Adobe Analytics，則會看到「報 **告來源** 」下拉式功能表。選取 **Adobe Target****或** Adobe Analytics做為來源。

   如果您選取&#x200B;**Adobe Analytics**，請選取公司和報表套裝。 如果您選取&#x200B;**Adobe Target**，則不需要任何動作。

   ![報表來源](../assets/targeted-reporting-source.png)

1. 在「目 **標量度** 」區域的「我的主要目標 **** 」下方，選取您要追蹤的成功量度——轉換、收入、參與——並輸入量度的測量方式 (或觀眾採取哪些動作來指出已達成目標)。請參閱上表中目標量度的定義，並參閱 [Adobe Target成功量度的相關檔案](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) 。

   您可以按一下右上角的三個點並選取「重新命名」，以重新命名目 **標**。

   如果您需要清除所有欄位，請按一下右上角的三個點，然後選取「清除所 **有欄位」**。

   所有量度也有您可定義的進階設定。 選擇&#x200B;**高級設定**&#x200B;以訪問這些設定。 請參閱上表中成功量度計算方式的定義，並參閱[Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)。

   >[!NOTE]
   >
   >必須至少定義一個目標。

   ![目標量度](../assets/targeted-goal-metric.png)

   >[!NOTE]
   >
   >如果量度中缺少資訊，量度周圍會出現紅線。

1. 按一下「**新增量度**」以設定其他成功量度。

   ![其他量度](../assets/targeted-additional-metrics.png)

   >[!NOTE]
   >
   >您可以按一下或點選三個點，然後按一下或點選&#x200B;**Delete**，以移除其他目標。 AEM要求您至少定義一個目標。

1. 如果您想要進一步控製成功量度的計算方式，請按一下或點選「**進階設定** 」以存取這些量度。
1. 按一下「**儲存**」。

設定後，您可以[檢視使用Adobe Target（體驗或A/B測試鎖定目標）之活動的效能](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test)。 此外，使用A/B測試鎖定目標，您可以[轉換獲勝者。](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## 模擬體驗{#simulating-an-experience}

模擬訪客的體驗，以根據您目標內容的設計，確認頁面內容如預期般顯示。 模擬時，載入不同的使用者設定檔，並查看該使用者的目標內容。

下列條件會決定模擬訪客體驗時顯示的內容：

* 使用者工作階段存放區中的資料（透過Context Hub）。
* 位於](/help/sites-cloud/authoring/personalization/activities.md)的[活動。
* 定義區段](/help/sites-cloud/authoring/personalization/segmentation.md)的[規則。
* Target元件中的體驗內容。
* 定位引擎](/help/sites-cloud/authoring/personalization/activities.md)的[配置。

如果載入設定檔時頁面上出現非預期的內容，請檢查此清單中每個項目的設定。

>[!NOTE]
>
>如果您使用A/B測試，則模擬體驗時會根據流量百分比顯示。 這是由Adobe Target控制，可能會導致作者產生非預期的結果。 （_author活動會與特定設定同步，以允許在模擬期間重新評估。） 作者可能需要重新整理，才能根據其流量設定查看其他體驗。

若要模擬訪客的體驗，請使用下列工具：

* 定位模式中的模擬活動：頁面會顯示目前在Context Hub中選取之使用者的選件。 您可以編輯以使用者為目標的選件。
* 預覽模式：使用「內容中樞」來選取符合您的體驗所根據之區段標準的使用者和位置。 當您的「內容中心」選取項目變更時，目標內容會隨之變更。

1. 若要切換至「預覽」模式，請在工具列上按一下或點選「**預覽**」。
1. 在工具列上，按一下或點選「內容中樞」圖示。

   ![ContextHub按鈕](../assets/targeted-contexthub-button.png)

1. 使用Context Hub來變更內容屬性。 例如，按一下或點選「角色」屬性，以選取不同的使用者。

   ![ContextHub工具列](../assets/targeted-contexthub-toolbar.png)

   頁面會變更，顯示針對目前內容鎖定的內容。

1. 若要變更顯示的選件，請切換至「定位」模式。 在選取模擬活動後，編輯您在預覽模式中設定之內容的選件。

## 配置目標元件選項{#configuring-target-component-options}

您可以透過下列兩種方式之一存取元件的選項來自訂Target元件：

1. 將元件定位後，在「目標」元件中，按一下或點選元件，然後按一下設定圖示（齒輪）。

   ![元件設定](../assets/targeted-component-settings.png)

   AEM會顯示「目標元件選項」視窗。

   ![Target對話方塊](../assets/targeted-dialog.png)

1. 或者，若要以全螢幕模式存取這些設定，請在「目標元件選項」視窗中，按一下或點選全螢幕圖示。

   ![全螢幕按鈕](../assets/targeted-fullscreen.png)

   AEM會顯示全螢幕Target元件選項視窗。

   ![全螢幕元件](../assets/targeted-target-as-enging.png)

1. 如下表所述，配置Target元件設定。

| 選項 | 說明 |
|---|---|
| 位置 | 位置是字串，為目標內容位置指定名稱，並將選件與應放置這些選件的頁面上的位置（或位置或元件）連接。 此欄位是一般值。 如果您將選件放入元件中，選件會記住位置ID。 執行頁面時，引擎會評估使用者的區段，並據此解析應顯示之作用中促銷活動的體驗。 接著會檢查頁面上的位置ID，並嘗試將選件與這些位置ID比對。 |
| 引擎 | 根據您要使用的引擎，在用戶端規則（不追蹤）、Adobe Target、ContextHub和Adobe Campaign之間選取。 |

如果您選取Adobe Target作為引擎：

![目標作為引擎](../assets/targeted-target-as-enging.png)

| 選項 | 說明 |
|---|---|
| 準確定位 | 啟用正確定位可告知元件，在將請求傳送至Adobe Target之前，應等待用戶端內容或內容中樞資料可供使用。 這可能會增載入入時間。 在製作時，一律會啟用精確鎖定目標。 如果您選取「準確鎖定目標」核取方塊，mbox會先執行mboxDefine，之後執行mboxUpdate，在資料可用時產生Ajax請求。 如果您未選取「準確鎖定目標」核取方塊，mbox會立即執行mboxCreate，導致同步請求（在此案例中，並非所有內容資料都可用）。 注意：對特定元件啟用或停用精確鎖定不會影響您已全域設定的設定。 您一律可以選取元件中的「精確鎖定目標」 ，以覆寫全域設定。 |
| 包括已解析的區段 | 選取此核取方塊會包含mbox呼叫中的所有已解析區段，以及頁面和架構中所設定的任何參數。 這隻適用於同步AEM區段的XML API。 如果AEM中有未由Adobe Target處理的區段（如指令碼區段），則此選項可讓您解析AEM中的區段，並將該區段作用中的資訊傳送至Adobe Target。 |
| 繼承的內容參數 | 列出與選定頁面相關聯的從Adobe Target框架繼承的上下文參數（如果有）。 |
| 內容參數 | 按一下或點選「新增」欄位，以設定其他內容參數（與Target架構中可用的參數相同）。 添加到元件的上下文參數僅應用於元件，而不適用於其他元件，如果直接將上下文參數添加到框架，則情況會如此。 |
| 靜態參數 | 按一下或點選「新增」欄位，以設定其他靜態參數（與Target架構中可用的參數相同）。 新增至元件的靜態參數只會套用至元件，不會套用至其他元件，如同您直接新增靜態參數至架構時的情況。 靜態參數不來自內容（內容中心的用戶端內容）。 |

>[!NOTE]
>
>選取元件並將其設為可目標時，AEM也會取代元件並插入Adobe Target元件。 (Adobe Target元件不僅會在您手動新增至頁面時使用，也會在您定位現有元件時使用。)
>
>如果您要整合AEM與Adobe Campaign，請選取&#x200B;**Adobe Campaign**&#x200B;作為引擎。 如需詳細資訊，請參閱整合AEM與Adobe Campaign 。
>
>如果您使用ContextHub進行定位，請選取&#x200B;**ContextHub**&#x200B;作為引擎。 如需詳細資訊，請參閱設定ContextHub 。
<!--You select **Adobe Campaign** as the engine if you are integrating AEM with Adobe Campaign. See [Integrating AEM with Adobe Campaign](/help/sites-administering/campaign.md) for more information.-->
<!--Select **ContextHub** as the engine if you are using ContextHub for targeting. See [Configuring ContextHub.](/help/sites-administering/contexthub-config.md)-->
