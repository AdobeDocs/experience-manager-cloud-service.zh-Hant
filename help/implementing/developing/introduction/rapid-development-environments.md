---
title: 快速開發環境
description: 了解如何善用快速開發環境，在雲端環境上快速反覆開發。
source-git-commit: 2de6e2b6357f6cd03be2736d09cb4687ff337450
workflow-type: tm+mt
source-wordcount: '3304'
ht-degree: 5%

---


# 快速開發環境 {#rapid-development-environments}

為了部署變更，目前的雲端開發環境需要使用採用廣泛程式碼安全性和品質規則的程式，稱為CI/CD管道。 對於需要快速和迭代更改的情況，Adobe引入了快速開發環境（簡稱RDE）。

RDE可讓開發人員快速部署和審核變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

在RDE中測試變更後，即可透過Cloud Manager管道部署至一般雲端開發環境。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以參閱其他示範影片 [如何設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [如何使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)，和 [開發生命週期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) 使用RDE。

## 簡介 {#introduction}

RDE可用於程式碼、內容，以及Apache或Dispatcher設定。 與一般雲端開發環境不同，開發人員可使用本機命令列工具，將本機建置的程式碼同步至RDE。

每個計畫都布建了RDE。 如果是沙箱帳戶，則會在數小時未使用後休眠。

建立後，RDE會設為最新可用的AEM版本。 RDE重設（可使用Cloud Manager執行）將循環RDE，並將其設為最新可用的AEM版本。

通常，單一開發人員會在指定時間使用RDE來測試和除錯特定功能。 完成開發工作階段時，RDE可重設為下次使用的預設狀態。

其他RDE可授權給生產（非沙箱）方案。

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

建立後，RDE會設為最新可用的AEM版本。 RDE重設（也可使用Cloud Manager執行）將循環RDE，並將其設為最新可用的AEM版本。

如需有關使用Cloud Manager建立環境、管理誰有權存取環境以及指派自訂網域的詳細資訊，請參閱 [Cloud Manager檔案。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安裝RDE命令行工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager為程式新增RDE後，您就可以依照下列步驟所述設定命令列工具，以與程式互動：

>[!IMPORTANT]
>
>請確定您有 [已安裝節點和NPM](https://nodejs.org/en/download/) 以使Adobe I/OCLI和相關外掛程式正常運作。


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

   >[!TIP]
   >
   >如果您看到 `Warning: cloudmanager:list-programs is not a aio command.` 錯誤，您需要安裝 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 執行以下命令：
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

如需詳細資訊和示範，請參閱 [如何設定RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) 影片教學課程。

## 在開發新功能時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用下列工作流程來開發新功能：

* 當達到中間里程碑並透過AEMas a Cloud Service SDK在本機成功驗證時，程式碼應提交至尚未納入主要行的git功能分支，不過提交至git是選用項目。 構成「中間里程碑」的內容因團隊習慣而異。 例如幾行新程式碼、半天工作或完成子功能。

* 如果RDE已被其他功能使用，並且您想要 [將其重設為預設狀態](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重設需要幾分鐘的時間，所有現有內容和程式碼都將被刪除。 您可以使用RDE狀態命令來確認RDE已就緒。 RDE將會提供最新的AEM版本。

   >[!IMPORTANT]
   >
   > 如果您的測試和生產環境未收到自動AEM版本更新，且遠落在最新的AEM版本之後，請留意RDE上執行的程式碼可能不符合程式碼在測試和生產上的運作方式。 在此情況下，在將程式碼部署至生產環境之前，請務必先在測試環境上對程式碼執行徹底測試。


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

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

依預設，成品會部署至製作和發佈層級，但可使用「 — s」標幟來鎖定特定層級。

任何AEM套件皆可部署，例如包含程式碼、內容或 [容器包裝](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （又稱為「all」套件）。

>[!IMPORTANT]
>
>WKND專案的Dispatcher設定不會透過上述內容套件安裝進行部署。 您需要依照「部署Apache/Dispatcher設定」步驟，個別部署。

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

此類型的設定需要整個資料夾結構的壓縮檔案形式。

從 `dispatcher` AEM專案的模組，您可以執行下列maven命令來壓縮dispatcher設定：

`mvn clean package`

或使用下列zip命令，從 `src` 目錄 `dispatcher` 模組：

`zip -y -r dispatcher.zip .`

然後，使用以下命令部署配置：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假設您部署 [WKND](https://github.com/adobe/aem-guides-wknd) 專案的dispatcher設定。 請務必更換 `X.X.X` 部署專案的dispatcher設定時，使用對應的WKND專案版本號碼或您專屬的版本號碼。

>[!NOTE]
>
>RDE支援「彈性模式」調度器設定，但不支援「舊式模式」調度器設定。 請參閱 [dispatcher檔案](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以取得這兩種模式的相關資訊。 您也可以參閱 [遷移到靈活模式](/help/implementing/dispatcher/validation-debug.md#migrating)，如果尚未這麼做。

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

如需詳細資訊和示範，請參閱 [如何使用RDE命令](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) 影片教學課程。

## 重設 {#reset-rde}

重設RDE會同時移除製作和發佈執行個體中的所有自訂程式碼、設定和內容。 例如，如果已使用RDE測試特定功能，並且您想要將其重置為預設狀態以測試不同功能，則此功能會很有用。

重設會將RDE設為最新可用的AEM版本。

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

## 執行模式 {#runmodes}

您可以在資料夾名稱上使用尾碼來套用RDE特定OSGI設定，如下列範例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

請參閱 [runmode檔案](/help/implementing/deploying/overview.md#runmodes) ，了解有關運行模式的一般資訊。

>[!NOTE]
>
>RDE OSGI配置是唯一的，因為它繼承了由捆綁包聲明的任何OSGI屬性的值 `dev` 運行模式。

RDE與其他環境不同，其內容可安裝在/apps底下的install.rde資料夾（或install.author.rde或install.publish.rde）中。 這可讓您將內容提交至Git，並使用命令列工具將其傳送至RDE。

## 填入內容 {#populating-content}

重設RDE時，會移除所有內容，因此，如果需要，必須執行明確動作以新增內容。 最佳實務是，請考慮組裝一組內容，以用作RDE中驗證或偵錯功能的測試內容。 使用該內容填入RDE的幾種可能策略：

1. 使用命令行工具將內容包顯式同步到RDE

1. 將範例內容放置並提交至git中/apps底下的install.rde資料夾，然後使用命令列工具將整體內容套件同步至RDE。

1. 使用套件管理器

請注意，同步內容套件時，限制為1GB。

## 記錄 {#logging}

可修改OSGi設定來設定記錄層級。 檢查 [檔案](/help/implementing/developing/introduction/logging.md) 以取得更多資訊。

## RDE與雲端開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在許多方面與雲端開發環境類似，但為了能快速同步程式碼，架構上仍有一些微幅差異。 將程式碼傳送至RDE的機制不同 — 對於RDE，一個會同步來自本機開發環境的程式碼，而對於雲端開發環境，一個會透過Cloud Manager部署程式碼。

基於這些原因，建議您在RDE環境上驗證程式碼後，使用非生產管道將程式碼部署至雲端開發環境。 最後，使用生產管道部署前，請先測試程式碼。

另請注意下列考量事項：

* RDE不包含預覽層
* RDE目前不支援檢視和偵錯使用Cloud Manager前端管道部署的前端程式碼。
* RDE目前不支援發行前管道。


## 我需要多少個RDE? {#how-many-rds-do-i-need}

每個授權解決方案都提供RDE，而Adobe也提供額外的RDE，這些RDE可授權給生產（非沙箱）方案。

需要的RDE數量取決於組織的組成和流程。 最靈活的模型是，組織可為每位AEM Cloud Service開發人員購買專屬的RDE。 在此模型中，每個開發人員都可以在RDE上測試其程式碼，而不需就RDE環境是否可用與其他團隊成員進行協調。

在另一個極端，具有單一RDE的團隊可能會使用內部流程來協調哪些開發人員可以在指定時間使用環境。 開發人員只要達到中繼功能里程碑並準備好在雲端環境中驗證，就能快速進行所需的變更，就可能是此情形。

中間模型是指組織購買多個RDE，因此未使用RDE可用的可能性較大的模型。 一個策略可能是為每個掃描團隊或主要功能分配RDE。 內部過程可用於協調環境的使用。

## AEM FormsCloud Service快速開發環境(RDE)與其他環境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms開發人員可使用AEM FormsCloud Service快速開發環境來快速開發適用性Forms、工作流程和自訂項目，例如自訂核心元件、與協力廠商系統的整合等。 AEM FormsCloud Service快速開發環境(RDE)不支援通訊API，以及需要記錄檔的功能，例如在提交最適化表單時產生記錄檔。 下列AEM Forms功能不適用於快速開發環境(RDE):

* 設定最適化表單的記錄檔案
* 在提交最適化表單或使用工作流程步驟時產生記錄檔案
* 在工作流中以「電子郵件提交」操作或「電子郵件」步驟作為附件發送記錄文檔
* 在適用性表單或工作流程步驟中使用Adobe Sign
* 通訊API

>[!NOTE]
>
> 快速開發環境(RDE)的UI與Forms的其他Cloud Service環境之間沒有差異。 所有與「記錄檔案」相關的選項（例如為最適化表單選取記錄範本檔案）會繼續顯示在UI中。 這些環境沒有測試這些選項的通訊API和記錄檔案功能。 因此，當您選擇任何需要通信API或記錄檔案功能的選項時，將不執行任何操作，並顯示或返回錯誤消息。

## RDE教學課程

若要了解AEMas a Cloud Service中的RDE，請參閱 [示範如何設定、如何使用及開發生命週期的影片教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)

