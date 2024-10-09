---
title: 在Cloud Manager中新增外部存放庫（早期採用者）
description: 瞭解如何將外部存放庫新增到Cloud Manager。 Cloud Manager支援與GitHub、GitLab和Bitbucket存放庫整合。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 4%

---


# 在Cloud Manager中新增外部存放庫 {#external-repositories}

瞭解如何將外部存放庫新增到Cloud Manager。 Cloud Manager支援與GitHub、GitLab和Bitbucket存放庫整合。

>[!NOTE]
>
>此功能僅適用於[早期採用方案](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)。

## 設定外部存放庫

在Cloud Manager中設定外部存放庫包含三個步驟：

1. [新增外部存放庫](#add-external-repo)至選取的方案。
1. 提供外部存放庫的存取權杖。
1. 驗證私人GitHub存放庫的所有權。


## 新增外部存放庫 {#add-ext-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取要連結外部存放庫的程式。

1. 在側邊功能表的&#x200B;**服務**&#x200B;下方，選取![資料夾圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存放庫**。

   ![存放庫頁面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存放庫**&#x200B;頁面的右上角附近，按一下&#x200B;**新增存放庫**。

1. 在&#x200B;**新增存放庫**&#x200B;對話方塊中，選取&#x200B;**私人存放庫**&#x200B;以將外部Git存放庫連結到您的程式。

   ![新增自己的存放庫](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每個欄位中，提供關於存放庫的下列詳細資訊：

   | 欄位 | 說明 |
   | --- | --- |
   | **存放庫名稱** | 必填。 您新存放庫的表現式名稱。 |
   | **存放庫URL** | 必填。 存放庫的URL。<br><br>如果您使用GitHub託管的存放庫，路徑必須在`.git`結尾。<br>例如，*`https://github.com/org-name/repo-name.git`* （URL路徑僅供插圖之用）。<br><br>如果您使用外部存放庫，則必須使用下列URL路徑格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br>或<br>`https://self-hosted-domain/org-name/repo-name.git`<br>並符合您的Git廠商。 |
   | S **選取存放庫型別** | 必填。 選取您正在使用的存放庫型別： **GitHub**、**GitLab**&#x200B;或&#x200B;**BitBucket**。 如果上述存放庫URL路徑包含Git供應商名稱（例如GitLab或Bitbucket），系統就會預先為您選取存放庫型別。 |
   | **說明** | 選填。 存放庫的詳細說明。 |

1. 選取&#x200B;**儲存**&#x200B;以新增存放庫。

1. 在&#x200B;**私人存放庫所有權驗證**&#x200B;對話方塊中，提供存取權杖以驗證外部存放庫的所有權，以便您可以存取它。

   ![選取存放庫的現有存取權杖](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *選取BitBucket儲存庫的現有存取權杖。*

   | 權杖型別 | 說明 |
   | --- | --- |
   | **使用現有的存取權杖** | 如果您已為貴組織提供存放庫存取權杖，並擁有多個存放庫的存取權，則可選取現有權杖。 使用&#x200B;**Token Name**&#x200B;下拉式清單，選擇要套用至存放庫的權杖。 否則，請新增存取權杖。 |
   | **新增存取權杖** | **存放庫型別： GitHub**<br>·在&#x200B;**Token名稱**&#x200B;文字欄位中，輸入您正在建立的存取權杖名稱。<br>·依照[GitHub檔案](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的指示建立個人存取權杖。<br>·需要的許可權：<br>  · `Read access to metadata`。<br>  · `Read and write access to code and pull requests`。<br>·在&#x200B;**存取權杖**&#x200B;欄位中，貼上您剛才建立的權杖。 |
   |  | **存放庫型別： GitLab**<br>·在&#x200B;**Token Name**&#x200B;文字欄位中，輸入您正在建立的存取權杖名稱。<br>·依照[GitLab檔案](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)中的指示建立個人存取權杖。<br>·需要的許可權：<br>  · `api`<br>  · `read_api`<br>  · `read_repository`<br>  · `write_repository`<br>·在&#x200B;**存取權杖**&#x200B;欄位中，貼上您剛才建立的權杖。 |
   |  | **儲存庫型別： Bitbucket**<br>·在&#x200B;**權杖名稱**&#x200B;文字欄位中，輸入您正在建立的存取權杖名稱。<br>·使用[Bitbucket檔案](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)建立存放庫存取權杖。<br>·需要的許可權：<br>  · `Read and write access to code and pull requests`。 |

   >[!NOTE]
   >
   >功能&#x200B;**新增存取權杖**&#x200B;目前處於早期採用者階段。 正在規劃其他功能。 因此，存取權杖的必要許可權可能會變更。 此外，管理權杖的使用者介面可能會更新，其中可能包括權杖到期日等功能。 以及自動化檢查，以確保連結至存放庫的Token保持有效。

1. 按一下&#x200B;**驗證**。

驗證後，外部存放庫已準備好使用並連結到管道。

## 將已驗證的外部存放庫連結至管道 {#validate-ext-repo}

1. 新增或編輯管道：
   * [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [編輯管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![管道的原始程式碼存放庫和Git分支](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *新增非生產管道對話方塊，其中包含選取的存放庫和Git分支，*

1. 新增或編輯管道時，若要為您新管道或現有管道指定&#x200B;**Source程式碼**&#x200B;位置，請從&#x200B;**存放庫**&#x200B;下拉式清單中選擇您想要使用的外部存放庫。

1. 在&#x200B;**Git分支**&#x200B;下拉式清單中，選取分支作為管道的來源。

1. 按一下「**儲存**」。


>[!TIP]
>
>如需關於在 Cloud Manager 管理存放庫的詳細資訊，請參閱「[Cloud Manager 存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)」。


## 限制

* 外部存放庫無法連結到設定管道。
* 使用外部存放庫的管道（不包括GitHub託管的存放庫）和&#x200B;**部署觸發程式**&#x200B;選項&#x200B;[!UICONTROL **在Git變更**]&#x200B;上，觸發程式不會自動啟動。 必須手動啟動。




