---
title: 建立生產計畫
description: 了解如何使用 Cloud Manager 建立您自己的生產計畫來主持即時流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 88%

---


# 建立生產計畫 {#create-production-program}

生產計畫適用於熟悉 AEM 和 Cloud Manager 並準備開始編寫、建構和測試程式碼以將其部署為託管即時流量的使用者。

在文件中了解有關計畫類型的更多資訊[了解計畫和計畫類型。](program-types.md)

## 建立生產計畫 {#create}

請依照以下步驟建立生產計畫。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 從畫面的右上角，按一下&#x200B;**新增計畫**。

   ![Cloud Manager 登陸頁面](assets/log-in.png)

1. 在「建立計畫」精靈中選取&#x200B;**為生產設定**&#x200B;以建立生產計畫並提供計畫名稱。

   ![建立計畫精靈](assets/create-production-program.png)

1. 或者，您可以將影像檔拖放到&#x200B;**新增計畫影像**&#x200B;目標或按一下它從檔案瀏覽器選取影像，藉此新增影像到計畫。點選或按一下&#x200B;**繼續**。

1. 如果您擁有必要的權益， **安全性** 標籤隨即顯示，並提供啟動選項 **HIPAA** 和/或 **WAF-DDOS保護** 用於您的生產計畫。 如果您正在建立的方案有需要，請核取適用的選項，然後點選或按一下 **繼續**.

   * HIPAA無法在方案建立後啟用或停用。
      * [深入了解](https://www.adobe.com/go/hipaa-ready_tw) Adobe 的 HIPAA 就緒解決方案實作方式。
   * 一旦啟動，就可以設定WAF-DDOS保護 [非生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

   ![安全性選項](assets/create-production-program-security.png)

1. 在&#x200B;**解決方案和附加元件**&#x200B;索引標籤上，選取要納入計畫中的解決方案。

   * 如果您不確定是否需要一個或多個計畫以使用各種您可用的解決方案，請選取您最感興趣的一個。您之後可以[編輯計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)來啟用其他解決方案。如需更多計畫設定建議，請參閱[生產計畫簡介文件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
   * 如果您之前選取了&#x200B;**啟用增強式安全性**，您只能選取可使用 HIPAA 權限的解決方案。

   ![選取解決方案](assets/setup-prod-select.png)

1. 按一下解決方案名稱前的 > 形圖示，即可顯示選用的附加元件，例如選擇&#x200B;**商務**&#x200B;下的附加選項 **Sites**。

   ![選取附加元件](assets/setup-prod-commerce.png)

1. 選擇您的解決方案和附加組件後，按一下&#x200B;**繼續**。

1. 在&#x200B;**上線日期**&#x200B;索引標籤，輸入您計畫上線的生產計畫的日期。

   ![缺少規劃的上線日期](assets/setup-go-live.png)

   * 這個日期可以隨時修改。
   * 此日期僅供參考，並會觸發計畫概觀頁面上的上線小工具，即時提供產品內連結至 AEM as a Cloud Service 最佳實務文件，以符合您的歷程，最終達成成功且順暢的上線體驗。

1. 按一下&#x200B;**建立**。

您的計畫由 Cloud Manager 建立，並在登陸頁面上顯示和選擇。

![Cloud Manager 概覽](assets/navigate-cm.png)

## 存取你的計畫 {#accessing}

1. 在登陸頁面上看到您的計畫卡後，選擇省略符號按鈕以查看可供您使用的選單選項。

   ![計畫概觀](assets/program-overview.png)

1. 選取&#x200B;**計畫概覽**&#x200B;導覽至 Cloud Manager 的&#x200B;**概覽**&#x200B;頁面。

1. 概覽頁面上的主要號召性用語卡片將指導您建立環境、非生產管道，最後是生產管道。

   ![計畫概觀](assets/set-up-prod5.png)

如果您在任何時候需要切換到另一個計畫或返回概覽頁面來建立另一個計畫，請按一下畫面左上角的計畫名稱以顯示&#x200B;**瀏覽**&#x200B;選項。

![瀏覽到](assets/create-program-a1.png)

>[!NOTE]
>
>不像一個[沙箱計畫](introduction-sandbox-programs.md#auto-creation)，生產計畫將要求具有相應 Cloud Manager 角色的使用者建立專案並透過自助服務 UI 新增環境。
