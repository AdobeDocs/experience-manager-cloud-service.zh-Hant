---
title: 管理內容傳遞網路設定
description: 瞭解如何使用Cloud Manager編輯和更新，或刪除Edge Delivery網站或Cloud Manager環境的CDN設定。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 02f9b035320bb4b6219d5ed4273554259fc09e59
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 9%

---


# 管理CDN設定 {#manage-cdn-configurations}

瞭解如何使用Cloud Manager編輯或刪除Edge Delivery網站或Cloud Manager環境的CDN設定。

## 從「CDN組態」頁面編輯CDN組態 {#edit-cdn}

在AdobeCloud Manager中，您可能會想要編輯CDN （內容傳遞網路）設定，包括環境層(Publish或預覽)和SSL憑證，理由有很多。

* **環境變更**：調整層級有助於將CDN設定與正確的環境進行比對，不論是用於即時生產(Publish)或測試（預覽）。
* **安全性增強功能**：在更新憑證或解決規範遵循與安全性需求時，可能需要選取不同的SSL憑證。
* **效能最佳化**：編輯組態可確保根據不斷變化的作業需求傳送內容時可使用正確的CDN設定。

您可以編輯設定，而不完全移除現有設定。 變更會套用至選取的環境（例如預備或生產），並可能影響內容的傳送和安全方式。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

**若要從CDN設定頁面編輯CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。
1. 在側面板的&#x200B;**服務**&#x200B;下方，按一下![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **CDN設定**。
1. 在&#x200B;**CDN設定**&#x200B;表格中，按一下您想要更新CDN設定的資料列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![編輯CDN設定](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. 從下拉式功能表，按一下&#x200B;**編輯**。

1. 在&#x200B;**編輯CDN組態**&#x200B;對話方塊中，設定個別下拉式清單中的一或多個選項。

   對話方塊中顯示的選項取決於您使用的是&#x200B;**Adobe管理的CDN**&#x200B;或&#x200B;**其他CDN提供者** （客戶管理的CDN）。

1. 按一下&#x200B;**更新**。

   已編輯CDN的狀態會在&#x200B;**CDN組態**&#x200B;資料表中更新，以反映您所做的變更。


## 從環境頁面編輯CDN設定

從&#x200B;**環境**&#x200B;頁面編輯CDN設定的步驟幾乎與從[編輯CDN設定頁面](#edit-cdn)的CDN設定相同，但進入點不同。

**若要從環境頁面編輯CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 在左側功能表中，按一下&#x200B;**環境**。

1. 在&#x200B;**環境**&#x200B;頁面上，選取感興趣的環境。

1. 在環境詳細資訊頁面上，在CDN設定群組中，按一下與您要編輯的CDN設定相對應的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![在環境詳情頁面輸入網域名稱](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. 在快顯功能表中按一下&#x200B;**編輯**。

1. 在&#x200B;**編輯CDN組態**&#x200B;對話方塊中，設定個別下拉式清單中的一或多個選項。

對話方塊中顯示的選項取決於您使用的是&#x200B;**Adobe管理的CDN**&#x200B;或&#x200B;**其他CDN提供者** （客戶管理的CDN）。

1. 按一下&#x200B;**更新**。


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## 刪除CDN設定 {#delete-cdn}

當您在Cloud Manager中刪除Adobe管理或客戶管理的CDN設定時，會移除關聯的網域路由和SSL憑證設定。 網域不再使用CDN來傳送流量，而且CDN提供的任何安全性或效能增強功能都會遺失。 在設定新設定之前，您可能會遇到服務中斷的情況，無論是重新新增已刪除的CDN或新增新的CDN。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

**若要刪除CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 在左側面板的&#x200B;**服務**&#x200B;下方，按一下&#x200B;**CDN設定**。

1. 在CDN設定表格中，按一下對應至您要移除之CDN之資料列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![正在刪除CDN設定](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. 在下拉式功能表中，按一下&#x200B;**刪除**。

1. 在&#x200B;**刪除CDN組態**&#x200B;對話方塊中，按一下&#x200B;**刪除**。

1. 再按一下&#x200B;**[刪除**]以確認移除網站的CDN。


## 從環境頁面刪除CDN設定

從&#x200B;**環境**&#x200B;頁面刪除CDN設定的步驟幾乎與從[刪除CDN設定頁面](#edit-cdn)的CDN設定相同，但進入點不同。

**若要從環境頁面刪除CDN設定：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 在左側功能表中，按一下&#x200B;**環境**。

1. 在&#x200B;**環境**&#x200B;頁面上，選取感興趣的環境。

1. 在環境詳細資訊頁面的&#x200B;**CDN設定**&#x200B;群組中，按一下與您要移除的CDN設定相對應的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   環境詳細資料頁面上的![CDN設定群組](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. 在下拉式功能表中，按一下&#x200B;**刪除**。

1. 在&#x200B;**刪除CDN組態**&#x200B;對話方塊中，按一下&#x200B;**刪除**。

1. 再按一下&#x200B;**[刪除**]以確認移除網站的CDN。


