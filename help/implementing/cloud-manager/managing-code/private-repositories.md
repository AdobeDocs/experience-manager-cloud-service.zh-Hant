---
title: 在Cloud Manager中新增私人GitHub存放庫
description: 了解如何設定 Cloud Manager 與您自己的私人 GitHub 存放庫搭配使用。
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5e9b29a8108d5c012d402fda8ff7544e02ca911
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 33%

---

# 在Cloud Manager中新增私人GitHub存放庫 {#private-repositories}

透過設定Cloud Manager以與您的私人GitHub存放庫整合，您可以直接在GitHub中使用Cloud Manager驗證您的程式碼。 此設定免除了定期將程式碼與Adobe存放庫同步的需求。

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager. -->

>[!NOTE]
>
>這是公開 GitHub 的專屬功能。不支援自行託管的 GitHub。

## 設定 {#configuration}

在Cloud Manager中設定私人GitHub存放庫包含兩個步驟：

1. [將私人GitHub存放庫](#add-repo)新增至選取的方案。
1. 然後，[驗證私人GitHub存放庫的所有權](#validate-ownership)。

### 將私人GitHub存放庫新增到計畫 {#add-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要連結私人Git存放庫的程式。

1. 在側邊功能表的&#x200B;**服務**&#x200B;下方，選取![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存放庫**。

   ![存放庫頁面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存放庫**&#x200B;頁面的右上角附近，按一下&#x200B;**新增存放庫**。

1. 在「**新增存放庫**」對話框內，選取「**私人存放庫**」作為存放庫類型。

   ![新增自己的存放庫](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 在每個欄位中，提供關於存放庫的下列詳細資訊：

   | 欄位 | 說明 |
   | --- | --- |
   | 存放庫名稱 | 您新存放庫的表現式名稱。 |
   | 存放庫 URL | 私人存放庫的URL，必須以`.git`結尾。<br>例如，*`https://github.com/org-name/repo-name.git`* （URL路徑僅供插圖之用）。 |
   | 說明 (選填) | 存放庫的詳細說明。 |

1. 選取&#x200B;**儲存**。
現在您可以[驗證私人存放庫的所有權](#validate-ownership)。

>[!TIP]
>
>如需關於在 Cloud Manager 管理存放庫的詳細資訊，請參閱「[Cloud Manager 存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)」。



### 驗證私人GitHub存放庫的所有權 {#validate-ownership}

Cloud Manager 現在知道您的 GitHub 存放庫，但仍然需要存取它。若要授予存取權，您需要安裝 Adobe GitHub 應用程式並驗證您擁有指定的存放庫。

**若要驗證私人GitHub存放庫的所有權：**

1. 新增您自己的存放庫後，請依照&#x200B;**私人存放庫所有權驗證**&#x200B;對話方塊中的剩餘步驟操作。

   ![私人存放庫所有權驗證](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | 說明 |
   | --- | --- |
   | **步驟1： GitHub應用程式** | Cloud Manager會使用GitHub應用程式，安全地與您的私人存放庫互動。<br>·您GitHub組織的所有者必須安裝位於`https://github.com/apps/cloud-manager-for-aem`的應用程式並授與存放庫的存取權。<br>·如需安裝和授與存取權完成的詳細資訊，請參閱GitHub的檔案。 |
   | **步驟2：機密檔案** | 若要增強安全性，您必須在存放庫的預設分支中建立機密檔案。<br>·按一下&#x200B;**產生**，然後按一下&#x200B;**確認**。 Cloud Manager會在&#x200B;**機密檔案內容**&#x200B;文字欄位中產生私人檔案的內容。<br>·按一下![復製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以複製該欄位中的內容。 密碼檔案的內容只會顯示一次。如果您在關閉此對話方塊之前未複製內容，請重新產生密碼。 |

1. 在GitHub存放庫的預設分支中建立名為的新檔案：

   `.well-known/adobe/cloud-manager-challenge`

1. 將機密檔案內容貼到您剛建立的新檔案中並儲存。

   安裝應用程式且存放庫中存在機密檔案後，請繼續此步驟。

1. 在&#x200B;**私人存放庫所有權驗證**&#x200B;對話方塊中，按一下&#x200B;**驗證**。

您可以安裝應用程式，並依任何順序建立機密檔案。 不過，必須先完成這兩個步驟才能進行驗證。

在驗證之前，存放庫會以紅色圖示列出，表示其尚未驗證且不能使用。

![未經驗證的存放庫](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

**存放庫**&#x200B;頁面上資料表中的&#x200B;**Type**&#x200B;資料行會識別Adobe提供的存放庫(**Adobe**)與您自己的私人存放庫(**GitHub**)。

如果您稍後需要返回存放庫以完成驗證，請在&#x200B;**存放庫**&#x200B;頁面上，按一下代表您剛剛新增的GitHub存放庫之列中的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。 在下拉式清單中，選取&#x200B;**所有權驗證**。



## 搭配Cloud Manager使用私人GitHub存放庫 {#using}

在Cloud Manager中驗證GitHub存放庫後，整合即完成。 您可以搭配Cloud Manager使用存放庫。

**搭配Cloud Manager使用私人存放庫：**

1. 當您建立提取請求時，會自動啟動 GitHub 檢查。

   ![GitHub 檢查](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. 對於每個提取請求，皆會自動建立[全端程式碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。此管道會在每次提取請求更新時啟動。

1. GitHub檢查會維持在執行狀態，直到程式碼品質檢查完成為止。 程式碼品質結果隨後會傳播至 GitHub 檢查。

   ![GitHub 程式碼品質檢查](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

當提取請求被合併或關閉時，建立的完整棧疊計畫碼品質管道會自動刪除。

>[!TIP]
>
>有關執行提取要求檢查時透過GitHub提供的詳細資訊，請參閱[GitHub檢查註解](github-annotations.md)。

>[!TIP]
>
>您可以控制自動建立的管道以驗證對私人存放庫的每個提取請求。請參閱[私人存放庫的 GitHub 檢查設定](github-check-config.md)，了解更多資訊。



## 將私人存放庫與管道建立關聯 {#pipelines}

已驗證的私人存放庫可以與[完整棧疊和前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)相關聯。



## 限制 {#limitations}

將私人存放庫與 Cloud Manager 搭配使用時會有某些限制。

* 私人存放庫不支援 Web 層和設定管道。
* 在生產全端管道上使用私人存放庫時，不會建立和推送 Git 標記。
* 如果AdobeGitHub應用程式從您的GitHub組織移除，其會移除所有存放庫的提取請求驗證功能。
* 當新提交被推送到所選分支時，使用私人存放庫和提交建置觸發器的管道不會自動啟動。
* [成品重複使用功能](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)不適用於私人存放庫。
* 您無法使用Cloud Manager的GitHub檢查來暫停提取請求驗證。
如果已在Cloud Manager中驗證GitHub存放庫，Cloud Manager會一律嘗試驗證為該存放庫建立的提取請求。
