---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.11.0 的發行說明
description: 瞭解AEM as a Cloud Service中的Cloud Manager 2024.11.0版。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 29%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.11.0 的發行說明 {#release-notes}

瞭解關於AEM (Adobe Experience Manager)as a Cloud Service中的Cloud Manager 2024.11.0版。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.11.0發行日期是2024年11月7日。

下一個預計發行日期為2024年12月5日。

## 新增功能 {#what-is-new}

* 透過AEM Cloud Service體驗Edge Delivery Services創新的最新進展 — 現在可讓您在沙箱程式中探索。 [深入瞭解](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* AEM Cloud Manager中的「網域設定」頁面現在包含搜尋功能，可讓您依名稱快速找到網域。 您可以在搜尋欄位中輸入關鍵字，以篩選及顯示相符的網域，讓您更輕鬆地有效管理多個網域。 此外，頁面還提供狀態篩選器，例如&#x200B;**已驗證**&#x200B;和&#x200B;**未驗證**，以進一步調整搜尋結果。<!-- (CMGR-62615) -->

![在網域設定中搜尋欄位](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## 早期採用方案 {#early-adoption}

成為 Cloud Manager 早期採用方案的一部分，並有機會測試即將推出的功能。

### AEM首頁 {#aem-home}

AEM首頁是全新的集中式起點，可讓您開始在Adobe Experience Manager中管理內容、資產和網站。 AEM Home為提供個人化體驗量身打造，協助使用者根據其角色和目標順暢瀏覽AEM生態系統。 其設計旨在成為您的指南，提供重要見解和建議動作，以有效實現預期結果。 AEM首頁透過展示清晰、以人物為導向的藍圖，確保使用者快速找到達成目標所需的內容，並透過所有AEM功能支援更簡化且有效的體驗。

AEM Home可供早期採用者客戶使用，以最佳化工作流程、區分目標優先順序及推動結果的進階體驗，帶給您全新的體驗。 透過選擇加入，您有機會塑造AEM首頁的發展，提供意見回饋會影響其演化，以最好地為AEM社群服務。

如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com)。 請務必加入下列資訊：

* 最適合您設定檔的角色：內容作者、開發人員、企業所有者、管理員或其他（提供說明）。
* 您的主要AEM存取介面： AEM Sites、AEM Assets、AEM Forms、Cloud Manager或其他（提供說明）。

### 自備 Git - 現在支援 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自備 Git** 功能已進行擴展，包括對 GitLab 和 Bitbucket 等外部存放庫的支援。這項新的支援功能是對私人和企業 GitHub 存放庫現有支援的補充。當您新增這些新存放庫時，也可以將它們直接連結到您的管道。您可以將這些存放庫託管在公有雲平台上或私有雲或基礎架構內。這項整合也消除了與 Adobe 存放庫持續進行代碼同步的需求，並提供了在提取請求合併到主分支之前，驗證提取請求的功能。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，立即可用的提取請求代碼品質檢查僅限於 GitHub 託管的存放庫，但我們正在進行一項更新以將此功能擴展到其他 Git 供應商。

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) 傳送電子郵件。請務必加入您要使用的Git平台，以及您是要使用私人/公有或企業存放庫結構。—>


## 錯誤修正

* 最近的一項更新解決了SonarQube中某些情況下偵測不到硬式編碼密碼的問題。 此修正現在包含展開的模式檢查，並符合SonarQube中的預設偵測標準。<!-- CMGR-62682 -->
* 嘗試在Cloud Manager中更新SSL憑證時，在&#x200B;**[!UICONTROL 檢視和更新SSL憑證]**&#x200B;對話方塊中按一下&#x200B;**[!UICONTROL 更新]**&#x200B;後，會出現未知錯誤。<!-- CMGR-62848 -->
* 在Cloud Manager中，SSL憑證更新會失敗，並出現錯誤「新憑證不符合現有網域」，即使網域相同但字母大小寫（大寫或小寫）不同。 此更新現在會將網域識別為不區分大小寫，並符合RFC標準。<!-- CMGR-62844 -->
* 在Cloud Manager中，IP允許清單繫結停留在執行狀態，因為缺少網域設定的外部索引鍵連結。 此修正現在可確保IP允許清單繫結正確連結至關聯的網域設定。<!-- CMGR-62838 -->
* Cloud Manager會驗證SSL憑證的OCSP （線上憑證狀態通訊協定）狀態。 Adobe建議您先使用`openssl verify -untrusted intermediate.pem certificate.pem`之類的工具在本機驗證憑證的完整性，然後再透過Cloud Manager安裝。 如需詳細資訊，請參閱[SSL憑證需求檔案](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements)。<!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->