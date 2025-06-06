---
title: 在Cloud Manager中新增外部存放庫
description: 了解如何將外部存放庫新增至 Cloud Manager。Cloud Manager支援與GitHub Enterprise、GitLab、Bitbucket和Azure DevOps存放庫整合。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期採用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: e881c3d8af7127e030aa9a0a2c163eaf04870c2b
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 25%

---

# 在 Cloud Manager 中新增外部存放庫 {#external-repositories}

了解如何將外部存放庫新增至 Cloud Manager。Cloud Manager支援與GitHub Enterprise、GitLab和Bitbucket存放庫整合。

客戶現在也可以將其Azure DevOps Git存放庫加入Cloud Manager，並支援現代Azure DevOps和舊版VSTS (Visual Studio Team Services)存放庫。

* Edge Delivery Services 使用者可以使用所加入的存放庫來同步處理及部署網站程式碼。
* AEM as a Cloud Service 和 Adobe Managed Services (AMS) 使用者可以將此存放庫連結至全堆疊以及前端管道。

>[!NOTE]
>
>本文所述功能僅可透過早期採用計畫使用。 如需詳細資訊，以及要註冊為早期採用者，請參閱[自備Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)。


## 設定外部存放庫

在Cloud Manager中設定外部存放庫包含下列步驟：

1. [新增外部存放庫](#add-external-repo)至所選方案。
1. 為外部存放庫提供存取權杖。
1. 驗證私人GitHub存放庫的所有權。
1. [將webhook](#configure-webhook)設定到外部存放庫。


## 新增外部存放庫 {#add-ext-repo}

>[!NOTE]
>
>外部存放庫無法連結到設定管道。

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取要連結外部存放庫的程式。

1. 在側邊功能表的&#x200B;**方案**&#x200B;下，按一下![資料夾大綱圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存放庫**。

   ![儲存庫頁面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在右上角附近的&#x200B;**存放庫**&#x200B;頁面，按一下&#x200B;**新增存放庫**。

1. 在&#x200B;**新增存放庫**&#x200B;對話框中，選取&#x200B;**私人存放庫**，將外部 Git 存放庫連結至您的方案。

   ![新增自己的存放庫](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每個對應欄位中，提供關於存放庫的下列詳細資料：

   | 欄位 | 說明 |
   | --- | --- |
   | **存放庫名稱** | 必要。您的新存放庫的生動名稱。 |
   | **存放庫 URL** | 必要。存放庫的 URL。<br><br>如果您使用GitHub託管的存放庫，路徑必須在`.git`結尾。<br>例如，*`https://github.com/org-name/repo-name.git`*(URL 路徑僅用於插圖目的)。<br><br>如果您正在使用外部存放庫，則必須遵循下列 URL 路徑格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> 或<br>`https://self-hosted-domain/org-name/repo-name.git`<br>，與您的 Git 廠商相符。 |
   | **選取存放庫類型** | 必要。選取您正在使用的存放庫型別。 如果存放庫URL路徑包含Git供應商名稱（例如GitLab或Bitbucket），系統已為您預先選取存放庫型別。：<ul><li>**GitHub** （GitHub Enterprise和自控版GitHub）</li><li>**GitLab** （包括`gitlab.com`和自控的GitLab版本） </li><li>**Bitbucket** （只有`bitbucket.org` — 雲端版本）受到支援。 自2024年2月15日起，已棄用自行託管的Bitbucket版本。)</li><li>**Azure DevOps** (`dev.azure.com`) </ul> |
   | **說明** | 選擇性。存放庫的詳細描述。 |

1. 選取&#x200B;**儲存**&#x200B;以新增存放庫。

1. 在&#x200B;**私人存放庫擁有權驗證**&#x200B;對話框中，提供存取權杖以驗證外部存放庫的擁有權，讓您可以進行存取。

   ![為存放庫選取現有的存取權杖](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *選取Bitbucket儲存庫的現有存取權杖。*

   | 權杖類型 | 說明 |
   | --- | --- |
   | **使用現有的存取權杖** | 如果您已為組織提供存放庫存取權杖，且有權存取多個存放庫，您可以選取現有的權杖。使用&#x200B;**權杖名稱**&#x200B;下拉清單，選取想要套用至存放庫的權杖。否則，請新增新的存取權杖。 |
   | **新增新的存取權杖** | **存放庫型別： GitHub Enterprise**<br><ul><li> 在&#x200B;**Token名稱**&#x200B;文字欄位中，輸入您要建立之存取權杖的名稱。<li>依照[GitHub檔案](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的指示建立個人存取權杖。<li>GitHub Enterprise Personal Access Token (PAT)的必要許可權<br>這些許可權確保Cloud Manager可以驗證提取請求、管理認可狀態檢查以及存取必要的存放庫詳細資訊。<br>當您在GitHub Enterprise中產生PAT時，請確定它包含下列存放庫許可權：<ul><li>提取請求（讀取和寫入）<li>認可狀態（讀取和寫入）<li>儲存區域中繼資料（唯讀）</li></li></ul></li></ul></ul></ul><ul><li>在&#x200B;**存取Token**&#x200B;欄位中，貼上您剛建立的權杖。 |
   | | **存放庫型別： GitLab**<ul><li>在&#x200B;**Token名稱**&#x200B;文字欄位中，輸入您要建立之存取權杖的名稱。<li>依照[GitLab檔案](https://docs.gitlab.com/user/profile/personal_access_tokens/)中的指示建立個人存取權杖。<li>GitLab個人存取權杖(PAT)的必要許可權<br>這些範圍允許Cloud Manager存取驗證和webhook整合所需的存放庫資料和使用者資訊。<br>當您在GitLab中產生PAT時，請確定它包含下列權杖範圍：<ul><li>api<li>read_user</li></li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**存取Token**&#x200B;欄位中，貼上您剛建立的權杖。 |
   | | **存放庫型別： Bitbucket**<ul><li>在&#x200B;**Token名稱**&#x200B;文字欄位中，輸入您要建立之存取權杖的名稱。<li>使用[Bitbucket檔案](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)建立存放庫存取權杖。<li>Bitbucket個人存取Token (PAT)的必要許可權<br>這些許可權可讓Cloud Manager存取存放庫內容、管理提取請求，以及設定或回應webhook事件。<br>當您在Bitbucket中建立應用程式密碼時，請確定它包含下列必要的應用程式密碼許可權：<ul><li>存放庫（唯讀）<li>提取請求（讀取和寫入）<li>Webhook （讀取和寫入）</li></li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**存取Token**&#x200B;欄位中，貼上您剛建立的權杖。 |
   | | **存放庫型別： Azure DevOps**<ul><li>在&#x200B;**Token名稱**&#x200B;文字欄位中，輸入您要建立之存取權杖的名稱。<li>使用[Azure DevOps檔案](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&amp;tabs=Windows)建立存放庫存取權杖。<li>Azure DevOps個人存取權杖(PAT)的必要許可權。<br>這些許可權可讓Cloud Manager存取存放庫內容、管理提取請求，以及設定或回應webhook事件。<br>當您在Azure DevOps中建立應用程式密碼時，請確定它包含下列必要的應用程式密碼許可權：<ul><li>存放庫（唯讀）</li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**存取Token**&#x200B;欄位中，貼上您剛建立的權杖。 |

   另請參閱[管理存取權杖](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

   >[!IMPORTANT]
   >
   >功能&#x200B;**新增存取權杖**&#x200B;目前處於早期採用者階段。 其他的功能正在規劃中。因此，存取權杖所需的權限可能會變更。另外，用於管理權杖的使用者介面可能會更新，可能包括權杖過期日期等功能。並且，自動檢查以確保連結至存放庫的權杖保持有效。

1. 按一下「**驗證**」。

   驗證之後，外部存放庫即可使用並連結至管道。


## 將驗證的外部存放庫連結至管道。 {#validate-ext-repo}

1. 新增或編輯管道：
   * [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [編輯管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   <!-- Add an Edge Delivery Pipeline -->

   ![管道的來源代碼存放庫和 Git 分支](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *新增非生產管道對話框，其中包含選取的存放庫和 Git 分支，*

1. 新增或編輯管道時，若要指定新管道或現有管道的&#x200B;**來源代碼**&#x200B;位置，請從&#x200B;**存放庫**&#x200B;下拉清單中選取要使用的外部存放庫。

1. 在 **Git 分支**&#x200B;下拉清單中，選取分支作為管道的來源。

1. 按一下「**儲存**」。


>[!TIP]
>
>如需關於在 Cloud Manager 管理存放庫的詳細資訊，請參閱「[Cloud Manager 存放庫](/help/implementing/cloud-manager/managing-code/managing-repositories.md)」。


## 為外部存放庫設定webhook {#configure-webhook}

Cloud Manager可讓您為已新增的外部Git存放庫設定webhook。 請參閱[新增外部存放庫](#add-ext-repo)。 這些Webhook可讓Cloud Manager接收與Git廠商解決方案中不同動作相關的事件。

例如，webhook可讓Cloud Manager根據下列事件觸發動作：

* 提取請求(PR)建立 — 起始PR驗證功能。
* 推播事件 — 在「開啟Git認可」觸發器開啟（啟用）時啟動管道。
* 未來的評論型動作 — 允許工作流程，例如從PR直接部署至快速開發環境(RDE)。

`GitHub.com`上託管的存放庫不需要Webhook設定，因為Cloud Manager會直接透過GitHub應用程式整合。

對於已上線存取權杖的所有其他外部存放庫，例如GitHub Enterprise、GitLab和Bitbucket，webhook設定可用，且必須手動設定。

**若要設定外部存放庫的webhook：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取您要設定外部Git存放庫webhook的程式。

1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。

1. 在左側功能表的&#x200B;**方案**&#x200B;標題下，按一下![資料夾大綱圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存放庫**。

1. 在&#x200B;**存放庫**&#x200B;頁面上，使用&#x200B;**型別**&#x200B;欄引導您進行選取，找出您想要的存放庫，然後按一下旁邊的![省略符號 — 更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![在下拉式功能表中為選取的存放庫設定Webhook選項](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. 從下拉式功能表，按一下&#x200B;**設定Webhook**。

   ![設定Webhook對話方塊](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. 在&#x200B;**設定Webhook**&#x200B;對話方塊中，執行下列動作：

   1. 在&#x200B;**Webhook URL**&#x200B;欄位旁邊，按一下![復製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)。
以純文字檔案貼上URL。 您的Git供應商Webhook設定需要複製的URL。
   1. 在&#x200B;**Webhook密碼**&#x200B;權杖/金鑰欄位旁邊，按一下&#x200B;**產生**，然後按一下![復製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)。
將密碼貼入純文字檔。 您的Git廠商Webhook設定需要複製的密碼。
1. 按一下&#x200B;**關閉**。
1. 導覽至您的Git廠商解決方案（GitHub Enterpriser、GitLab或Bitbucket）。

   在[新增外部存放庫](#add-ext-repo)中可取得webhook組態的所有詳細資訊以及每個廠商所需的事件。 在步驟8下，檢視表格。

1. 找到解決方案的&#x200B;**Webhook**&#x200B;設定區段。
1. 將您先前複製的Webhook URL貼到URL文字欄位中。
   1. 將Webhook URL中的`api_key`查詢引數取代為您自己的實際API金鑰。

      若要產生API金鑰，您必須在Adobe Developer Console中建立整合專案。 如需完整詳細資訊，請參閱[建立API整合專案](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。

1. 將您先前複製的Webhook密碼貼到&#x200B;**密碼** （或&#x200B;**密碼金鑰**&#x200B;或&#x200B;**密碼權杖**）文字欄位中。
1. 設定webhook以傳送Cloud Manager預期的所需事件。

   | 存放庫 | 必要的webhook事件 |
   | --- | --- |
   | GitHub企業版 | 這些事件可讓Cloud Manager回應GitHub活動，例如提取請求驗證、管道的推播型觸發器或Edge Delivery Services程式碼同步。<br>請確定webhook已設定為在下列必要webhook事件上觸發：<ul><li>提取請求<li>推送<li>問題註解</li></li></li></ul></ul></ul> |
   | GitLab | 這些webhook事件可讓Cloud Manager在推送程式碼或提交合併請求時觸發管道。 也會追蹤與提取請求驗證相關的註解（透過附註事件）。<br>請確定webhook已設定為在下列必要webhook事件上觸發<ul><li>推送事件<li>合併請求事件<li>附註事件</li></li></li></ul></ul></ul> |
   | Bitbucket | 這些事件確保Cloud Manager可以驗證提取請求、回應程式碼推送，以及與評論互動以協調管道。<br>請確定webhook已設定為在下列必要webhook事件上觸發<ul><li>提取請求：已建立<li>提取請求：已更新<li>提取請求：已合併<li>提取請求：註解<li>存放庫：推播</li></li></li></ul></ul></ul> |
   | Azure DevOps | 這些事件確保Cloud Manager可以驗證提取請求、回應程式碼推送，以及與評論互動以協調管道。<br>請確定webhook已設定為在下列必要webhook事件上觸發<ul><li>存放庫：推播</li></li></ul></ul></ul> |


### 使用Webhook驗證提取請求

正確設定Webhook後，Cloud Manager會自動觸發管道執行，或針對您的存放庫進行PR驗證檢查。

下列行為適用：

* **GitHub Enterprise**

  建立檢查時，其外觀類似下列熒幕擷圖。 與`GitHub.com`的主要差異在於`GitHub.com`使用檢查執行，而GitHub Enterprise （使用個人存取權杖）會產生認可狀態：

  ![認可狀態以指示GitHub Enterprise上的PR驗證程式](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **位元貯體**

  程式碼品質驗證執行時：

  ![執行程式碼品質驗證時的狀態](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  使用認可狀態來追蹤PR驗證進度。 在以下案例中，熒幕擷圖顯示程式碼品質驗證因客戶問題而失敗時會發生什麼情況。 新增附有詳細錯誤資訊的註解，並建立確認檢查，以顯示失敗（顯示在右側）：

  位元貯體的![提取要求驗證狀態](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  GitLab互動僅依賴評論。 驗證開始時，會新增註解。 驗證完成後（無論成功還是失敗），初始註解都將被移除並替換為包含驗證結果或錯誤詳細資料的新註解。

  程式碼品質驗證執行時：

  ![執行程式碼品質驗證時](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  完成冷品質驗證時：

  ![當冷品質驗證完成時](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  當程式碼品質驗證失敗並出現錯誤時：

  ![當程式碼品質驗證失敗並出現錯誤時](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

  當程式碼品質驗證因客戶問題而失敗時：

  ![當程式碼品質驗證因客戶問題而失敗時](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## 疑難排解webhook問題

* 請確定Webhook URL包含有效的API金鑰。
* 檢查您的Git廠商設定中是否已正確設定webhook事件。
* 如果PR驗證或管道觸發程式無法運作，請確認Cloud Manager和您的Git供應商中的Webhook密碼都是最新的。


