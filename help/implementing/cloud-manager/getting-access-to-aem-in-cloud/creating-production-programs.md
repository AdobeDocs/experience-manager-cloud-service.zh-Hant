---
title: 建立生產計畫
description: 了解如何使用 Cloud Manager 建立您自己的生產計畫來主持即時流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: a25f1c674534792353cb9b34d4f88a5e32230bc1
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 33%

---


# 建立生產計畫 {#create-production-program}

生產計畫適用於熟悉 AEM 和 Cloud Manager 並準備開始編寫、建構和測試程式碼以將其部署為託管即時流量的使用者。

在文件中了解有關計畫類型的更多資訊[了解計畫和計畫類型。](program-types.md)

## 建立生產計畫 {#create}

請依照以下步驟建立生產計畫。 請注意，根據您組織的權益，您可能會看到 [其他選項](#options) 新增您的程式時。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在 **[我的計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 熒幕，點選或按一下 **新增計畫** 在畫面的右上角。

   ![Cloud Manager 登陸頁面](assets/log-in.png)

1. 在「建立計畫」精靈中選取&#x200B;**為生產設定**&#x200B;以建立生產計畫並提供計畫名稱。

   ![建立計畫精靈](assets/create-production-program.png)

1. 或者，您可以將影像檔拖放到&#x200B;**新增計畫影像**&#x200B;目標或按一下它從檔案瀏覽器選取影像，藉此新增影像到計畫。選取「**繼續**」。

1. 在&#x200B;**解決方案和附加元件**&#x200B;索引標籤上，選取要納入計畫中的解決方案。

   * 如果您不確定是否需要一個或多個計畫以使用各種您可用的解決方案，請選取您最感興趣的一個。您之後可以[編輯計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)來啟用其他解決方案。如需更多計畫設定建議，請參閱[生產計畫簡介文件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
   * 程式建立至少需要一個解決方案。
   * 如果您已選取 **[啟用增強式安全性](#security)** 選項，您只能選取可使用HIPAA許可權的解決方案。

   ![選取解決方案](assets/setup-prod-select.png)

1. 按一下解決方案名稱前的>形圖示，即可顯示選用的附加元件，例如選取 **商務** 下的附加選項 **網站**.

   ![選取附加元件](assets/setup-prod-commerce.png)

1. 選擇您的解決方案和附加組件後，按一下&#x200B;**繼續**。

1. 在&#x200B;**上線日期**&#x200B;索引標籤，輸入您計畫上線的生產計畫的日期。

   ![缺少規劃的上線日期](assets/setup-go-live.png)

   * 這個日期可以隨時修改。
   * 此日期僅供參考，並會在以下位置觸發上線Widget： [**計畫總覽** 頁面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) 及時提供AEMas a Cloud Service最佳實務檔案的產品內連結，以符合您的歷程，最終達成成功且順暢的上線體驗。

1. 按一下&#x200B;**建立**。

您的計畫由 Cloud Manager 建立，並在登陸頁面上顯示和選擇。

![Cloud Manager 概覽](assets/navigate-cm.png)

## 其他生產計畫選項 {#options}

根據您的組織可用的權益，當您建立生產計畫時，可能有其他選項可供您使用。

### 安全性 {#security}

如果您擁有必要的權益， **安全性** 標籤會顯示為 **為生產設定** 對話方塊。

此 **安全性** 索引標籤提供啟動選項 **HIPAA** 和/或 **WAF-DDOS保護** 用於您的生產計畫。

符合HIPAA規範的Adobe和Web應用程式防火牆(WAF)有助於雲端式安全性，是防範漏洞的多層方法的一部分。

* **HIPAA**  — 此選項可啟用Adobe的HIPPA就緒解決方案實作。
   * [深入了解](https://www.adobe.com/go/hipaa-ready_tw) Adobe 的 HIPAA 就緒解決方案實作方式。
   * HIPAA無法在方案建立後啟用或停用。
* **WAF-DDOS保護**  — 此選項會透過規則啟用Web應用程式防火牆，以保護您的應用程式。
   * 一旦啟動，就可以設定WAF-DDOS保護 [非生產管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * 檢視檔案 [包含WAF規則的流量篩選規則](/help/security/traffic-filter-rules-including-waf.md) 以瞭解如何管理存放庫中的流量篩選規則，以便正確部署。

![安全性選項](assets/create-production-program-security.png)

### SLA {#sla}

如果您擁有必要的權益， **SLA** 標籤會顯示為中的第二個或第三個標籤 **為生產設定** 對話方塊。

AEM Sites提供標準的99.9%服務等級協定(SLA)。 此 **99.99%服務等級協定** 選項可為您的生產環境啟用99.99%的最低連續運作時間百分比。

99.99% SLA的優點包括更高的可用性和更低的延遲，並且需要 [其他發佈區域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 要套用至計畫中的生產環境。

![SLA選項](assets/create-production-program-sla.png)

一旦 [需求](#sla-requirements) 若要啟用99.99%的SLA，您必須執行 [完整棧疊管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 以啟動它。

#### 99.99% SLA的要求 {#sla-requirements}

除了必要的權利要求之外，99.99%的SLA還有額外的使用要求。

* 在將99.99% SLA套用至方案時，組織必須同時具有99.99% SLA和額外的發佈區域權益。
* 為了將99.99% SLA套用至計畫，Cloud Manager將檢查以確保未使用 [其他發佈區域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 權利也可用，並且可以套用至方案。
* 編輯方案時，如果方案已包含具有至少一個額外發佈區域的生產環境，則Cloud Manager僅檢查99.99% SLA權利的可用性。
* 為了啟用99.99%的SLA和報告， [生產/中繼環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 必須已建立，且生產/中繼環境上必須至少已套用一個其他發佈區域。
   * 若使用 [進階網路、](/help/security/configuring-advanced-networking.md) 請務必檢視 [將多個發佈區域新增到新環境](/help/implementing/cloud-manager/manage-environments.md#adding-regions) 建議檔案，以便在區域故障時維持連線。
* 您的99.99% SLA方案中必須至少保留一個額外的發佈區域。 不允許使用者從99.99% SLA方案中刪除最後一個額外的發佈區域。
* 99.99% SLA支援已啟用Sites解決方案的生產計畫。
* 您必須執行 [完整棧疊管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 為了啟動（或在編輯方案時停用） 99.99% SLA。

## 存取你的計畫 {#accessing}

1. 當您在登陸頁面上看到您的計畫卡時，選擇省略符號按鈕以檢視您可以使用的選單選項。

   ![計畫概觀](assets/program-overview.png)

1. 選取&#x200B;**計畫概覽**&#x200B;導覽至 Cloud Manager 的&#x200B;**概覽**&#x200B;頁面。

1. 概覽頁面上的主要號召性用語卡片將指導您建立環境、非生產管道，最後是生產管道。

   ![計畫概觀](assets/set-up-prod5.png)

如果您在任何時候需要切換到另一個計畫或返回概覽頁面來建立另一個計畫，請按一下畫面左上角的計畫名稱以顯示 **瀏覽至** 選項。

![瀏覽到](assets/create-program-a1.png)

>[!NOTE]
>
>不像一個[沙箱計畫](introduction-sandbox-programs.md#auto-creation)，生產計畫將要求具有相應 Cloud Manager 角色的使用者建立專案並透過自助服務 UI 新增環境。
