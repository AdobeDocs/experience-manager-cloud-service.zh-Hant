---
title: Cloud Manager 環境變數
description: 標準環境變數可以透過 Cloud Manager 進行設定和管理，並提供給執行階段環境，用於 OSGi 設定。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 76%

---


# Cloud Manager 環境變數 {#environment-variables}

可以透過 Cloud Manager 設定和管理標準環境變數。它們提供給執行階段環境並且可以在 OSGi 設定中使用。環境變數可以是特定環境的值或環境密碼，具體取決於變更的內容。

## 概觀 {#overview}

環境變數為 AEM as a Cloud Service 的使用者提供了許多好處：

* 環境變數可讓您的程式碼和應用程式的行為根據內容和環境而變化。例如，與生產或中繼環境相比，環境變數可用於在開發環境中啟用不同的設定，以避免代價高昂的錯誤。
* 環境變數只需要設定一次，並且可以在必要時更新和刪除。
* 環境變數的值可以隨時更新並立即生效，無需任何程式碼變更或部署。
* 環境變數可以將程式碼與設定分開，也無須在版本控制中包含敏感資訊。
* 環境變數提高了 AEM as a Cloud Service 應用程式的安全性，因為它們位於程式碼之外。

使用環境變數的典型使用案例包括：

* 連接您的 AEM 應用程式與不同的外部端點
* 在儲存密碼時使用參考而不是直接在程式碼庫中儲存
* 當一個計畫中存在多個開發環境，且環境間的部分設定不同時

## 新增環境變數 {#add-variables}

>[!NOTE]
>
>您必須是 [**Deployment Manager** 角色](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)的成員才能新增或修改環境變數。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要管理的程式。
1. 從側邊導覽列中選取所選程式的&#x200B;**環境**&#x200B;視窗，然後選取您要建立環境變數的環境。
1. 在環境的詳細資訊中，選擇&#x200B;**設定**&#x200B;索引標籤，然後選擇&#x200B;**新增**&#x200B;以打開&#x200B;**環境設定**&#x200B;對話框。
   * 如果您是第一次新增環境變數，可以在頁面中央看到&#x200B;**新增組態**&#x200B;按鈕。 您可以使用此按鈕或&#x200B;**新增**&#x200B;來打開&#x200B;**環境設定**&#x200B;對話框。

   ![設定索引標籤](assets/configuration-tab.png)

1. 輸入變數詳細資訊。
   * **名稱**
   * **值**
   * **已套用服務** — 定義變數適用於哪個服務(作者/Publish/預覽)，或適用於所有服務
   * **類型** - 定義變數是普通變數還是密碼

   ![新增變數](assets/add-variable.png)

1. 輸入新變數後，您必須在包含新變數之列的最後一欄中選擇&#x200B;**新增**。
   * 您可以透過輸入新行並選擇&#x200B;**新增**&#x200B;來一次輸入多個變數。

   ![儲存變數](assets/save-variables.png)

1. 選取「**儲存**」以儲存變數。

具有&#x200B;**更新**&#x200B;狀態的指示器會顯示在表格頂端和新增的變數旁邊，表示正在使用設定更新環境。完成後，新的環境變數會顯示在表格中。

![更新變數](assets/updating-variables.png)

>[!TIP]
>
>如果要新增多個變數，建議新增第一個變數，然後使用&#x200B;**環境設定**&#x200B;對話方塊中的&#x200B;**新增**&#x200B;按鈕來新增其他變數。 這樣，只要更新環境一次即可新增這些變數。

## 更新環境變數 {#update-variables}

建立環境變數後，您可以使用&#x200B;**新增/更新**&#x200B;按鈕以啟動&#x200B;**環境設定**&#x200B;對話框來更新變數。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。
1. Cloud Manager 列出可用的各種方案。選取您要管理的專案。
1. 在導覽面板中，選取所選程式的&#x200B;**環境**&#x200B;視窗，然後選取您要修改環境變數的環境。
1. 在環境的詳細資訊中，選擇&#x200B;**設定**&#x200B;索引標籤，然後在右上角選擇&#x200B;**新增更新**&#x200B;以打開&#x200B;**環境設定**&#x200B;對話框。
1. 使用您要修改之變數列最後一欄中的省略符號按鈕，選取&#x200B;**編輯**&#x200B;或&#x200B;**刪除**。

   ![編輯或刪除變數](assets/edit-delete-variable.png)

1. 根據需要編輯環境變數。
   * 編輯時，省略符號按鈕將變更為選項以恢復原始值或確認您的變更。
   * 編輯密碼時，只能更新值，不能查看。

   ![編輯變數](assets/edit-variable.png)

1. 完成必要的組態變更後，請選取&#x200B;**儲存**。

[新增變數時](#add-variables)，具有&#x200B;**更新**&#x200B;狀態的指示器會顯示在表格頂端和更新的變數旁邊，表示正在使用設定更新環境。完成後，更新的環境變數會顯示在表格中。

>[!TIP]
>
>如果要更新多個變數，建議使用&#x200B;**環境設定**&#x200B;對話方塊，在點選或按一下&#x200B;**儲存**&#x200B;之前一次更新所有必要的變數。 這樣，只要更新環境一次即可新增這些變數。

## 使用環境變數 {#using}

環境變數可讓您的 `pom.xml` 設定更加安全和靈活。例如，密碼不需要硬式編碼，您的設定可以根據環境變數中的值進行調整。

您可以透過 XML 存取環境變數和密碼，如下所示。

* `${env.VARIABLE_NAME}`

如需有關如何在 `pom.xml` 檔案中使用這兩種類型變數的範例，請參見文件：[設定專案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)。

如需詳細資訊，請參閱[正式 Maven 文件](https://maven.apache.org/settings.html#quick-overview)。

## 環境變數可用性 {#availability}

環境變數可以用在幾個地方。

### 編寫、預覽和發佈 {#author-preview-publish}

一般環境變數和密碼均可用於編寫、預覽和發佈環境。

### Dispatcher {#dispatcher}

只有一般環境變數可搭配[使用Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)密碼無法使用。

但是環境變數不能在 `IfDefine` 指令中使用。

>[!TIP]
>
>在部署之前，您應該透過 [本機 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) 驗證您對環境變數的使用。

### OSGi 設定 {#osgi}

一般環境變數和密碼都可以在 [OSGi 設定](/help/implementing/deploying/configuring-osgi.md)中使用。

### 管道變數 {#pipeline}

除了環境變數，還有管道變數會在建置階段顯示。深入瞭解[組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)下的管道變數。
