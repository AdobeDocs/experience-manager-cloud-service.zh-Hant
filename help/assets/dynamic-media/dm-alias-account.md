---
title: 設定Dynamic Media公司別名帳戶
description: 瞭解如何在Dynamic Media設定公司別名帳戶。
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 關於設定Dynamic Media公司別名帳戶 {#about-dm-alias-acct}

<!-- hide: yes
hidefromtoc: yes 
-->

<!-- 
>[!NOTE]
>
>This feature to create a Dynamic Media company alias account is in the Prerelease Channel for January 2022. See [Prerelease Channel documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) for information on how to enable the feature for your environment. The feature is generally available in the February 2022 release. 
-->

Dynamic Media URL和檢視器內嵌程式碼包含您的公司帳戶名稱。 此帳戶名稱是在布建Dynamic Media時建立的。 在某些情況下，您的企業可能會經歷收購或重新品牌化，或者您只想使用更令人難忘的名稱。 在這種情況下，在開箱即用的所有URL和檢視器內嵌程式碼中，手動更新您的公司帳戶名稱並不容易。 此外，您也可能會影響現有的Dynamic Media存放庫或即時內容。 若要解決此問題，您可以設定Dynamic Media公司別名帳戶。

Dynamic Media公司別名帳戶可確保使用者介面中所有開箱即用的Dynamic Media URL和檢視器內嵌程式碼都會反映對企業內容所做的任何更新，例如品牌重塑。 別名帳戶也會對您的SEO （搜尋引擎最佳化）產生正面影響，因為Dynamic Media URL和檢視器內嵌程式碼會反映新的公司帳戶名稱。

設定Dynamic Media公司別名帳戶時，請注意下列事項：

* 您&#x200B;*即時*&#x200B;數位屬性上的任何現有Dynamic Media URL或檢視器內嵌程式碼都必須手動更新，以反映新的別名名稱。 不過，任何採用您原始Dynamic Media公司名稱的URL或檢視器內嵌程式碼仍可用於現有或新資產。
* Dynamic Media公司別名帳戶功能僅限於Experience Manager Assets製作模式和傳送。 公司別名不適用於Experience Manager Sites。 WCM （Web內容管理）元件未針對此變更進行更新。 這些元件可繼續搭配原始Dynamic Media公司名稱運作，以擷取Dynamic Media資產。
* 您只能在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面上設定一個公司別名帳戶。 不過，您可以透過支援案例來建立儘可能多的公司別名帳戶，並在Dynamic Media URL或檢視器內嵌程式碼中手動反映必要的別名名稱。
* Dynamic Media的現成可用[快取失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)功能會使在Cloud Services的Dynamic Media設定頁面中設定了公司和公司別名帳戶的URL失效。
* 當您在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面上設定公司別名帳戶時，為了成功讓快取失效，您必須同時使&#x200B;**&#x200B; **&#x200B;[!UICONTROL 公司]&#x200B;**&#x200B;帳戶和&#x200B;**&#x200B;[!UICONTROL 公司別名]**&#x200B;帳戶的URL失效。

另請參閱[在雲端服務中建立Dynamic Media設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## 設定Dynamic Media公司別名帳戶 {#configure-dm-alias-account}

請先提交支援案例，以開始設定Dynamic Media公司別名帳戶。 此為必要步驟。

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在您的支援案例中提供下列資訊：

   * 您要使用的Dynamic Media公司別名。 名稱只能包含&#x200B;*個*&#x200B;字母（允許混合大小寫）、數字、連字型大小和底線。
   * 您的地區。
   * 先前是否使用任何[規則集](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)來透過替代Dynamic Media公司帳戶名稱提供Dynamic Media內容。

1. 支援人員建立Dynamic Media別名帳戶後，在Experience Manager as a Cloud Service Author例項中，選取Experience Manager as a Cloud Service標誌以存取全域導覽主控台。
1. 在主控台左側，選取[工具]圖示，然後前往&#x200B;**[!UICONTROL 雲端服務> Dynamic Media設定]**。
1. 在[Dynamic Media設定瀏覽器]頁面的左側窗格中，選取&#x200B;**[!UICONTROL 全域]** （不要選取&#x200B;**[!UICONTROL 全域]**&#x200B;左側的資料夾圖示）。 然後選取&#x200B;**[!UICONTROL 編輯]**。

   ![Dynamic Media公司別名文字欄位](/help/assets/assets-dm/dm-company-alias.png)

1. 在&#x200B;**[!UICONTROL 編輯Dynamic Media設定]**&#x200B;頁面的&#x200B;**[!UICONTROL 公司別名]**&#x200B;文字欄位中，輸入您先前在支援案例中指定的Dynamic Media別名帳戶名稱。
1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。
Dynamic Media公司別名帳戶現在已儲存並啟用；現有及新資產的所有URL和檢視器內嵌程式碼現在都會反映新的公司別名。