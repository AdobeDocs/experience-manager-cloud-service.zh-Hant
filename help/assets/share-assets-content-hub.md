---
title: 在 [!DNL the Content Hub]中共用Assets
description: 在 [!DNL the Content Hub]中共用Assets
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="適用於AEM Assets)。"
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 2%

---

# 在 Content Hub 中分享資產 {#search-assets-as-a-link}

建立所選資產的連結，以便輕鬆與他人共用。 以授權[!DNL Content Hub]使用者的身分，選取您[!DNL Content Hub]環境中可用的一或多個資產、產生連結，然後傳送給其他私人或公開使用者。

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以建立所選資產的連結，並與其他使用者共用。

## 共用資產 {#share-assets}

若要與私人或公開使用者共用一或多個資產，請執行以下步驟：

1. 導覽至您的[!DNL Content Hub]首頁，選取一或多個資產並按一下![共用](/help/assets/assets/share.svg) **[!UICONTROL 共用]**，以在&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊中顯示單一選取的資產或多個選取的資產清單。

   您也可以選取並共用![集合](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL 集合]**&#x200B;中可用的資產。

1. 檢視資產或檢閱&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊中可用的資產清單。 按一下資產旁的![取消選取](/help/assets/assets/Close.svg)，即可將其從清單中移除。

1. 指定標題和可選說明，定義選取的資產集。

1. 選取&#x200B;**[!UICONTROL 到期期間]**。

1. 在&#x200B;**[!UICONTROL 誰可以存取]**&#x200B;下拉式清單下，選取存取選項並按一下&#x200B;**[!UICONTROL 取得連結]**&#x200B;以產生連結以與選取的使用者共用。 私人使用者需要登入其[!DNL Content Hub]環境才能存取共用資產頁面。 然而，公用使用者作為來賓，不需登入[!DNL Content Hub]即可存取共用資產頁面。

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![私人與公開連結](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [從設定頁面](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)啟用公用連結共用，以在&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊上顯示&#x200B;**[!UICONTROL 公用連結]**&#x200B;切換按鈕。

## 從資產的預覽頁面共用資產 {#share-asset-from-preview-page}

執行以下步驟，在預覽資產時共用資產：

1. 導覽至[!DNL Content Hub]首頁，然後按一下資產縮圖以預覽資產，並在對話方塊的右側窗格中顯示功能表選項。
1. 選取![共用](/help/assets/assets/share.svg)以顯示&#x200B;**[!UICONTROL 共用]**面板。
   預覽資產時![共用資產](/help/assets/assets/share-link-asset-preview.png)
1. 請依照[共用資產](#share-assets)區段中的步驟3到5，從此&#x200B;**[!UICONTROL 共用]**&#x200B;面板產生並共用資產連結（私人或公開）。

## 存取已共用的資產 {#access-shared-assets}

透過連結存取共用資產頁面，並執行下列動作：

* 選取一或多個資產，然後按一下[下載] ![](/help/assets/assets/download-icon.svg) **[!UICONTROL {下載]]**，從可用的下載選項中選取[原始] **[!UICONTROL 、[靜態]]** **[!UICONTROL 或兩個轉譯。]**
  ![](/help/assets/assets/download-shared-assets.png)
* 按一下資產縮圖以檢視資產的中繼資料。
* 在共用資產頁面（[透過私人連結存取](#share-assets)）上，按一下資產縮圖，然後選取![下載](/help/assets/assets/download-icon.svg)，在選取和下載之前，先在&#x200B;**[!UICONTROL 下載]**面板上選取並檢視可用的資產動態轉譯。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## 常見問題 {#faqs-share-assets-content-hub}

### 在AEM Assets Content Hub中共用資產有何意義？

在AEM Assets Content Hub中共用資產可讓授權的使用者透過產生連結，輕鬆與他人共用一個或多個資產或整個集合。 此連結可以傳送給私人使用者（必須登入）或公開使用者（可以訪客身分存取），讓收件者直接存取檢視和下載選取的資產。

### 如何使用AEM Assets Content Hub與他人共用資產或集合？

若要在Content Hub中共用資產或集合，請導覽至Content Hub首頁，選取一或多個資產（或前往「集合」標籤以共用集合），然後按一下「共用」圖示。 在「共用」對話方塊中，您可以預覽資產、視需要移除任何資產、新增標題和說明、選取可以存取連結（私人或公開）的人員、設定有效期，然後按一下「取得連結」以產生和複製可共用的URL。 然後可將連結傳送給團隊成員或利害關係人。

### 在AEM Assets Content Hub中共用資產時，有哪些存取選項可用，以及其不同之處？

Content Hub可讓您為共用連結選擇兩個存取選項：私人與公開。 私人連結會要求收件者登入其Content Hub環境以檢視及下載資產，提供額外的安全性。 擁有此連結的任何人都可以存取公開連結，不需要登入。 每種連結型別都有自己的到期設定，例如公開連結需要24小時到一週時間，私人連結則需要24小時到一週時間。

### 管理員是否管理任何設定，以致於能在AEM Assets Content Hub中產生資產的公開連結？

可以，管理員可以啟用或停用設定UI上&#x200B;**集合和共用**&#x200B;索引標籤中提供的&#x200B;**啟用公開連結**&#x200B;切換功能，以管理在AEM Assets Content Hub中產生資產的公開連結。

### 我可以在AEM Assets Content Hub中設定共用資產連結的到期日嗎？這為何重要？

可以，您可以在Content Hub中設定私人與公開共用連結的到期日。 對於公開連結，您可以從24小時至一週之類的預設集進行選擇，而私人連結則可讓您從預設集進行選擇，或設定自訂到期日。 到期日很重要，因為連結一旦到期，就無法再用來存取或下載資產，這有助於維持內容的安全性和控制力。

### 收件者如何處理使用AEM Assets Content Hub建立的共用資產連結，以及是否有下載不同轉譯的選項？

接收共用資產連結的收件者可在瀏覽器中開啟該連結，以預覽、選取和下載提供的資產。 如果在Content Hub中啟用資產轉譯，收件者可以選擇要下載的轉譯（例如原始或靜態）。 資產和轉譯會下載為zip檔案，而且按一下資產縮圖可檢視中繼資料。 連結在設定的到期日之前仍然有效。




