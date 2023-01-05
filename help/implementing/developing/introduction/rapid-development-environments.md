---
title: 快速開發環境
description: 了解如何善用快速開發環境，在雲端環境上快速反覆開發。
hidefromtoc: true
source-git-commit: 983901387d059a98942b4f7c533770a55dd4ff4a
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 7%

---


# 快速開發環境 {#rapid-development-environments}

>[!AVAILABILITY]
>
>此功能尚未提供。

為了部署變更，目前的雲端開發環境需要使用採用廣泛程式碼安全性和品質規則的程式，稱為CI/CD管道。 對於需要快速和迭代更改的情況，Adobe引入了快速開發環境（簡稱RDE）。

RDE可讓開發人員快速部署和審核變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

在RDE中測試變更後，即可透過Cloud Manager管道部署至一般雲端開發環境。

## 簡介 {#introduction}

RDE可用於程式碼、內容，以及Apache或Dispatcher設定。 與一般雲端開發環境不同，開發人員可使用本機命令列工具，將本機建置的程式碼同步至RDE。

每個計畫都布建了RDE。 如果是沙箱帳戶，則會在數小時未使用後休眠。

通常，單一開發人員會在指定時間使用RDE來測試和除錯特定功能。 完成開發工作階段時，RDE可重設為下次使用的預設狀態。

<!-- Temporarily hiding this. See CQDOC-19795 for more details

Additional RDEs may be purchased for Production programs -->

## 在程式中啟用RDE {#enabling-rde-in-a-program}

請依照下列步驟，使用Cloud Manager為您的方案建立RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要添加RDE的程式以顯示其詳細資訊。

   * 可將RDE新增至兩者 [沙箱方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [生產計畫。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. 在&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**新增環境**&#x200B;以新增環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

      ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選擇 **快速發展** 在 **選擇環境類型** 標題。
      * 可用/使用的環境數量會以括弧顯示在環境類型後面。
   * 提供 **名稱** 環境。
   * 提供選用 **說明** 環境。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

現在&#x200B;**總覽**&#x200B;畫面會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。

如需有關使用Cloud Manager建立環境、管理誰有權存取環境以及指派自訂網域的詳細資訊，請參閱 [Cloud Manager檔案。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安裝RDE命令行工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager為程式新增RDE後，您就可以依照下列步驟所述設定命令列工具，以與程式互動：

1. 按照以下過程安裝Adobe I/OCLI工具 [此處](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安裝Adobe I/OCLI工具cloud manager外掛程式，並依照說明進行配置 [此處](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 運行以下命令以安裝Adobe I/OCLI工具AEM RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 為您的組織ID設定cloud manager外掛程式：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   並將英數字串取代為您自己的組織ID，以便使用策略來查詢 [此處](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 接下來，配置您的程式id:

   `aio config:set cloudmanager_programid 12345`

1. 然後，設定RDE要附加至的環境id:

   `aio config:set cloudmanager_environmentid 123456`

1. 完成外掛程式的設定後，請執行

   `aio login`

   成功登入的回應應類似於下列輸出，但您可以忽略顯示的值。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. 驗證登錄是否通過運行成功完成

   `aio cloudmanager:list-programs`

   這應該會列出您所設定組織下的所有程式。

   請注意，上述要求您必須是Cloud Manager的成員 **開發人員 — Cloud Service** 產品設定檔。 請參閱 [本頁](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 以取得更多詳細資訊。

   或者，如果您可以執行以下命令登入開發人員主控台，則可確認您擁有此開發人員角色：

   `aio cloudmanager:environment:open-developer-console`

## 在開發新功能時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用下列工作流程來開發新功能：

* 當達到中間里程碑並透過AEMas a Cloud Service SDK在本機成功驗證時，程式碼應提交至尚未納入主要行的git功能分支，不過提交至git是選用項目。 構成「中間里程碑」的內容因團隊習慣而異。 例如幾行新程式碼、半天工作或完成子功能。

* 如果RDE已被其他功能使用，並且您想要 [將其重設為預設狀態](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重設需要幾分鐘的時間，所有現有內容和程式碼都將被刪除。 您可以使用RDE狀態命令來確認RDE已就緒。

* 使用RDE命令行介面，將本地代碼同步到RDE。 選項包括安裝內容套件、特定套件組合、OSGI設定檔案、內容檔案，以及Apache/Dispatcher設定的zip檔案。 也可參考遠端內容套件。 請參閱 [RDE命令行工具](#rde-cli-commands) 一節以取得詳細資訊。 您可以使用status命令來驗證部署是否成功。 （可選）使用包管理器來安裝內容包。

* 在RDE中測試程式碼。 Cloud Manager中提供製作和發佈URL。

* 如果程式碼的行為不如預期，請使用標準除錯技術來了解問題並進行適當的變更。 若不將程式碼修改提交至git（因為這些修改尚未通過驗證），請使用本機CLI將程式碼同步至RDE。 請持續反覆進行，直到問題解決為止。

* 一旦程式碼如預期般運作，請將程式碼提交至Git功能分支。

* 同步至RDE的程式碼不會使用Cloud Manager管道，因此現在您應使用Cloud Manager非生產管道，將git功能分支部署至雲端開發環境。 這可驗證程式碼是否通過Cloud Manager品質入口，讓您確信程式碼稍後將可透過Cloud Manager生產管道成功部署。

* 對每個中繼里程碑重複上述步驟，直到該功能的所有程式碼就緒為止，並在RDE和雲端開發環境中皆正常運作。

* 透過Cloud Manager生產管道將程式碼部署至生產環境。

## 使用RDE對現有功能進行偵錯 {#use-rde-to-debug-an-existing-feature}

工作流程類似於開發新功能。 區別在於，同步至RDE的程式碼會反映推送至發現問題之環境的Git標籤。 此外，部署與上游環境相符的內容可能會很實用。 這可透過匯出和匯入內容套件來達成。

## 多名開發人員協作使用同一個RDE {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支援單一專案。 由於程式碼會從本機開發環境同步至RDE環境，因此某位開發人員在指定時間獨自使用最自然的作法。

不過，若經過謹慎的協調，可能有多名開發人員驗證特定功能或對特定問題進行除錯。 關鍵是每個開發人員都會保持其本機專案同步，讓特定開發人員所做的程式碼變更會被其他開發人員吸收，否則某個開發人員可能會不慎覆寫其他開發人員的程式碼。 建議的策略是，每位開發人員在同步至RDE前，先將變更提交至共用的Git分支，讓其他開發人員在自行變更前先提取變更。

## RDE命令行工具命令 {#rde-cli-commands}

### 說明/一般資訊 {#help}

* 對於命令清單，鍵入：

   `aio aem:rde`

* 有關命令的詳細幫助，請鍵入：

   `aio aem rde <command> --help`

### 部署到RDE {#deploying-to-rde}

本節說明如何使用RDE CLI來部署、安裝或更新套件組合、OSGI設定、內容套件、個別內容檔案，以及Apache或Dispatcher設定。

一般使用模式為 `aio aem:rde:install <artifact>`.

您可以找到下列範例：

<u>部署內容套件</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的回應類似下列：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

您可以參考遠端存放庫（可選）:

`aio aem:rde:install 'https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip'`

<u>部署OSGI設定</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

其中成功部署的回應類似下列：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署套件</u>

要部署捆綁包，請使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

其中成功部署的回應類似下列：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署內容檔案</u>

要部署內容檔案，請使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

其中成功部署的回應類似下列：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher設定</u>

此類型的設定需要整個資料夾結構的壓縮檔案形式。 您可以從Dispatcher設定資料夾的根目錄中執行此命令來壓縮：

`zip -y -r dispatcher.zip`

然後，使用以下命令部署配置：

`aio aem:rde:install -t dispatcher-config dispatcher-wknd-2.1.0.zip`

成功的部署會產生類似下列的回應：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署至RDE的程式碼不會經過Cloud Manager管道及其相關的品質閘道，但程式碼會經過一些分析，進而報告錯誤，如下列程式碼範例所示：

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

上述程式碼範例說明如果套件組合未解析的行為，在此情況下，此套件會「暫存」，且只有透過安裝其他程式碼而滿足其需求（缺少匯入，在此例中為）時才會安裝。

### 檢查RDE的狀態 {#checking-rde-status}

您可以使用RDE CLI來檢查環境是否已準備好部署到，因為哪些部署是通過RDE插件進行的。

正在執行:

`aio aem:rde:status`

將返回：

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

如果命令傳回關於執行個體部署的備注，您仍可繼續執行下次更新，但您最後一個更新可能尚未顯示在執行個體上。

### 顯示部署歷史記錄 {#show-deployment-history}

您可以執行以下程式來檢查對RDE進行的部署歷史記錄：

`aio aem:rde:history`

其會以下列形式傳回回應：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 從RDE刪除 {#deleting-from-rde}

您可以透過CLI工具刪除先前已部署至RDE的配置和套件組合。 使用 `status` 命令，其中包括 `bsn` 對於套件和 `pid` 供delete命令中參考的設定。

例如，若 `com.adobe.granite.demo.MyServlet.cfg.json` 已安裝， `bsn` 只是 `com.adobe.granite.demo.MyServlet`，而 **cfg.json** 尾碼。

不支援刪除內容包或內容檔案。 若要移除這些變數，RDE應重設，而這會將其傳回預設狀態。

如需詳細資訊，請參閱下列範例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

## 重設 {#reset-rde}

重設RDE會同時移除製作和發佈執行個體中的所有自訂程式碼、設定和內容。 例如，如果已使用RDE測試特定功能，並且您想要將其重置為預設狀態以測試不同功能，則此功能會很有用。

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

您可以依照下列步驟，使用Cloud Manager重設RDE:

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要重置RDE的程式。

1. 在&#x200B;**總覽**&#x200B;頁面，按一下畫面頂端的&#x200B;**環境**&#x200B;索引標籤。

   ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**全部顯示**&#x200B;按鈕直接跳到&#x200B;**環境**&#x200B;索引標籤。

      ![顯示全部選項](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 此 **環境** 窗口開啟，並列出程式的所有環境。

   ![環境索引標籤](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 按一下要重置的RDE的刪節號按鈕，然後選擇 **重設**.

   ![檢視環境詳細資訊](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 按一下以確認您要重設RDE **重設** 的下一頁。

   ![確認重設](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager會透過橫幅通知確認重設程式已開始。

   ![重設橫幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重設程式一旦啟動，通常需要幾分鐘的時間才能完成，並將環境恢復為預設狀態。 您可以隨時在 **狀態** 欄 **環境** 卡片或 **環境** 窗口。

![RDE重置狀態](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您也可以直接從 **環境** 卡 **概述** 頁面。

![從環境卡重置RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

如需如何使用Cloud Manager管理環境的詳細資訊，請參閱 [Cloud Manager檔案。](/help/implementing/cloud-manager/manage-environments.md)

## 記錄 {#logging}

可修改OSGi設定來設定記錄層級。 檢查 [檔案](/help/implementing/developing/introduction/logging.md) 以取得更多資訊。

## RDE與雲端開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在許多方面與雲端開發環境類似，但為了能快速同步程式碼，架構上仍有一些微幅差異。 將程式碼傳送至RDE的機制不同 — 對於RDE，一個會同步來自本機開發環境的程式碼，而對於雲端開發環境，一個會透過Cloud Manager部署程式碼。

基於這些原因，建議您在RDE環境上驗證程式碼後，使用非生產管道將程式碼部署至雲端開發環境。 最後，使用生產管道部署前，請先測試程式碼。

<!-- Temporarily hiding this. See CQDOC-19795 for more details

## How many RDEs do I need? {#how-many-rds-do-i-need}

The purchase of additional RDEs for Production programs will be possible beginning with late January.

The number of RDEs needed depends on the make-up and processes of an organization. The most flexible model is where an organization purchases a dedicated RDE for each one of their AEM CS developers. In this model, each developer can test their code on the RDE without needing to coordinate with other team members around whether an RDE environment is available.

At the other extreme, a team with a single RDE may use internal processes to coordinate which developer can use the environment at a given time. This can possibly be whenever a developer has hit an intermediate feature milestone and is ready to validate in a Cloud environment where they can quickly make the changes they need.

An intermediate model is one where an organization purchases a number of RDEs that will create a situation in which not every developer will have a dedicated environment, but there is a greater likelihood of an unused RDE being available. One strategy could be to allocate an RDE per scrum team or major feature. Internal processes may be used to coordinate usage of the environments. -->
