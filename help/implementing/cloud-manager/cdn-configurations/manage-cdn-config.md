---
title: 管理網域對應
description: 瞭解如何使用Cloud Manager編輯和更新，或刪除Edge Delivery網站或Cloud Manager環境的CDN設定。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 41155a724f48ad28a12aac615a3e9a13bb3afa26
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 8%

---

# 管理網域對應 {#manage-cdn-configurations}

瞭解如何使用Cloud Manager編輯或刪除Edge Delivery網站或Cloud Manager環境的CDN設定。

## 從網域對應頁面編輯CDN組態 {#edit-cdn}

基於多種原因，您可能會想要在Adobe Cloud Manager中編輯CDN （內容傳遞網路）設定，包括環境層（發佈或預覽）和SSL憑證。

* **環境變更**：調整層級有助於將CDN設定與正確的環境進行比對，不論是用於即時生產（發佈）或測試（預覽）。
* **安全性增強功能**：在更新憑證或解決規範遵循與安全性需求時，可能需要選取不同的SSL憑證。
* **效能最佳化**：編輯組態可確保根據不斷變化的作業需求傳送內容時可使用正確的CDN設定。

您可以編輯設定，而不完全移除現有設定。 變更會套用至選取的環境（例如預備或生產），並可能影響內容的傳送和安全方式。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

**若要從網域對應頁面編輯CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。
1. 在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **網域對應**。
1. 在&#x200B;**網域對應**&#x200B;表格中，按一下您想要更新CDN設定之資料列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 從下拉式功能表，按一下&#x200B;**編輯**。

1. 在&#x200B;**編輯CDN組態**&#x200B;對話方塊中，設定個別下拉式清單中的一或多個選項。

   對話方塊中顯示的選項取決於您使用的是&#x200B;**Adobe管理的CDN**&#x200B;或&#x200B;**其他CDN提供者** （客戶管理的CDN）。

1. 按一下&#x200B;**更新**。

   已編輯的CDN狀態會在&#x200B;**網域對應**&#x200B;資料表中更新，以反映您所做的變更。


## 從環境頁面編輯CDN設定

從&#x200B;**環境**&#x200B;頁面編輯CDN設定的步驟幾乎與從網域對應頁面](#edit-cdn)編輯CDN設定的步驟[相同，但進入點不同。

**若要從環境頁面編輯CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。

1. 在左側功能表中，按一下![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**。

1. 在&#x200B;**環境**&#x200B;頁面上，選取感興趣的環境。

1. 在環境詳細資訊頁面上的網域對應群組中，按一下與您要編輯的CDN設定相對應的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在快顯功能表中按一下&#x200B;**編輯**。

1. 在&#x200B;**編輯CDN組態**&#x200B;對話方塊中，設定個別下拉式清單中的一或多個選項。

   對話方塊中顯示的選項取決於您使用的是&#x200B;**Adobe管理的CDN**&#x200B;或&#x200B;**其他CDN提供者** （客戶管理的CDN）。

1. 按一下&#x200B;**更新**。

<!-- 
## Go live readiness: Configure DNS settings for a custom domain {#go-live-readiness} 

Before a custom domain can serve traffic in Adobe Cloud Manager, you must complete DNS configuration with your DNS provider. After deploying a domain mapping and clicking **Go live**, Cloud Manager displays a dialog box that guides you through the DNS record setup process. You have the option to go live by adding either a CNAME record type or an A record type representing Fastly's IPs, simplifying domain routing. This ability eliminates the restriction of relying solely on CNAME records for domain setup with Fastly.

MAYBE There is support for A record types to improve Go Live readiness for domains using CDN configurations in AEM Cloud Manager. MAYBE

See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record).

**To configure Go live readiness:**

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.

1. In the left side menu, under **Services**, click ![Social network icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domain Mappings**.

1. In the Domain Mappings table, click **Go live** near the end of a row that corresponds to a CDN whose Go Live readiness you want to configure. 

1. In the Go live readiness dialog box, do one of the following:

    | Configure  | Steps |
    | --- | --- |
    | A RECORD | Recommended for root domains like `example.com`<br><ol><li>Log in to your DNS service provider's portal.<li>Go to the DNS Records section.<li>Create an A record to point to all the listed IP addresses.<li>In the Go live readiness dialog box, click **OK**.<li>In the Domain Mappings table, under the **Status** column, click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg).<br>The status is updated to **Verified** when the resolution is complete.</li></ol> |
    | CNAME | Recommended for custom domains like `www.example.com`<br><ol><li>Log in to your DMS service provider's portal.<li>Go to the DNS Records section.<li>Map [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME record) in the DNS record of the DNS service provider (your custom domain). This mapping ensures that requests received at the custom domain are redirected to Adobe's CDN.<li>In the **Go live readiness** dialog box, click **OK** to save the record.<br>Wait for DNS propogation (may take several minutes to a few hours). When the **[!UICONTROL Status]** column in the Domamin Mappings table updates to **[!UICONTROL Verified]**, the custom domain is ready to use. You may need to click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) to refresh the status.</li></ol> | 
    
-->

## 刪除CDN設定 {#delete-cdn}

當您在Cloud Manager中刪除Adobe管理或客戶管理的CDN設定時，會移除關聯的網域路由和SSL憑證設定。 網域不再使用CDN來傳送流量，而且CDN提供的任何安全性或效能增強功能都會遺失。 在設定新設定之前，您可能會遇到服務中斷的情況，無論是重新新增已刪除的CDN或新增新的CDN。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

**若要刪除CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。

1. 在左側功能表的&#x200B;**服務**&#x200B;下方，按一下![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **網域對應**。

1. 在[網域對應]表格中，按一下對應至您要移除之CDN之資料列結尾的![其他圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**刪除**。

1. 在&#x200B;**刪除CDN組態**&#x200B;對話方塊中，按一下&#x200B;**刪除**。

1. 再按一下&#x200B;**[刪除**]以確認移除網站的CDN。


## 從環境頁面刪除CDN設定

從&#x200B;**環境**&#x200B;頁面刪除CDN設定的步驟與從[網域對應頁面](#edit-cdn)刪除CDN設定的步驟幾乎相同，但進入點不同。

**若要從環境頁面刪除CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。

1. 在左側功能表中，按一下![資料圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**。

1. 在&#x200B;**環境**&#x200B;頁面上，選取感興趣的環境。

1. 在環境詳細資訊頁面的&#x200B;**網域對應**&#x200B;群組中，按一下與您要移除之CDN組態相對應的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**刪除**。

1. 在&#x200B;**刪除CDN組態**&#x200B;對話方塊中，按一下&#x200B;**刪除**。

1. 再按一下&#x200B;**[刪除**]以確認移除網站的CDN。
