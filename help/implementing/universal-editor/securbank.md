---
title: 通用編輯器的SecurBank範例應用程式
description: 透過使用SecurBank應用程式來瞭解具有實作體驗的通用編輯器，該應用程式旨在展示Universal Editor加速內容建立的強大功能、靈活性和可用性。
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---

# 通用編輯器的SecurBank範例應用程式 {#securbank}

透過使用SecurBank應用程式來瞭解具有實作體驗的通用編輯器，該應用程式旨在展示Universal Editor加速內容建立的強大功能、靈活性和可用性。

## 先決條件 {#prerequisites}

* 您必須指派給&#x200B;**AEM系統管理員** [產品設定檔](/help/journey-onboarding/assign-profiles-aem.md)，才能安裝SecurBank應用程式。
* 您必須安裝[Node.js](https://nodejs.org)版本20或更新版本，才能進行本機開發。

## 安裝SecurBank {#installation}

SecurBank應用程式的安裝很簡單，但由於涉及AEM as a Cloud Service的許多領域，因此需要執行許多步驟。 以下是主要步驟的概觀。

1. [在Cloud Manager中建立沙箱計畫](#create-sandbox-program)。
1. [復製程式的Git存放庫並更新為SecurBank AEM專案內容](#clone-and-update)。
1. [執行管道以部署SecurBank AEM專案](#run-pipeline)。
1. [擷取Cloud Manager認證以進行本機Web應用程式開發](#retrieve-credentials)。
1. [下載並設定SecurBank網頁應用程式](#download-web-app)。
1. [執行SecurBank網頁應用程式](#run-web-app)。

以下小節詳細說明所需的個別工作。

### 在Cloud Manager中建立沙箱計畫。 {#create-sandbox-program}

您需要新的Cloud Manager程式，才能安裝SecurBank。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織。

1. 為SecurBank應用程式建立新的沙箱計畫。

   * 選取&#x200B;**解決方案和附加元件**&#x200B;時使用預設選項。
   * 如需有關如何建立沙箱計畫的詳細資訊，請參閱檔案[建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。

### 複製計畫的Git存放庫並更新SecurBank AEM專案內容。 {#clone-and-update}

1. 建立程式後，請開啟該程式，並在&#x200B;**存放庫**&#x200B;索引標籤上，點選或按一下&#x200B;**存取存放庫資訊**&#x200B;按鈕，以開啟&#x200B;**存放庫資訊**&#x200B;對話方塊，並檢視存取沙箱環境的Git存放庫所需的認證。

   * 如需有關如何存取存放庫資訊的詳細資訊，請參閱檔案[存取存放庫](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

1. 使用&#x200B;**存放庫資訊**&#x200B;對話方塊中的認證，在本機電腦上複製存放庫。

1. 找出本機複製的資料夾，將其開啟並刪除隱藏/點檔案以外的所有內容。

1. 按一下&#x200B;**代碼**，然後在下拉式清單中按一下&#x200B;**下載ZIP**，以從[`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank)的GitHub擷取最新的SecurBank AEM專案代碼。

1. 將您本機檔案系統上的zip檔案內容解壓縮，並將其移至沙箱程式本機複製的現成空白資料夾。

1. 使用終端機，切換到複製專案的資料夾並提交所有內容並將其推送到Git。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### 執行管道以部署SecurBank AEM專案。 {#run-pipeline}

SecurBank的AEM專案已送交沙箱存放庫後，便可隨管道部署。

1. 返回Cloud Manager中沙箱程式的&#x200B;**總覽**&#x200B;標籤，並執行完整棧疊非生產管道。

   * 取消勾選管道執行的所有選項。
   * 如需有關執行管道的詳細資訊，請參閱檔案[管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)。

### 擷取Cloud Manager認證，用於本機Web應用程式開發。 {#retrieve-credentials}

在執行SecurBank應用程式之前，您需要先取得Cloud Manager憑證，才能將應用程式連線至Cloud Manager。

1. 管道執行時，請返回Cloud Manager中的&#x200B;**總覽**&#x200B;標籤，然後點選或按一下環境名稱旁的省略符號按鈕，並選取&#x200B;**Developer Console**。

1. 在Developer Console中，選取「**整合**」標籤，然後選取「**本機權杖**」標籤，然後點選或按一下「**取得本機開發權杖**」。

1. 使用存取權杖產生JSON檔案。 僅將權杖本身（剩餘的JSON不需要複製）複製到安全位置，以便在關閉Developer Console並返回Cloud Manager之前的未來步驟中使用。

1. 返回Cloud Manager，在&#x200B;**總覽**&#x200B;標籤上，以滑鼠右鍵按一下環境的URL以複製並將其儲存在安全位置，以供日後步驟使用。

### 下載及設定SecurBank網頁應用程式。 {#download-web-app}

現在您可以下載並設定SecurBank網頁應用程式。

1. 按一下&#x200B;**代碼**，然後在下拉式清單中按一下&#x200B;**下載ZIP**，從GitHub [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events)擷取最新的SecurBank應用程式代碼。

1. 解壓縮本機檔案系統上的zip檔案內容。

1. 啟動您偏好的程式碼編輯器，並在`summit-2024-l425-ue-z-final-with-events/react-app/.env`的SecurBank應用程式專案中開啟隱藏的環境檔案。

1. 對`.env`檔案進行下列變更並儲存變更。

   * 針對`REACT_APP_HOST_URI`，貼上您環境先前複製的URL值。
   * 針對`REACT_APP_DEV_TOKEN`，貼上先前複製的本機開發權杖的值。

### 執行SecurBank網頁應用程式。 {#run-web-app}

在Cloud Manager和本機中設定所有專案，您就能執行SecurBank網頁應用程式。

1. 在本機電腦的命令列上，導覽至您下載並解壓縮之SecurBank應用程式專案的`react-app`資料夾。

1. 在您的`react-app`資料夾中使用`node -i`命令安裝SecurBank應用程式。

1. 安裝後，使用`npm start`命令啟動SecurBank應用程式。

1. 如果安裝及啟動成功，您將會看到：

* 終端機中的下列輸出。

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * 而且瀏覽器視窗會開啟至URL `https://localhost:3000`。

      * 請注意，這是為了開發目的，因此不提供有效的憑證。 因此，您可能需要通知瀏覽器，允許其存取頁面。

恭喜！您現在應該會看到SecurBank應用程式在瀏覽器中成功執行。

如果內容尚未顯示，請確定您執行的&#x200B;**部署至開發**&#x200B;管道已成功完成。

瀏覽器中的![SecurBank應用程式](assets/securbank.png)
