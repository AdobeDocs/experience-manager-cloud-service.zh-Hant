---
title: 管理環境
description: 了解您可以建立的環境類型，以及如何為您的 Cloud Manager 專案建立環境類型。
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: ht
source-wordcount: '1745'
ht-degree: 100%

---

# 管理環境 {#managing-environments}

了解您可以建立的環境類型，以及如何為您的 Cloud Manager 專案建立環境類型。

## 環境類型 {#environment-types}

具有必要權限的使用者可以建立以下環境類型 (在特定租使用者可用的範圍內)。

* **生產與測試** - 生產環境和測試環境組成一組使用，分別用於生產和測試目的。

* **開發** - 可以為開發和測試目的建立開發環境，並且只能與非生產管道相關聯。


各個環境的功能取決於包含在[計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)中啟用的解決方案。

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [畫面](/help/screens-cloud/home.md)

>[!NOTE]
>
>生產和測試環境都是以一組建立。您不能只建立一個測試環境或只建立一個生產環境。

## 新增一個環境 {#adding-environments}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要新增環境的方案。

1. 在&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**新增環境**&#x200B;以新增環境。

   ![環境卡](assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

      ![「環境」索引標籤](assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選取&#x200B;**環境類型**。
      * 可用/已使用環境的數量會顯示在開發環境類型後面的括號中。
   * 提供&#x200B;**環境名稱**。
   * 提供&#x200B;**環境說明**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](assets/add-environment2.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

現在&#x200B;**總覽**&#x200B;畫面會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。現在您可以設定新環境的管道。

## 環境詳細資訊 {#viewing-environment}

您可以使用總覽頁面上的&#x200B;**環境**&#x200B;卡以兩種方式存取環境詳細資訊。

1. 在&#x200B;**總覽**&#x200B;頁面，按一下畫面頂端的&#x200B;**環境**&#x200B;索引標籤。

   ![「環境」索引標籤](assets/environments-tab2.png)

   * 或者，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**全部顯示**&#x200B;按鈕直接跳到&#x200B;**環境**&#x200B;索引標籤。

      ![顯示全部選項](assets/environment-showall.png)

1. **環境**&#x200B;隨即開啟並列出該計畫的所有環境。

   ![環境索引標籤](assets/environment-view-2.png)

1. 按一下清單中的環境以顯示其詳細資訊。

   ![環境詳細資訊](assets/environ-preview1.png)

或者，按一下所需環境的省略符號按鈕，然後選擇&#x200B;**查看詳細資訊**。

![檢視環境詳細資訊](assets/view-environment-details.png)

>[!NOTE]
>
>新環境列在&#x200B;**環境**&#x200B;卡只會列出三個環境。如前所述，按一下&#x200B;**顯示全部**&#x200B;按鈕以查看計畫的所有環境。

### 存取預覽服務 {#access-preview-service}

Cloud Manager 為每個 AEM as a Cloud Service 環境提供預覽服務 (作為附加發佈服務提供)。

使用該服務，您可以在網站到達實際發佈環境並公開使用之前預覽網站的最終體驗。

建立後，預覽服務將套用預設的 IP 允許清單，標記為 `Preview Default [<envId>]`，其會封鎖所有流向預覽服務的流量。您必須主動從預覽服務中取消套用預設的 IP 允許清單才能啟用存取。

![預覽服務和其允許清單](assets/preview-ip-allow.png)

具有必要權限的使用者必須在與您的任何團隊共用預覽服務 URL 之前完成以下選項的步驟，以確保存取預覽 URL。

1. 建立適當的 IP 允許清單，將其套用於預覽服務，然後立即取消套用 `Preview Default [<envId>]` 允許清單。

   * 如需了解詳細資訊，請參閱文件：[套用和取消套用 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)。

1. 使用更新 **IP 允許清單**&#x200B;工作流程移除預設 IP，並依需要新增 IP。如需了解更多，請參閱[管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md)。

解鎖預覽服務的存取權後，預覽服務名稱前面的鎖定圖示將不再顯示。

啟動後，您可以使用 AEM 中的管理發佈 UI 將內容發佈到預覽服務。如需更多詳細資訊，請參閱文件：[預覽內容](/help/sites-cloud/authoring/fundamentals/previewing-content.md)。

>[!NOTE]
>
>您的環境必須是 AEM 版本 `2021.05.5368.20210529T101701Z` 或更新版本。確保更新管道已在您的環境中成功執行以執行此操作。

## 更新環境 {#updating-dev-environment}

作為雲端原生服務，Adobe 會自動管理生產計畫中的測試和生產環境的更新。

但開發環境更新和沙箱計畫中的環境更新是在計畫中管理的。當這類環境未執行最新的公開 AEM 版本時，計畫的&#x200B;**總覽**&#x200B;中&#x200B;**環境**&#x200B;卡上的狀態將顯示&#x200B;**可用更新**。

![環境更新狀態](assets/environ-update.png)

### 更新和管道 {#updates-pipelines}

管道是將 [ 計劃碼部署到 AEM as a Cloud Service 環境的唯一途徑。](deploy-code.md)因此，每個管道都與特定的 AEM 版本相關聯。

如果 Cloud Manager 偵測到可用的 AEM 版本比上次使用的管道部署版本還新，它會顯示環境的&#x200B;**可用更新**&#x200B;狀態。

因此，更新流程分為兩個步驟：

1. 使用最新的 AEM 版本更新管道
1. 執行管道以將新版本的 AEM 部署到環境

### 更新您的環境 {#updating-your-environments}

按一下環境的省略符號按鈕，可以從&#x200B;**環境**&#x200B;卡中取得用於開發環境和沙箱計畫中環境的&#x200B;**更新**&#x200B;選項。

![更新環境卡的選項](assets/environ-update2.png)

也可以按一下計畫的&#x200B;**環境**&#x200B;索引標籤，然後選擇環境的省略符號按鈕來使用此選項。

![更新環境索引標籤的選項](assets/environ-update3.png)

具有&#x200B;**部署管理員**&#x200B;角色的使用者可以使用此選項將與此環境關聯的管道更新到最新的 AEM 版本。

管道版本更新到最新公開的 AEM 版本後，系統會提示使用者執行關聯的管道以將最新版本部署到環境中。

![提示執行管道以更新環境](assets/update-run-pipeline.png)

**更新**&#x200B;選項的行為取決於計畫的設定和目前狀態。

* 如果管道已經更新，則&#x200B;**更新**&#x200B;選項會提示使用者執行管道。
* 如果管道已經在更新，則&#x200B;**更新**&#x200B;選項會通知使用者更新已經在執行。
* 如果不存在適當的管道，則&#x200B;**更新**&#x200B;選項會提示使用者建立管道。

## 刪除開發環境 {#deleting-environment}

具有必要權限的使用者將能夠刪除開發環境。

在&#x200B;**環境**&#x200B;卡上計畫的&#x200B;**總覽**&#x200B;畫面中，按一下要刪除的開發環境的省略符號按鈕。

![刪除選項](assets/environ-delete.png)

刪除選項也可在計畫&#x200B;**總覽**&#x200B;視窗的&#x200B;**環境**&#x200B;索引標籤中找到。按一下環境的省略符號按鈕，然後選擇&#x200B;**刪除**。

![環境索引標籤的刪除選項](assets/environ-delete2.png)

>[!NOTE]
>
>* 不能刪除在生產計畫中建立的生產環境和測試環境。
>* 不能刪除在沙箱計畫中的生產和測試環境。


## 管理存取權 {#managing-access}

從&#x200B;**環境**&#x200B;卡上環境的省略符號選單中選擇&#x200B;**管理存取權**。您可以直接瀏覽到作者執行個體，管理您環境的存取權。

![管理存取權選項](assets/environ-access.png)

## 存取開發人員主控台 {#accessing-developer-console}

從&#x200B;**環境**&#x200B;卡上環境的省略符號選單中選擇&#x200B;**開發人員主控台**。這將在您的瀏覽器中打開一個新索引標籤，其中包含 **Developer Console** 的登入頁面。

![](assets/environ-devconsole.png)

只有具有&#x200B;**開發人員**&#x200B;角色的使用者才能存取&#x200B;**開發人員主控台**。但是對於沙箱計畫，任何有權存取沙箱計畫的使用者都可以存取&#x200B;**開發人員主控台**。

如需了解詳細資訊，請參閱文件：[休眠和去休眠沙箱環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html?lang=zh-Hant#hibernating-introduction)。

按一下個別環境的省略符號選單時，此選項也可從&#x200B;**總覽**&#x200B;視窗的&#x200B;**環境**&#x200B;索引標籤中使用。

## 本機登入 {#login-locally}

從&#x200B;**環境**&#x200B;卡中環境的省略符號選單中選擇&#x200B;**本機登入**，以本機登入到 Adobe Experience Manager。

![本機登入](assets/environ-login-locally.png)

此外，您可以從&#x200B;**總覽**&#x200B;頁面的&#x200B;**環境**&#x200B;索引標籤本機登入。

![從環境索引標籤本機登入](assets/environ-login-locally-2.png)

## 管理客戶網域名稱 {#manage-cdn}

Cloud Manager 支援 Sites 計畫的發佈和預覽服務的自訂網域名稱。每個 Cloud Manager 環境最多可以託管 250 個自訂網域。

要設定自訂網域名稱，請瀏覽到&#x200B;**環境**&#x200B;索引標籤，然後按一下環境以查看環境詳細資訊。

![環境詳細資訊](assets/domain-names.png)

可以對您的環境的發佈服務執行以下動作。

* [新增客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [管理客戶網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)或 [SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)。

* [管理 IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## 管理 IP 允許清單 {#manage-ip-allow-lists}

Cloud Manager 支援 IP 允許清單，用於 Sites 計畫的作者、發佈和預覽服務。

要管理 IP 允許清單，請瀏覽到計畫&#x200B;**總覽**&#x200B;頁面的&#x200B;**環境**&#x200B;索引標籤。按一下單個環境以管理其詳細資訊。

### 套用 IP 允許清單 {#apply-ip-allow-list}

套用 IP 允許清單會將允許清單定義中包含的所有 IP 範圍與環境中的作者或發佈服務相關聯。擁有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者必須登入才能套用 IP 允許清單。

IP 允許清單必須存在於 Cloud Manager 中才能將其套用於環境。要了解有關 Cloud Manager 中 IP 允許清單的更多資訊，請參閱文件：[Cloud Manager 中的 IP 允許清單簡介。](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

請按照以下步驟套用 IP 允許清單。

1. 從計劃&#x200B;**總覽**&#x200B;畫面的&#x200B;**環境**&#x200B;索引標籤瀏覽到特定環境，然後瀏覽到 **IP 允許清單**。
1. 使用 IP 允許清單表頂端的輸入欄位來選擇 IP 允許清單，和您希望將其套用到的作者或發佈服務。
1. 按一下&#x200B;**套用**，然後確認您的訂閱。

### 取消套用 IP 允許清單 {#unapply-ip-allow-list}

取消套用 IP 允許清單將取消包含在允許清單定義中的所有 IP 範圍與環境中的作者或發佈者服務的關聯。擁有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者必須登入才能取消套用 IP 允許清單。

請按照以下步驟取消套用 IP 允許清單。

1. 從計劃&#x200B;**總覽**&#x200B;畫面的&#x200B;**環境**&#x200B;索引標籤瀏覽到特定環境，然後瀏覽到 **IP 允許清單**。
1. 確定已列出要取消套用 IP 允許清單規則的列。
1. 從列尾選擇省略符號按鈕。
1. 選取&#x200B;**取消套用**，然後確認您的訂閱。
