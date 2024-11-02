---
title: 在 Cloud Manager 中新增外部存放庫 (早期採用者)
description: 了解如何將外部存放庫新增至 Cloud Manager。Cloud Manager 支援與 GitHub、GitLab 和 Bitbucket 存放庫整合。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6c7f2e2d18e8adf7c85d963f4cd1f81000aa8332
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 94%

---


# 在 Cloud Manager 中新增外部存放庫 {#external-repositories}

了解如何將外部存放庫新增至 Cloud Manager。Cloud Manager 支援與 GitHub、GitLab 和 Bitbucket 存放庫整合。

>[!NOTE]
>
>此功能僅適用於[早期採用方案](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)。

## 設定外部存放庫

在 Cloud Manager 中設定存放庫包含三個步驟：

1. [新增外部存放庫](#add-external-repo)至所選方案。
1. 為外部存放庫提供存取權杖。
1. 驗證私人GitHub存放庫的所有權。


## 新增外部存放庫 {#add-ext-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取要連結外部存放庫的程式。

1. 在側邊選單中，在&#x200B;**服務**&#x200B;下，選取![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)**存放庫**。

   ![儲存庫頁面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在右上角附近的&#x200B;**存放庫**&#x200B;頁面，按一下&#x200B;**新增存放庫**。

1. 在&#x200B;**新增存放庫**&#x200B;對話框中，選取&#x200B;**私人存放庫**，將外部 Git 存放庫連結至您的方案。

   ![新增自己的存放庫](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每個對應欄位中，提供關於存放庫的下列詳細資料：

   | 欄位 | 說明 |
   | --- | --- |
   | **存放庫名稱** | 必要。您的新存放庫的生動名稱。 |
   | **存放庫 URL** | 必要。存放庫的 URL。<br><br> 如果您使用 GitHub 託管的存放庫，則路徑為以 `.git` 結尾。<br>例如，*`https://github.com/org-name/repo-name.git`*(URL 路徑僅用於插圖目的)。<br><br>如果您正在使用外部存放庫，則必須遵循下列 URL 路徑格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> 或<br>`https://self-hosted-domain/org-name/repo-name.git`<br>，與您的 Git 廠商相符。 |
   | S **選取存放庫型別** | 必要。選取您所使用的存放庫類型：**GitHub**、**GitLab** 或 **BitBucket**。若上述存放庫 URL 路徑包含 Git 廠商名稱，例如 GitLab 或 Bitbucket，則系統已為您預先選擇存放庫類型。 |
   | **說明** | 選擇性。存放庫的詳細描述。 |

1. 選取&#x200B;**儲存**&#x200B;以新增存放庫。

1. 在&#x200B;**私人存放庫擁有權驗證**&#x200B;對話框中，提供存取權杖以驗證外部存放庫的擁有權，讓您可以進行存取。

   ![為存放庫選取現有的存取權杖](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *為 BitBucket 存放庫選取現有的存取權杖。*

   | 權杖類型 | 說明 |
   | --- | --- |
   | **使用現有的存取權杖** | 如果您已為組織提供存放庫存取權杖，且有權存取多個存放庫，您可以選取現有的權杖。使用&#x200B;**權杖名稱**&#x200B;下拉清單，選取想要套用至存放庫的權杖。否則，請新增新的存取權杖。 |
   | **新增新的存取權杖** | **存放庫類型：GitHub**<br>• 在&#x200B;**權杖名稱**&#x200B;文字欄位，輸入您建立的存取權杖名稱。<br>• 依照 [GitHub 文件](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的指示，建立個人存取權杖。<br>• 需要權限：<br>  • `Read access to metadata`。<br>  • `Read and write access to code and pull requests`。<br>• 在&#x200B;**存取權杖**&#x200B;欄位，貼上您所建立的權杖。 |
   |  | **存放庫類型：GitLab**<br>• 在&#x200B;**權杖名稱**&#x200B;文字欄位，輸入您建立的存取權杖名稱。<br>• 依照 [GitLab 文件](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)中的指示，建立個人存取權杖。<br>• 需要權限：<br>  • `api`<br>  • `read_api`<br>  • `read_repository`<br>  • `write_repository`<br>• 在&#x200B;**存取權杖**&#x200B;欄位，貼上您所建立的權杖。 |
   |  | **存放庫類型：Bitbucket**<br>• 在&#x200B;**權杖名稱**&#x200B;文字欄位，輸入您建立的存取權杖名稱。<br>• 使用 [Bitbucket 文件](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)建立存放庫存取權杖。<br>• 需要權限：<br>  • `Read and write access to code and pull requests`。 |

   >[!NOTE]
   >
   >**新增新的存取權杖**&#x200B;功能目前在「早期採用者」階段。其他的功能正在規劃中。因此，存取權杖所需的權限可能會變更。另外，用於管理權杖的使用者介面可能會更新，可能包括權杖過期日期等功能。並且，自動檢查以確保連結至存放庫的權杖保持有效。

1. 按一下「**驗證**」。

驗證之後，外部存放庫即可使用並連結至管道。

## 將驗證的外部存放庫連結至管道。 {#validate-ext-repo}

1. 新增或編輯管道：
   * [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [編輯管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![管道的來源代碼存放庫和 Git 分支](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *新增非生產管道對話框，其中包含選取的存放庫和 Git 分支，*

1. 新增或編輯管道時，若要指定新管道或現有管道的&#x200B;**來源代碼**&#x200B;位置，請從&#x200B;**存放庫**&#x200B;下拉清單中選取要使用的外部存放庫。

1. 在 **Git 分支**&#x200B;下拉清單中，選取分支作為管道的來源。

1. 按一下「**儲存**」。


>[!TIP]
>
>如需關於在 Cloud Manager 管理存放庫的詳細資訊，請參閱「[Cloud Manager 存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)」。


## 限制

* 外部存放庫無法連結到設定管道。
* 使用外部存放庫 (不包括 GitHub 託管存放庫) 和&#x200B;**部署觸發程序**&#x200B;選項「[!UICONTROL **在 Git 變更時**]」，觸發程序不會自動啟動。它們必須手動啟動。
