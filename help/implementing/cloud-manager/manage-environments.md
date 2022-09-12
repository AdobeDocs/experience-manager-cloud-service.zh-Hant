---
title: 管理環境
description: 了解您可以建立的環境類型，以及如何為Cloud Manager專案建立環境。
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# 管理環境 {#managing-environments}

了解您可以建立的環境類型，以及如何為Cloud Manager專案建立環境。

## 環境類型 {#environment-types}

具有必要權限的使用者可以建立下列環境類型（在特定租用戶可用內容的範圍內）。

* **生產與預備**  — 生產和測試環境可分別以對的形式提供，並用於生產和測試用途。

* **開發**  — 可建立開發環境以供開發及測試之用，且僅能與非生產管道相關聯。


個別環境的功能取決於容納中啟用的解決方案 [程式。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [畫面](/help/screens-cloud/home.md)

>[!NOTE]
>
>生產和測試環境僅建立為一組。 您不能僅建立測試環境，也不能僅建立生產環境。

## 新增環境 {#adding-environments}

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下要為其添加環境的程式。

1. 從 **計畫概述** 頁面，按一下 **新增環境** 在 **環境** 卡片來新增環境。

   ![環境卡](assets/no-environments.png)

   * 此 **新增環境** 選項 **環境** 標籤。

      ![環境標籤](assets/environments-tab.png)

   * 此 **新增環境** 選項可能會因為缺少權限或取決於授權資源而停用。

1. 在 **新增環境** 對話方塊中顯示：

   * 選取 **環境類型**.
      * 可用/使用的環境數量會以括弧顯示在「開發」環境類型後面。
   * 提供 **環境名稱**.
   * 提供 **環境說明**.
   * 選取 **雲區域**.

   ![「添加環境」對話框](assets/add-environment2.png)

1. 按一下 **儲存** 添加指定環境。

此 **概述** 畫面現在會在 **環境** 卡片。 您現在可以為新環境設定管道。

## 環境詳細資訊 {#viewing-environment}

您可以使用 **環境** 「概觀」頁面上的「 」卡片，可透過兩種方式存取環境詳細資訊。

1. 從 **概述** 頁面，按一下 **環境** 標籤。

   ![環境標籤](assets/environments-tab2.png)

   * 或者，按一下 **全部顯示** 按鈕 **環境** 卡片直接跳到 **環境** 標籤。

      ![顯示全部選項](assets/environment-showall.png)

1. 此 **環境** 開啟並列出程式的所有環境。

   ![環境標籤](assets/environment-view-2.png)

1. 按一下清單中的環境，以顯示其詳細資訊。

   ![環境詳細資訊](assets/environ-preview1.png)

或者，按一下所需環境的刪節號按鈕，然後選擇 **檢視詳細資料**.

![檢視環境詳細資訊](assets/view-environment-details.png)

>[!NOTE]
>
>此 **環境** 卡片僅列出三個環境。 按一下 **全部顯示** 按鈕（如前所述）以查看方案的所有環境。

### 存取預覽服務 {#access-preview-service}

Cloud Manager為每個AEMas a Cloud Service環境提供預覽服務（以額外發佈服務的形式提供）。

使用此服務，您可以在網站最終體驗到達實際發佈環境且可供公開使用之前先行預覽。

建立預覽服務時，會套用預設IP允許清單(標示為 `Preview Default [<envId>]`，會封鎖預覽服務的所有流量。 您必須主動取消從預覽服務套用預設IP允許清單，才能啟用存取權。

![預覽服務及其允許清單](assets/preview-ip-allow.png)

擁有必要權限的使用者必須先完成下列選項的步驟，才能與您的任何團隊共用預覽服務URL，以確保可存取預覽URL。

1. 建立適當的IP允許清單，將其套用至預覽服務，然後立即取消套用 `Preview Default [<envId>]` 允許清單。

   * 請參閱該文檔 [套用和取消套用IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 以取得更多詳細資訊。

1. 使用更新 **IP允許清單** 移除預設IP並視需要新增IP的工作流程。 請參閱 [管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) 了解更多。

一旦預覽服務的存取解除鎖定，預覽服務名稱前面的鎖定圖示將不再顯示。

啟動後，您可以使用AEM內的「管理出版物UI」，將內容發佈至預覽服務。 請參閱該文檔 [預覽內容](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 以取得更多詳細資訊。

>[!NOTE]
>
>您的環境必須使用AEM版本 `2021.05.5368.20210529T101701Z` 或更新版本。 請確定更新管道已在您的環境中成功執行，以執行此動作。

## 更新環境 {#updating-dev-environment}

作為雲端原生服務，生產程式中的測試和生產環境更新會由Adobe自動管理。

不過，方案內會管理開發環境以及沙箱方案中環境的更新。 當此環境未執行最新的公開可用AEM版本時， **環境** 卡 **概述** 節目螢幕將顯示 **可用更新**.

![環境更新狀態](assets/environ-update.png)

### 更新和管道 {#updates-pipelines}

管道是 [將程式碼部署至AEMas a Cloud Service的環境。](deploy-code.md) 因此，每個管道都與特定AEM版本相關聯。

如果Cloud Manager偵測到可用的AEM版本比上次透過管道部署的更新版本，便會顯示 **可用更新** 環境的狀態。

因此，更新程式是兩步驟程式：

1. 使用最新的AEM版本更新管道
1. 執行管道以將新版AEM部署至環境

### 更新環境 {#updating-your-environments}

此 **更新** 選項 **環境** 按一下環境的刪節號按鈕，即可在沙箱方案中針對開發環境和環境使用資訊卡。

![從「環境」卡更新選項](assets/environ-update2.png)

您也可以按一下 **環境** 頁簽，然後選擇環境的刪節號按鈕。

![從「環境」索引標籤更新選項](assets/environ-update3.png)

使用 **部署管理員** 角色可使用此選項將與此環境相關聯的管道更新為最新AEM版本。

管道版本更新為最新公開可用的AEM版本後，系統會提示使用者執行相關管道，將最新版本部署至環境。

![提示運行管道以更新環境](assets/update-run-pipeline.png)

此 **更新** 選項的行為會根據程式的設定和目前狀態而有所不同。

* 如果管道已更新，則 **更新** 選項會提示使用者執行管道。
* 如果管道已更新，則 **更新** 選項會通知使用者更新已執行。
* 如果適當的管道未退出，則 **更新** 選項會提示使用者建立選項。

## 刪除開發環境 {#deleting-environment}

具有必要權限的使用者將能刪除開發環境。

從 **概述** 螢幕 **環境** 卡片上，按一下您要刪除之開發環境的刪節號按鈕。

![刪除選項](assets/environ-delete.png)

您也可以從 **環境** 的 **概述** 窗口。 按一下環境的刪節號按鈕，然後選取 **刪除**.

![「環境」索引標籤中的刪除選項](assets/environ-delete2.png)

>[!NOTE]
>
>* 無法刪除在生產程式中建立的生產和測試環境。
>* 您可以刪除沙箱程式中的生產和測試環境。


## 管理存取 {#managing-access}

選擇 **管理存取** 從上面環境的刪節號菜單 **環境** 卡片。 您可以直接導覽至製作例項，並管理環境的存取權。

![管理存取選項](assets/environ-access.png)

## 存取開發人員控制台 {#accessing-developer-console}

選擇 **開發人員控制台** 從上面環境的刪節號菜單 **環境** 卡片。 這會在您的瀏覽器中開啟新標籤，其中登入頁面會顯示 **開發人員控制台**.

![](assets/environ-devconsole.png)

只有使用 **開發人員** 角色將有權存取 **開發人員控制台**. 不過，對於沙箱方案，任何具有沙箱方案存取權的使用者都可存取 **開發人員控制台**.

請參閱該文檔 [休眠和解除休眠沙箱環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) 以取得更多詳細資訊。

您也可以從 **環境** 的 **概述** 按一下個別環境的刪節號選單時顯示。

## 本機登入 {#login-locally}

選擇 **本機登入** 從 **環境** 本機登入Adobe Experience Manager的卡片。

![本機登入](assets/environ-login-locally.png)

此外，您也可以從 **環境** 的 **概述** 頁面。

![從「環境」索引標籤在本機登入](assets/environ-login-locally-2.png)

## 管理自訂網域名稱 {#manage-cdn}

Cloud Manager for Sites程式支援發佈和預覽服務的自訂網域名稱。 每個Cloud Manager環境最多可托管250個自訂網域。

若要設定自訂網域名稱，請導覽至 **環境** 標籤，然後按一下環境以檢視環境詳細資訊。

![環境詳細資訊](assets/domain-names.png)

可在您環境的發佈服務上執行下列動作。

* [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [檢查自定義域名的狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 或 [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## 管理IP允許清單 {#manage-ip-allow-lists}

Cloud Manager支援IP允許清單，以供Sites程式製作、發佈及預覽服務。

若要管理IP允許清單，請導覽至 **環境** 的 **概述** 頁面。 按一下個別環境以管理其詳細資訊。

### 套用IP允許清單 {#apply-ip-allow-list}

套用IP允許清單會將允許清單定義中包含的所有IP範圍，與環境中的製作或發佈服務建立關聯。 中的使用者 **業務負責人** 或 **部署管理員** 必須記錄角色，才能套用IP允許清單。

IP允許清單必須存在於Cloud Manager中，才能套用至環境。 若要進一步了解Cloud Manager中的IP允許清單，請參閱本檔案[Cloud Manager的IP允許清單簡介。](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

請依照下列步驟，套用IP允許清單。

1. 從導覽至特定環境 **環境** 頁簽 **概述** 畫面並導覽至 **IP允許清單** 表格。
1. 使用IP允許清單表格頂端的輸入欄位，選取IP允許清單，以及您要套用該清單的製作或發佈服務。
1. 按一下 **套用** 並確認您的提交。

### 取消套用IP允許清單 {#unapply-ip-allow-list}

取消套用IP允許清單會取消關聯環境中製作或發佈者服務中允許清單定義中包含的所有IP範圍。 中的使用者 **業務負責人** 或 **部署管理員** 必須記錄角色，才能取消套用IP允許清單。

請依照下列步驟，取消套用IP允許清單。

1. 從導覽至特定環境 **環境** 頁簽 **概述** 畫面並導覽至 **IP允許清單** 表格。
1. 識別列出您要取消套用的IP允許清單規則的列。
1. 從行末選擇刪節號按鈕。
1. 選擇 **取消套用** 並確認您的提交。
