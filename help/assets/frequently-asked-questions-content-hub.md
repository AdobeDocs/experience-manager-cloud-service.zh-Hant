---
title: Content Hub常見問題集(FAQ)
description: 取得Content Hub部分常見問題(FAQ)的回應。
source-git-commit: 1d51a1e0858e975bc354ffd9c4b32c26aa1604af
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# Content Hub常見問題 {#content-hub-frequently-asked-questions}

![Content Hub常見問題](assets/content-hub-faqs.png)

## 什麼是Content Hub？ {#what-is-content-hub}

Content Hub是Adobe Experience Manager Assetsas a Cloud Service的一項功能。

Content Hub可讓更廣大的團隊透過直覺式的入口網站，輕鬆探索相關、已核准的資產，並快速因應其需求進行調整。  此外，Content Hub提供內嵌機制，讓這些使用者可在將資產上傳至DAM時輕鬆自助。 這直接符合組織對於更高內容建立速度的需求，同時保留品牌一致性和合規性，並具備適當的保護措施。

## 為何無法在Cloud Manager程式/環境中啟用Content Hub？ {#cannot-enable-content-hub}

目前Content Hub僅適用於AEM Cloud Manager生產程式，其中包括Assets授權。 當您按一下[Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub)以啟用時，它會進行部署，並與此程式中AEM的製作生產環境建立關聯。 請參閱[部署Content Hub](/help/assets/deploy-content-hub.md)以取得詳細資訊和先決條件。

有一個在沙箱程式/創作生產環境中搶先使用Content Hub的程式。 如需詳細資訊，請參閱[沙箱計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。 若要進一步瞭解搶先體驗方案，請洽詢您的Adobe帳戶團隊。

在此階段，Content Hub不適用於非生產環境（中繼、開發等）。

## 我在生產程式/環境中啟用了Content Hub，可以停用它嗎？ {#can-i-disable-content-hub}

在生產計畫上啟用Content Hub會將其部署為生產基礎結構的一部分。 AEM Cloud Manager不允許移除或停用生產基礎架構，以將人為錯誤導致的生產使用風險降至最低。

如果您不想在部署後將Content Hub提供給您的使用者，請勿在Admin Console中將任何使用者指派給Content Hub產品設定檔。 請參閱[部署Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)以取得詳細資料。

## 我如何在組織中評估Content Hub （因為它僅適用於生產計畫/生產製作環境）？ {#how-can-i-evaluate-content-hub}

Content Hub是Adobe提供和維護的功能，其沒有任何需要透過dev/stage/production進行典型驗證的自訂程式碼。 此外，使用者的功能存取權完全由管理員控制，因此您可以評估該功能，而不會向所有使用者公開。

您可以評估Content Hub，而不會影響您在AEM as a Cloud Service Assets中管理的使用者/生產內容。 評估程式可能如下所示：

* 在生產環境中[啟用Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) (Cloud Manager程式)
* [從生產作者將AEM管理員使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)新增到Content Hub產品設定檔。
* AEM管理員[設定Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM生產作者的AEM管理員或AEM使用者[核准Content Hub](/help/assets/approve-assets-content-hub.md)的許多資產；如果您不想變更DAM中的任何生產內容，您可能會想要在AEM製作執行個體中建立個別的評估資料夾，然後上傳/標籤或將DAM的部分資產複製到其中。
* Admin Console管理員將[一些選取的使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users)新增到Content Hub產品設定檔，以便他們開始評估。
* 評估完成後，作者執行個體中的AEM使用者可以從測試資產中移除核准、核准Content Hub的生產資產，然後Admin Console管理員可以新增所有需要存取Content Hub和核准內容的使用者。 恭喜，您的Content Hub現已上線。

Adobe也提供在預備環境中搶先使用Content Hub的方案 — 請參閱問題[為什麼我無法在Cloud Manager方案/環境中啟用Content Hub？](#cannot-enable-content-hub)以取得詳細資料。

## 為何登入Content Hub後看不到任何資產？ {#no-assets-in-content-hub}

在Assetsas a Cloud Service中標示為已核准的資產會自動在Content Hub中使用。 如果您在登入Content Hub後看不到任何資產，請使用AEM as a Cloud Service製作環境核准資產，以便在Content Hub中使用。 如需詳細資訊，請參閱[核准Content Hub的資產](/help/assets/approve-assets-content-hub.md)。

## 為何我無法看到使用Content Hub直接上傳，或使用Content Hub從Dropbox或OneDrive帳戶匯入的資產？ {#no-assets-uploaded-from-content-hub}

是否顯示使用Content Hub上傳的資產，取決於您已啟用「設定」使用者介面上的[自動核准](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)切換功能：

* 如果已啟用&#x200B;**自動核准**&#x200B;切換，則您使用Content Hub上傳的資產會自動可供使用。

* 如果&#x200B;**自動核准**&#x200B;切換功能已停用，您使用Content Hub上傳的資產不會自動顯示。 這些資產可在Assetsas a Cloud Service環境的`hydrated-assets`資料夾中使用。 導覽至資料夾，然後[大量編輯](/help/assets/approve-assets-content-hub.md)這些資產的狀態到`Approved`，以便這些資產顯示在Content Hub中。

## 如何在AEM as a Cloud Service環境中快速找到使用Content Hub上傳的資產？ {#find-uploaded-assets-on-aem-cloud}

您可以在AEM as a Cloud Service環境中透過以下方式，快速找到使用Content Hub上傳的資產：

1. 瀏覽至`hydrated-assets`資料夾。

1. 按一下&#x200B;**[!UICONTROL 篩選器]**&#x200B;並在&#x200B;**[!UICONTROL 資產狀態]**&#x200B;欄位中設定&#x200B;**[!UICONTROL 無狀態]**。

1. 使用&#x200B;**[!UICONTROL 修改日期]**&#x200B;欄位排序資產。

## 為何我無法在資產卡上檢視使用Adobe Express編輯選項，以混合資產建立新變數？ {#edit-using-express-not-available}

若要檢視資產卡上的使用Adobe Express編輯選項，除了擁有[Content Hub使用者許可權之外，您還必須擁有Adobe Express權益，該使用者有權將資產重新混合成新的變數](#onboard-content-hub-users-add-assets)。 Adobe Express必須在部署Adobe Experience Manager的Adobe Admin Console中的相同組織中部署。

## 我可以設定Content Hub，好讓我的組織的品牌指導方針在首頁上顯示為連結嗎？ {#content-hub-setup-brand-guidelines}

除了Content Hub首頁上的標準「所有Assets」、「集合」和「前瞻分析」標籤之外，您還可以新增自訂連結作為單獨的標籤。 如需如何設定的詳細資訊，請參閱[自訂連結](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否計畫將現有Brand Portal客戶移轉至Content Hub？ {#migration-brand-portal}

Adobe提供從Brand Portal到Content Hub的移轉支援，您可透過建立Adobe支援票證來使用。

## 為什麼在Content Hub中看不到「產品設定/組態」選項？ {#ui-configuration-option-missing}

若要存取[設定使用者介面](/help/assets/configure-content-hub-ui-options.md)，您必須是[Content Hub管理員](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。 如果您在Adobe Admin Console的生產製作執行個體中被指派給AEM管理員產品設定檔，而且您仍然看不到設定選項，請確保AEM管理員產品設定檔未重新命名。 如需詳細資訊，請參閱[AEM as a Cloud Service團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md)。


