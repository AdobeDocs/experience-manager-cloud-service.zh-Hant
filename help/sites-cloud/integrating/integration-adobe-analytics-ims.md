---
title: 與 Adobe Analytics 整合時使用的 IMS 設定
description: 瞭解與Adobe Analytics整合時使用的IMS設定
exl-id: 12bd1573-373a-4001-be71-c8f155ef6896
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 5%

---

# 與 Adobe Analytics 整合時使用的 IMS 設定 {#ims-configuration-for-integration-with-adobe-analytics}

透過Analytics Standard API整合Adobe Experience Manager as a Cloud Service (AEMaaCS)與Adobe Analytics時，需要設定Adobe IMS (Identity Management System)。 此設定是透過Adobe Developer Console實現。

>[!NOTE]
>
>AEMaaCS 2022.2.0中新增了對Adobe Analytics Standard API 2.0的支援。此版本的API支援IMS驗證。
>
>API選擇由用於AEM/Analytics整合的驗證方法驅動。
>
>如需詳細資訊，請參閱 [移轉至2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## 必備條件 {#prerequisites}

開始此程式之前：

* [Adobe支援](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html) 必須為下列專案布建您的帳戶：

   * Adobe主控台
   * Adobe Developer Console
   * Adobe Analytics和
   * Adobe IMS (Identity Management System)

* 您組織的系統管理員應使用Admin Console，將您組織中所需的開發人員新增到相關產品設定檔。

   * 這可讓特定開發人員透過使用Adobe Developer Console來啟用整合。
   * 如需詳細資訊，請參閱 [管理開發人員](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 設定IMS設定 — 產生公開金鑰 {#configuring-ims-generating-a-public-key}

設定的第一個階段是在AEM中建立IMS設定並產生公開金鑰。

1. 在AEM中開啟 **工具** 功能表。
1. 在 **安全性** 區段選取 **Adobe IMS設定**.
1. 選取 **建立** 以開啟 **Adobe IMS技術帳戶設定**.
1. 使用下方的下拉式清單 **雲端設定**，選取 **Adobe Analytics**.
1. 啟動 **建立新憑證** 並輸入新別名。
1. 確認方式 **建立憑證**.

   ![建立憑證](assets/integrate-analytics-ims-01.png)

1. 選取 **下載** (或 **下載公開金鑰**)將檔案下載至本機磁碟機，以便在下列情況下可以使用： [為Adobe Analytics與AEM的整合設定IMS](#configuring-ims-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >保持此設定開啟，以下情況下將再次需要它： [完成AEM中的IMS設定](#completing-the-ims-configuration-in-aem).

   ![下載憑證](assets/integrate-analytics-ims-02.png)

## 為Adobe Analytics與AEM的整合設定IMS {#configuring-ims-adobe-analytics-integration-with-aem}

使用Adobe Developer Console時，您需要使用Adobe Analytics (供AEM使用)建立專案（整合），然後指派所需的許可權。

### 建立專案 {#creating-the-project}

開啟Adobe Developer Console以使用AEM將使用的Adobe Analytics建立專案：

1. 開啟專案的Adobe Developer主控台：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 將會顯示您擁有的任何專案。 選取 **建立新專案**  — 位置和使用將取決於：

   * 如果您還沒有任何專案， **建立新專案** 將會是底部中心。
     ![建立新專案 — 第一個專案](assets/integration-analytics-ims-02.png)
   * 如果您已有專案，這些專案將會列示於 **建立新專案** 將位於右上方。
     ![建立新專案 — 多個專案](assets/integration-analytics-ims-03.png)


1. 選取 **新增至專案** 後面接著 **API**：

   ![開始使用您的新專案](assets/integration-analytics-ims-10.png)

1. 選取 **Adobe Analytics**，則 **下一個**：

   >[!NOTE]
   >
   >如果您已訂閱Adobe Analytics，但未看到它列出，則應檢視 [必要條件](#prerequisites).

   ![新增API](assets/integration-analytics-ims-12.png)

1. 選取 **服務帳戶(JWT)** 做為驗證型別，然後繼續使用 **下一個**：

   ![選取驗證型別](assets/integration-analytics-ims-12a.png)

1. **上傳您的公開金鑰**，完成後，請繼續 **下一個**：

   ![上傳您的公開金鑰](assets/integration-analytics-ims-13.png)

1. 檢閱認證，並繼續 **下一個**：

   ![檢閱認證](assets/integration-analytics-ims-15.png)

1. 選取所需的產品設定檔，並繼續 **儲存已設定的API**：

   ![選取所需的產品設定檔](assets/integration-analytics-ims-16.png)

1. 將會確認設定。

### 指派許可權給整合 {#assigning-privileges-to-the-integration}

您現在必須將必要的許可權指派給整合：

1. 開啟Adobe **Admin Console**：

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 導覽至 **產品** （頂端工具列），然後選取 **ADOBE ANALYTICS - &lt;*your-tenant-id*>** （從左側面板）。
1. 選取 **產品設定檔**，然後從顯示的清單中找出您所需的工作區。 例如，預設工作區。
1. 選取 **API認證**，則為所需的整合設定。
1. 選取 **編輯者** 作為 **產品角色**；而非 **觀察者**.

## 為Adobe Developer主控台整合專案儲存的詳細資訊 {#details-stored-for-the-ims-integration-project}

在Adobe Developer Console — 專案中，您可以看到所有整合專案的清單：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

選取特定專案專案以顯示有關設定的更多詳細資訊。 這些類別包括：

* 專案概述
* Insights
* 認證
   * 服務帳戶(JWT)
      * 認證詳細資料
      * 產生JWT
* API
   * 例如，Adobe Analytics

您需要其中的一些專案，才能在AEM的IMS架構中完成Adobe Analytics的整合。

## 完成AEM中的IMS設定 {#completing-the-ims-configuration-in-aem}

返回AEM後，您可以新增適用於Analytics的IMS整合中的所需值來完成IMS設定：

1. 返回 [在AEM中開啟的IMS設定](#configuring-ims-generating-a-public-key).
1. 選取 **下一個**.

1. 您可以在此處使用 [Adobe Developer Console中專案設定的詳細資料](#details-stored-for-the-ims-integration-project)：

   * **標題**：您的文字。
   * **授權伺服器**：從以下位置複製/貼上此 `aud` 行 **裝載** 下方的區段，例如， `https://ims-na1.adobelogin.com` 在以下範例中
   * **API金鑰**：從以下位置複製此專案： **認證** 部分 [專案概述](#details-stored-for-the-ims-integration-project)
   * **使用者端密碼**：在中產生此專案 [「服務帳戶(JWT)」區段的「使用者端密碼」索引標籤](#details-stored-for-the-ims-integration-project)，並複製
   * **裝載**：從以下位置複製此專案： [產生「服務帳戶(JWT)」區段的JWT標籤](#details-stored-for-the-ims-integration-project)

   ![AEM IMS設定詳細資料](assets/integrate-analytics-ims-10.png)

1. 使用&#x200B;**建立**&#x200B;確認。

1. 您的Adobe Analytics設定將顯示在AEM主控台中。

   ![IMS 設定](assets/integrate-analytics-ims-11.png)

## 確認IMS設定 {#confirming-the-ims-configuration}

若要確認設定是否如預期般運作，請執行下列動作：

1. 開啟:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. 選取您的設定。
1. 選取 **檢查健康狀態** （從工具列），後面接著 **Check**.

   ![IMS設定 — 檢查健康狀態](assets/integrate-analytics-ims-12.png)

1. 如果成功，您將看到確認訊息。

## 完成與Adobe Analytics的整合 {#complete-the-integration-with-adobe-analytics}

您現在可以使用此IMS設定來完成 [與Adobe Analytics整合](/help/sites-cloud/integrating/integrating-adobe-analytics.md).

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank, it is generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that will be sent to Adobe Analytics. 
-->
