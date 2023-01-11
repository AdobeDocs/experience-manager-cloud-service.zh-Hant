---
title: Cloud Manager 環境變數
description: 標準環境變數可以透過 Cloud Manager 進行設定和管理，並提供給執行階段環境，用於 OSGi 設定。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
source-git-commit: a8a7bd1f892c7c6eeb1753c8a55f884a33b397d4
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 88%

---


# Cloud Manager 環境變數 {#environment-variables}

可以透過 Cloud Manager 設定和管理標準環境變數。它們提供給執行階段環境並且可以在 OSGi 設定中使用。環境變數可以是特定環境的值或環境祕密，具體取決於變更的內容。

## 總覽 {#overview}

環境變數為 AEM as a Cloud Service 的使用者提供了許多好處：

* 環境變數可讓您的計劃碼和應用計劃的行為根據內容和環境而變化。例如，與生產或測試環境相比，環境變數可用於在開發環境中啟用不同的設定，以避免代價高昂的錯誤。
* 環境變數只需要設定一次，並且可以在必要時更新和刪除。
* 環境變數的值可以隨時更新並立即生效，無需任何計劃碼變更或部署。
* 環境變數可以將計劃碼與設定分開，也無須在版本控制中包含敏感資訊。
* 環境變數提高了 AEM as a Cloud Service 應用計劃的安全性，因為它們位於計劃碼之外。

使用環境變數的典型使用案例包括：

* 連接您的 AEM 應用計劃與不同的外部端點
* 在儲存密碼時使用參考而不是直接在計劃碼庫中儲存
* 當一個計畫中存在多個開發環境，且環境間的部分設定不同時

## 新增環境變數 {#add-variables}

>[!NOTE]
>
>您必須是 [**Deployment Manager** 角色](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)的成員才能新增或修改環境變數。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。
1. Cloud Manager 列出了可用的各種計畫。選擇您要管理的計畫。
1. 選擇所選計畫的&#x200B;**環境**&#x200B;索引標籤，然後在左側瀏覽面板中選擇要建立環境變數的環境。
1. 在環境的詳細資訊中，選擇&#x200B;**設定**&#x200B;索引標籤，然後選擇&#x200B;**新增**&#x200B;以打開&#x200B;**環境設定**&#x200B;對話框。
   * 如果您是第一次新增環境變數，將會在頁面中央看到&#x200B;**新增設定**&#x200B;按鈕。您可以使用此按鈕或&#x200B;**新增**&#x200B;來打開&#x200B;**環境設定**&#x200B;對話框。

   ![設定索引標籤](assets/configuration-tab.png)

1. 輸入變數詳細資訊。
   * **名稱**
   * **值**
   * **已套用服務** - 定義變數適用於哪個服務 (作者/發佈/預覽)，或適用於所有服務
   * **類型** - 定義變數是普通變數還是祕密

   ![新增變數](assets/add-variable.png)

1. 輸入新變數後，您必須在包含新變數之列的最後一欄中選擇&#x200B;**新增**。
   * 您可以透過輸入新行並選擇&#x200B;**新增**&#x200B;來一次輸入多個變數。

   ![儲存變數](assets/save-variables.png)

1. 選取「**儲存**」以儲存變數。

具有&#x200B;**更新**&#x200B;狀態的指示器會顯示在表格頂端和新增的變數旁邊，表示正在使用設定更新環境。完成後，新的環境變數將顯示在表格中。

![更新變數](assets/updating-variables.png)

>[!TIP]
>
>如果要新增多個變數，建議新增第一個變數，然後使用&#x200B;**環境設定**&#x200B;對話框中的&#x200B;**新增**&#x200B;按鈕以新增其他變數。這樣，只要更新環境一次即可新增這些變數。

## 更新環境變數 {#update-variables}

建立環境變數後，您可以使用&#x200B;**新增/更新**&#x200B;按鈕以啟動&#x200B;**環境設定**&#x200B;對話框來更新變數。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。
1. Cloud Manager 列出了可用的各種計畫。選擇您要管理的計畫。
1. 選擇&#x200B;**環境**&#x200B;所選計畫的索引標籤，然後在左側瀏覽面板中選擇要為其建立環境變數的環境。
1. 在環境的詳細資訊中，選擇&#x200B;**設定**&#x200B;索引標籤，然後在右上角選擇&#x200B;**新增更新**&#x200B;以打開&#x200B;**環境設定**&#x200B;對話框。

   ![變數的新增/更新按鈕](assets/add-update-variables.png)

1. 使用要修改變數之列最後一欄中的省略符號按鈕，選擇&#x200B;**編輯**&#x200B;或&#x200B;**刪除**。

   ![編輯或刪除變數](assets/edit-delete-variable.png)

1. 根據需要編輯環境變數。
   * 編輯時，省略符號按鈕將變更為選項以恢復原始值或確認您的變更。
   * 編輯祕密時，只能更新值，不能查看。

   ![編輯變數](assets/edit-variable.png)

1. 完成所有必需的設定變更後，選擇&#x200B;**儲存**。

[新增變數時](#add-variables)，具有&#x200B;**更新**&#x200B;狀態的指示器會顯示在表格頂端和更新的變數旁邊，表示正在使用設定更新環境。完成後，更新的環境變數將顯示在表格中。

>[!TIP]
>
>如果要更新多個變數，建議使用&#x200B;**環境設定**&#x200B;對話框，在點選或按一下&#x200B;**儲存**&#x200B;之前立即更新所有必要的變數。這樣，只要更新環境一次即可新增這些變數。

## 使用環境變數 {#using}

環境變數可讓您的 `pom.xml` 設定更加安全和靈活。例如，密碼不需要硬式編碼，您的設定可以根據環境變數中的值進行調整。

您可以透過 XML 存取環境變數和祕密，如下所示。

* `${env.VARIABLE_NAME}`

有關如何在 `pom.xml` 檔案中使用這兩種類型變數的範例，請參見文件：[設定專案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)。

如需詳細資訊，請參閱[正式 Maven 文件](https://maven.apache.org/settings.html#quick-overview)。

## 環境變數可用性 {#availability}

環境變數可用於多個位置。

### 製作、預覽和發佈 {#author-preview-publish}

一般環境變數和機密都可用於製作、預覽和發佈環境。

### Dispatcher {#dispatcher}

只有一般環境變數可搭配使用 [調度程式。](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 無法使用機密。

不過，環境變數無法用於 `IfDefine` 指令。

>[!TIP]
>
>您應驗證是否使用環境變數搭配 [本機](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) 部署前。

### OSGi配置 {#osgi}

規則環境變數和機密皆可用於 [OSGi設定。](/help/implementing/deploying/configuring-osgi.md)

### 管道變數 {#pipeline}

除了環境變數外，還有管線變數，這些變數會在建置階段公開。 [如需管道變數的詳細資訊，請參閱這裡。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)
