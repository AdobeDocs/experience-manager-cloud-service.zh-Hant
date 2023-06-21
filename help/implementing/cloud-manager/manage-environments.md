---
title: 管理環境
description: 瞭解您可以建立的環境型別，以及如何為您的Cloud Manager專案建立環境型別。
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 48%

---


# 管理環境 {#managing-environments}

瞭解您可以建立的環境型別，以及如何為您的Cloud Manager專案建立環境型別。

## 環境類型 {#environment-types}

具有必要權限的使用者可以建立以下環境類型 (在特定租使用者可用的範圍內)。

* **生產 + 測試** - 生產環境和測試環境組成一組使用，分別用於生產和測試目的。

* **開發** - 可以為開發和測試目的建立開發環境，也可以只與非生產管道相關聯。

* **快速開發**  — 快速開發環境(RDE)可讓開發人員快速部署和檢閱變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。 另請參閱 [快速開發環境檔案](/help/implementing/developing/introduction/rapid-development-environments.md) 瞭解如何使用RDE的詳細資訊。

各個環境的功能取決於環境[計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中啟用的解決方案。

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [畫面](/help/screens-cloud/home.md)

>[!NOTE]
>
>生產和測試環境都是以一組建立。您不能只建立測試環境或只建立生產環境。

## 新增一個環境 {#adding-environments}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要新增環境的計畫。

1. 從 **計畫總覽** 頁面，按一下 **新增環境** 於 **環境** 卡片以新增環境。

   ![環境卡](assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

     ![「環境」索引標籤](assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選取&#x200B;[**環境類型**。](#environment-types)
      * 可用/已使用環境的數量會顯示在環境類型名稱後面的括號中。
   * 提供環境&#x200B;**名稱**。
   * 提供環境&#x200B;**說明**。
   * 如果您要新增 **生產+中繼** 環境，您必須提供生產和中繼環境的環境名稱和說明。
   * 從下拉清單中選取一個&#x200B;**主要區域**。
      * 建立後無法變更主要區域。
      * 根據您可用的權益，您或許可以設定 [多個區域](#multiple-regions).

   ![新增環境對話框](assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

現在&#x200B;**總覽**&#x200B;畫面會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。現在您可以設定新環境的管道。

## 多個發佈區域 {#multiple-regions}

使用者具有 **業務負責人** 角色可以設定生產和測試環境，以便在主要區域之外包括最多三個額外的發佈區域。 額外的發佈區域可提高可用性。如需詳細資訊，請參閱[「額外發佈區域」文件](/help/operations/additional-publish-regions.md)。

>[!TIP]
>
>您可以使用 [Cloud Manager  API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) 查詢可用區域的最新清單。

### 將多個發佈區域新增至新環境 {#add-regions}

新增環境時，您可以選擇設定主要區域以外的其他區域。

1. 選取&#x200B;**主要區域**。
   * 建立環境後無法變更主要區域。
1. 選取選項 **新增其他發佈區域** 和新的 **其他發佈區域** 選項下拉式清單隨即顯示。
1. 在 **其他發佈區域** 從下拉式清單中選取額外的區域。
1. 選取區域會新增到下拉式清單下方以顯示其選取範圍。
   * 點選或按一下 `X` ，以便取消選取。
1. 從「**額外發佈區域**」下拉式清單中選取另一個區域，以新增另一個區域。
1. 準備要建立環境時，點選或按一下「**儲存**」。

![選取多個區域](assets/select-multiple-regions.png)

所選區域同時適用於生產和中繼環境。

如果您未指定任何額外區域，[您可以稍後在建立環境後再執行此步驟。](#edit-regions)

如果您想要布建 [進階網路](/help/security/configuring-advanced-networking.md) 對於方案，建議先完成此布建，再使用Cloud Manager API將其他發佈區域新增到環境。 否則，其他發佈區域的流量會流經主要區域的Proxy。

### 編輯多個發佈區域 {#edit-regions}

如果您最初沒有指定任何額外區域，並且您擁有必要的權益，則可以在建立環境後再執行此步驟。

您也可以移除額外發佈區域。但是，在一次異動中，您只能新增或移除區域。如果您必須新增一個區域並移除一個區域，請先新增、儲存變更，然後移除（反之亦然）。

1. 從計畫的「計畫概觀」主控台中，按一下生產環境的省略號按鈕並從選單中選取「**編輯**」。

   ![編輯環境](assets/select-edit-environment.png)

1. 在「**編輯生產環境**」對話框中，對額外發佈區域進行必要的變更。
   * 使用「**額外發佈區域**」下拉式清單，以選取額外區域。
   * 按一下選取的額外發佈區域旁邊的 X，即可將其取消選取。

   ![編輯環境](assets/edit-environment.png)

1. 點選或按一下「**儲存**」，以儲存變更。

對生產環境所做的變更會同時套用至生產和中繼環境。 只能在生產環境中編輯對多個發佈區域的變更。

如果您想要布建 [進階網路](/help/security/configuring-advanced-networking.md) 對於方案，建議先完成此布建，然後再將其他發佈區域新增到環境。 否則，其他發佈區域的流量會流經主要區域的Proxy。

## 環境詳細資訊 {#viewing-environment}

您可以使用 **環境** 卡片（在概覽頁面上）可透過兩種方式存取環境的詳細資訊。

1. 從 **概觀** 頁面，按一下 **環境** tab鍵來切換畫面。

   ![「環境」索引標籤](assets/environments-tab2.png)

   * 或者，按一下 **全部顯示** 上的按鈕 **環境** 卡片直接跳至 **環境** 標籤。

     ![顯示全部選項](assets/environment-showall.png)

1. **環境**&#x200B;隨即開啟並列出該計畫的所有環境。

   ![環境索引標籤](assets/environment-view-2.png)

1. 按一下清單中的環境，即可顯示其詳細資訊。

   ![環境詳細資訊](assets/environ-preview1.png)

或者，按一下所需環境的省略符號按鈕，然後選擇&#x200B;**查看詳細資訊**。

![檢視環境詳細資訊](assets/view-environment-details.png)

>[!NOTE]
>
>新環境列在&#x200B;**環境**&#x200B;卡只會列出三個環境。按一下 **全部顯示** 如前所述，檢視計畫的所有環境。

### 存取預覽服務 {#access-preview-service}

Cloud Manager為每個AEMas a Cloud Service環境提供預覽服務（作為額外發佈服務提供）。

使用該服務，您可以在網站到達實際發佈環境並公開使用之前預覽網站的最終體驗。

建立時，預覽服務套用預設的IP允許清單，標籤為 `Preview Default [<envId>]`，會封鎖所有流向預覽服務的流量。 從預覽服務中取消套用預設的IP允許清單，以便您可以啟用存取。

![預覽服務和其允許清單](assets/preview-ip-allow.png)

具有必要許可權的使用者必須在共用預覽服務URL之前完成以下步驟，以確儲存取它。

1. 建立適當的IP允許清單，將其套用至預覽服務，然後立即取消套用 `Preview Default [<envId>]` 允許清單。

   * 另請參閱 [套用和取消套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 以取得更多詳細資料。

1. 使用更新 **IP 允許清單**&#x200B;工作流程移除預設 IP，並依需要新增 IP。如需了解更多，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md)。

解鎖預覽服務的存取權後，預覽服務名稱前面的鎖定圖示不再顯示。

啟動後，您可以使用 AEM 中的管理發佈 UI 將內容發佈到預覽服務。另請參閱 [預覽內容](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 以取得更多詳細資料。

>[!NOTE]
>
>您的環境必須在 AEM 版本 `2021.05.5368.20210529T101701Z` 或更高版本才能使用預覽服務。請確定更新管道已在您的環境中成功執行，以便您可以使用預覽服務。

## 更新環境 {#updating-dev-environment}

作為雲端原生服務，Adobe 會自動管理生產計畫中的測試和生產環境的更新。

但是，對開發環境和沙箱計畫中環境的更新是在計畫中管理的。 當這類環境未執行最新的公開AEM版本時， **環境** 卡在上 **概觀** 計畫的畫面顯示 **有可用的更新**.

![環境更新狀態](assets/environ-update.png)

### 更新和管道 {#updates-pipelines}

管道是將 [ 計劃碼部署到 AEM as a Cloud Service 環境的唯一途徑。](deploy-code.md)因此，每個管道都與特定的 AEM 版本相關聯。

如果Cloud Manager偵測到可用的AEM版本比上次使用管道部署時更新，則會顯示 **有可用的更新** 環境的狀態。

因此，更新流程分為兩個步驟：

1. 使用最新的 AEM 版本更新管道
1. 執行管道以將新版本的 AEM 部署到環境

### 更新您的環境 {#updating-your-environments}

此 **更新** 選項可從以下網址取得： **環境** 按一下環境的省略符號按鈕，在沙箱程式中用於開發環境和環境的卡片。

![更新環境卡的選項](assets/environ-update2.png)

您也可以按一下 **環境** 索引標籤，然後選取環境的省略符號按鈕。

![更新環境索引標籤的選項](assets/environ-update3.png)

具有&#x200B;**部署管理員**&#x200B;角色的使用者可以使用此選項將與此環境關聯的管道更新到最新的 AEM 版本。

管道版本更新到最新公開的 AEM 版本後，系統會提示使用者執行關聯的管道以將最新版本部署到環境中。

![提示執行管道以更新環境](assets/update-run-pipeline.png)

**更新**&#x200B;選項的行為取決於計畫的設定和目前狀態。

* 如果管道已經更新，則&#x200B;**更新**&#x200B;選項會提示使用者執行管道。
* 如果管道已經在更新，則&#x200B;**更新**&#x200B;選項會通知使用者更新已經在執行。
* 如果不存在適當的管道，則&#x200B;**更新**&#x200B;選項會提示使用者建立管道。

## 刪除開發環境 {#deleting-environment}

具有必要許可權的使用者可以刪除開發環境。

從 **概觀** 上的程式畫面 **環境** 卡片上，按一下您要刪除之開發環境的省略符號按鈕。

![刪除選項](assets/environ-delete.png)

刪除選項也可在計畫&#x200B;**總覽**&#x200B;視窗的&#x200B;**環境**&#x200B;索引標籤中找到。按一下環境的省略符號按鈕並選取 **刪除**.

![環境索引標籤的刪除選項](assets/environ-delete2.png)

>[!NOTE]
>
>* 無法刪除在生產計畫中建立的生產和中繼環境。
>* 不能刪除在沙箱計畫中的生產和測試環境。

## 管理存取權 {#managing-access}

從&#x200B;**環境**&#x200B;卡上環境的省略符號選單中選擇&#x200B;**管理存取權**。您可以直接瀏覽到作者執行個體，管理您環境的存取權。

![管理存取權選項](assets/environ-access.png)

>[!TIP]
>
>另請參閱 [AEMas a Cloud Service團隊和產品設定檔](/help/onboarding/aem-cs-team-product-profiles.md) 如果您想瞭解AEMas a Cloud Service團隊和產品設定檔如何能夠授與和限制您的授權Adobe解決方案的存取權。

## 存取開發人員主控台 {#accessing-developer-console}

從&#x200B;**環境**&#x200B;卡上環境的省略符號選單中選擇&#x200B;**開發人員主控台**。您的瀏覽器中會開啟一個新索引標籤，其中的「登入」頁面為 **開發人員主控台**.

![登入開發人員主控台](assets/environ-devconsole.png)

僅限具有下列條件的使用者： **開發人員** 角色可以存取 **開發人員主控台**. 但是，對於沙箱計畫，任何有權存取沙箱計畫的使用者都可以存取 **開發人員主控台**.

另請參閱 [使沙箱環境休眠和解除沙箱環境休眠](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html#hibernation) 以取得更多詳細資料。

按一下個別環境的省略符號選單時，此選項也可從&#x200B;**總覽**&#x200B;視窗的&#x200B;**環境**&#x200B;索引標籤中使用。

## 本機登入 {#login-locally}

選取 **本機登入** 從環境的省略符號選單 **環境** 卡片，方便您在本機登入Adobe Experience Manager。

![本機登入](assets/environ-login-locally.png)

此外，您也可以從以下位置本機登入： **環境** 的標籤 **概觀** 頁面。

![從環境索引標籤本機登入](assets/environ-login-locally-2.png)

## 管理客戶網域名稱 {#manage-cdn}

Cloud Manager 支援 Sites 計畫的發佈和預覽服務的自訂網域名稱。每個 Cloud Manager 環境最多可以託管 250 個自訂網域。

若要設定自訂網域名稱，請導覽至 **環境** 標籤並按一下環境以檢視環境詳細資訊。

![環境詳細資訊](assets/domain-names.png)

可以對您的環境的發佈服務執行以下動作。

* [新增客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [管理客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)或 [SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)。

* [管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## 管理 IP 允許清單 {#manage-ip-allow-lists}

Cloud Manager支援IP允許清單，用於Sites計畫的作者、發佈和預覽服務。

若要管理IP允許清單，請瀏覽至 **環境** 的標籤 **概觀** 程式頁面。 按一下個別環境，即可管理其詳細資訊。

### 套用 IP 允許清單 {#apply-ip-allow-list}

套用IP允許清單會將允許清單定義中包含的所有IP範圍與環境中的作者或發佈服務相關聯。 中的使用者 **業務負責人** 或 **部署管理員** 角色必須登入才能套用IP允許清單。

IP允許清單必須存在於Cloud Manager中才能將其套用至環境。 若要深入瞭解Cloud Manager中的IP允許清單，請參閱 [Cloud Manager中的IP允許清單簡介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

**若要套用IP允許清單：**

1. 從計劃&#x200B;**總覽**&#x200B;畫面的&#x200B;**環境**&#x200B;索引標籤瀏覽到特定環境，然後瀏覽到 **IP 允許清單**。
1. 使用IP允許清單表頂端的輸入欄位，以便您可以選取IP允許清單以及要將其套用到的作者或發佈服務。
1. 按一下&#x200B;**套用**，然後確認您的訂閱。

### 取消套用IP允許清單 {#unapply-ip-allow-list}

取消套用IP允許清單會取消包含在允許清單定義中的所有IP範圍與環境中的作者或發佈者服務的關聯。 中的使用者 **業務負責人** 或 **部署管理員** 角色必須登入才能取消套用IP允許清單。

**若要取消套用IP允許清單：**

1. 從計劃&#x200B;**總覽**&#x200B;畫面的&#x200B;**環境**&#x200B;索引標籤瀏覽到特定環境，然後瀏覽到 **IP 允許清單**。
1. 識別列出要取消套用IP允許清單規則的列。
1. 從列尾選擇省略符號按鈕。
1. 選取&#x200B;**取消套用**，然後確認您的訂閱。
