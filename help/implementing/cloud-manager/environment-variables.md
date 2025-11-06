---
title: Cloud Manager中的環境變數
description: 標準環境變數可透過Cloud Manager進行設定和管理，並提供給執行階段環境，用於OSGi設定。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 29%

---


# Cloud Manager中的環境變數 {#environment-variables}

可以透過 Cloud Manager 設定和管理標準環境變數。它們提供給執行階段環境並且可以在OSGi設定中使用。

環境變數可以是特定環境的值或環境密碼，具體取決於變更的內容。

## 關於環境變數 {#overview}

環境變數為AEM as a Cloud Service的使用者提供了許多好處，如下所示：

* 環境變數可讓您的程式碼和應用計劃的行為根據內容和環境而變化。例如，與生產或預備環境相比，環境變數可用於在開發環境中啟用不同的設定，以避免代價高昂的錯誤。
* 環境變數只需要設定一次，並且可以在必要時更新和刪除。
* 環境變數的值可以隨時更新並立即生效，無需任何程式碼變更或部署。
* 環境變數可以將程式碼與設定分開，也無須在版本控制中包含敏感資訊。
* 環境變數提高了 AEM as a Cloud Service 應用計劃的安全性，因為它們位於程式碼之外。

使用環境變數的典型使用案例包括：

* 連接您的 AEM 應用程式與不同的外部端點
* 在儲存密碼時使用參考而不是直接在程式碼庫中儲存
* 當一個計畫中存在多個開發環境，且環境間的部分設定不同時

## 新增環境變數 {#add-variables}

若要新增多個變數，Adobe建議您新增第一個變數，然後在![環境設定](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)對話方塊中使用&#x200B;**新增圖示** **新增**&#x200B;來新增其他變數。 此方法表示只要更新一次環境，即可新增這些變數。

若要新增、更新或刪除環境變數，您必須是&#x200B;[**部署管理員**&#x200B;角色](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)的成員。

**若要新增環境變數：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要管理的程式。
1. 從側邊功能表，按一下&#x200B;**環境**。
1. 在&#x200B;**環境**&#x200B;頁面上，選取包含您想要新增環境變數之環境的表格列。
1. 在環境的詳細資訊頁面上，按一下「**設定**」標籤。
1. 按一下![新增/更新 — 新增圓形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **新增/更新**。
如果您是第一次新增環境變數，請按一下頁面中央的[新增組態] **&#x200B;**。

   ![設定索引標籤](assets/configuration-tab.png)

1. 在&#x200B;**環境組態**&#x200B;對話方塊中，在表格的第一列輸入詳細資料。

   | 欄位 | 說明 |
   | --- | --- |
   | 名稱 | 設定變數的唯一名稱。 它會識別環境中使用的特定變數。 它必須遵循以下命名慣例：<ul><li>變數只能包含英數字元和底線(`_`)。</li><li>每個環境有200個變數的限制。</li><li>每個名稱不得超過100個字元。</li></ul> |
   | 值 | 變數儲存的值。 |
   | 套用的步驟 | 選取要套用變數的服務。 選取&#x200B;**全部**&#x200B;以將變數套用至所有服務。<ul><li>**全部**</li><li>**製作者**</li><li>**發佈**</li><li>**預覽**</li></ul> |
   | 類型 | 選取變數是普通或秘密。 |

   ![新增變數](assets/add-variable.png)

1. 按一下「![新增」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)**新增**。

   視需要新增其他變數。

1. 按一下&#x200B;**儲存**。

   狀態為&#x200B;**正在更新**&#x200B;的進度環會顯示在表格的右上角。 任何新新增的變數左側也會出現旋轉圖示。 這些狀態表示正在使用設定更新環境。 完成後，新的環境變數會顯示在表格中。

![更新變數](assets/updating-variables.png)

## 更新環境變數 {#update-variables}

建立環境變數後，您可以使用![新增/更新 — 新增圓形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **新增/更新**&#x200B;來更新變數，以開啟&#x200B;**環境設定**&#x200B;對話方塊。

如果您想要更新多個變數，Adobe建議您使用&#x200B;**環境設定**&#x200B;對話方塊，在按一下&#x200B;**儲存**&#x200B;之前，一次更新所有必要的變數。 這樣，只要更新環境一次即可新增這些變數。

**若要更新環境變數：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要管理的程式。
1. 從側邊功能表，按一下&#x200B;**環境**。
1. 在&#x200B;**環境**&#x200B;頁面上，選取有您要更新變數之環境的資料表列。
1. 在環境的詳細資訊頁面上，按一下「**設定**」標籤。
1. 按一下![新增/更新 — 新增圓形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **新增/更新**。
1. 在&#x200B;**環境組態**&#x200B;對話方塊中，在您要變更之變數列的最後一欄按一下![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 在下拉式功能表中，按一下&#x200B;**編輯**。

   ![編輯或刪除變數](assets/edit-delete-variable.png)

1. 視需要更新環境變數的值。
編輯密碼時，只能更新值，不能檢視。

   ![編輯變數](assets/edit-variable.png)

1. 執行下列任一項作業：

   * 按一下![套用 — 勾選圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)以套用變更。
   * 按一下![復原圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg)以復原變更。

1. 按一下&#x200B;**儲存**。

   狀態為&#x200B;**正在更新**&#x200B;的進度環會顯示在表格的右上角。 旋轉圖也會出現在任何已更新變數的左側。 這些狀態表示正在使用設定更新環境。 完成後，更新的環境變數會顯示在表格中。

## 刪除環境變數 {#delete-env-variable}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要管理的程式。
1. 從側邊功能表，按一下&#x200B;**環境**。
1. 在&#x200B;**環境**&#x200B;頁面上，選取有您要更新變數之環境的資料表列。
1. 在環境的詳細資訊頁面上，按一下「**設定**」標籤。
1. 按一下![新增/更新 — 新增圓形圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **新增/更新**。
1. 在&#x200B;**環境組態**&#x200B;對話方塊中，在您要變更之變數列的最後一欄按一下![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 在下拉式功能表中，按一下&#x200B;**刪除**&#x200B;以立即移除變數。
1. 按一下&#x200B;**儲存**。

## 使用環境變數 {#using}

環境變數可讓您的 `pom.xml` 設定更加安全和靈活。例如，密碼不需要硬式編碼，您的設定可以根據環境變數中的值進行調整。

您可以透過XML存取環境變數和秘密，如下所示：

`${env.VARIABLE_NAME}`

請參閱[設定專案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)，以取得如何在`pom.xml`檔案中使用這兩種型別變數的範例。

如需詳細資訊，另請參閱[正式Maven檔案](https://maven.apache.org/settings.html#quick-overview)。

## 環境變數的可用性 {#availability}

環境變數可以用在幾個地方，如下所示：

| 可在其中使用環境變數的位置 | 說明 |
| --- | --- |
| 編寫、預覽和發佈 | 一般環境變數和密碼均可用於編寫、預覽和發佈環境。 |
| Dispatcher | 只有一般環境變數可搭配[Dispatcher](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)使用。<ul><li>不能使用密碼。</li><li>環境變數不能在`IfDefine`指令中使用。</li><li>在部署之前，請透過[本機使用 Dispatcher](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools) 驗證您所使用的環境變數。</li></ul> |
| OSGi 設定 | 一般環境變數和秘密都可以在[OSGi設定](/help/implementing/deploying/configuring-osgi.md)中使用。 |
| 管道變數 | 除了環境變數，還有管道變數會在建置階段顯示。深入瞭解[組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)中的管道變數。 |

