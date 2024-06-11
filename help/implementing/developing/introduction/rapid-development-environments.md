---
title: 快速開發環境
description: 瞭解如何使用快速開發環境在雲端環境中進行快速開發反複專案。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 1c157af3f7ed4ab3ae4a67d7db200e772cf8b565
workflow-type: tm+mt
source-wordcount: '4312'
ht-degree: 4%

---

# 快速開發環境 {#rapid-development-environments}

若要部署變更，目前的雲端開發環境需要使用採用廣泛程式碼安全性和品質規則（稱為CI/CD管道）的程式。 對於需要快速反複變更的情況，Adobe已推出快速開發環境（簡稱RDE）。

RDE可讓開發人員快速部署和檢閱變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

在RDE中測試變更後，可以透過Cloud Manager管道將其部署到常規雲端開發環境。

>[!NOTE]
> 與RDE開發人員聯絡，瞭解 [不和諧的頻道](https://discord.com/channels/1131492224371277874/1245304281184079872). 歡迎您針對RDE主題提出任何問題或給予回饋。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以觀看其他示範影片 [如何設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)， [使用方式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)，以及 [開發生命週期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) 使用RDE。

## 簡介 {#introduction}

RDE可用於程式碼、內容以及Apache或Dispatcher設定。 不像一般的雲端開發環境，開發人員可以使用本機命令列工具，將本機建置的程式碼同步到RDE。

每個方案都布建了RDE。 如果存在沙箱帳戶，則會在不使用數小時後休眠。

建立後，RDE會設定為最新可用的Adobe Experience Manager (AEM)版本。 RDE重設（可使用Cloud Manager執行）會循環RDE並將其設定為最新可用的AEM版本。

通常，單一開發人員在指定時間會使用RDE來測試和偵錯特定功能。 當開發工作階段完成時，RDE可以重設為預設狀態以供下次使用。

其他RDE可授權用於生產（非沙箱）計畫。

## 在程式中啟用RDE {#enabling-rde-in-a-program}

請按照以下步驟操作，以便您可以使用Cloud Manager為您的計畫建立RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要新增RDE的計畫以顯示其詳細資訊。

   * RDE可新增至兩者 [沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. 在「**計畫概觀**」頁面，按一下「**環境**」卡上的「**新增環境**」以新增環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

     ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選取 **快速開發** 在 **選取環境型別** 標題。
      * 可用/已使用環境的數量會顯示在環境型別後面的括弧中。
   * 提供 **名稱** 適用於環境。
   * 提供選填 **說明** 適用於環境。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

此 **概觀** 畫面現在會在中顯示您的新環境 **環境** 卡片。

建立後，RDE會設定為最新可用的AEM版本。 RDE重設（也可以使用Cloud Manager執行）會循環RDE並將其設定為最新可用的AEM版本。

如需有關使用Cloud Manager建立環境、管理誰有權存取環境以及指派自訂網域的詳細資訊，請參閱 [Cloud Manager檔案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## 安裝RDE命令列工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager為程式新增RDE後，您可以透過設定命令列工具與其互動，如以下步驟所述：

>[!IMPORTANT]
>
>請確定您擁有最新版本的 [已安裝節點和NPM](https://nodejs.org/en/download/) 以讓Adobe I/OCLI和相關外掛程式正常運作。


1. 依照以下程式安裝Adobe I/OCLI工具 [此處](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安裝Adobe I/OCLI工具Cloud Manager外掛程式，並依照說明進行設定 [此處](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 執行下列命令，安裝Adobe I/OCLI工具AEM RDE外掛程式：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 為您的組織ID設定Cloud Manager外掛程式：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   並將英數字串取代為您自己的組織ID，您可利用策略查詢此組織ID [此處](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 接下來，設定您的程式ID：

   `aio config:set cloudmanager_programid 12345`

1. 然後，設定要附加RDE的環境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 完成外掛程式的設定後，請透過執行

   `aio login`

   成功登入時的回應應與下面的輸出類似，但您可以忽略顯示的值。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   此步驟需要您是Cloud Manager的成員 **開發人員 — Cloud Service** 產品設定檔。 另請參閱 [此頁面](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 以取得更多詳細資料。

   或者，如果您可以透過執行此命令登入開發人員主控台，則可以確認您擁有此開發人員角色：

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >如果您看到 `Warning: cloudmanager:list-programs is not a aio command.` 錯誤，您必須安裝 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 透過執行以下命令：
   >
   >```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. 執行以驗證登入是否成功完成

   `aio cloudmanager:list-programs`

   這應該會列出您設定之組織下的所有程式。


如需詳細資訊和示範，請觀看教學課程影片 [如何設定RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html).

## 安裝RDE命令列工具（使用互動模式） {#installing-the-rde-command-line-tools-interactive}

>[!NOTE]
>
> 此設定程式尚無法使用。 它將在6月的某個時候取代先前的程式。
> 

使用Cloud Manager為程式新增RDE後，您可以透過設定命令列工具與其互動，如以下步驟所述：

>[!IMPORTANT]
>
>請確定您擁有最新版本的 [已安裝節點和NPM](https://nodejs.org/en/download/) 以讓Adobe I/OCLI和相關外掛程式正常運作。


1. 依照以下說明安裝Adobe I/OCLI工具 [程式](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安裝Adobe I/OCLI工具AEM RDE外掛程式：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 設定RDE外掛程式以使用您的組織、程式和環境。 以下的設定指令將以互動方式提供使用者組織內的程式清單，並顯示該程式中可供選擇的RDE環境。

   ```
   aio login
   aio aem:rde:setup
   ```

   如果目的是使用指令碼式環境，則可以跳過設定步驟，在這種情況下，組織、程式和環境值可以包含在每個命令中。 [如需詳細資訊，請參閱下方的rde命令](#rde-cli-commands).

### 互動式設定

setup命令會詢問所提供的組態應該儲存在本機還是全域。

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

選擇 `no` 至
* 在您的aio設定中，將組織、計畫和環境全域儲存。
* 僅適用於單一RDE。

選擇 `yes` 至
* 將組織、方案和環境本機儲存在目前的目錄中，在 `.aio` 檔案。 如果您想要將檔案提交至版本控制，讓其他複製Git存放庫的人可以使用此檔案，就可以使用此功能。
* 使用多個RDE，以便切換到其他目錄時會改用該設定。
* 在程式化前後關聯中使用組態，例如可參照它的指令碼。


選取本機或全域組態後，setup命令會嘗試從您目前的登入讀取您的組織id，然後讀取組織的程式。 如果找不到組織，您可以手動輸入，並附上一些指引。

```
 Selected only organization: XYXYXYXYXYXYXYXXYY
 retrieving programs of your organization ...
```

擷取程式後，使用者可以從清單中選取，也可以鍵入以進行篩選。
選擇計畫時，會列出可供選擇的RDE環境清單。
如果只有一個可用的方案和/或RDE環境，則會自動選取它。

若要檢視目前的環境內容，請執行：

```aio aem rde setup --show```

其他指令會以類似下列的結果回應：

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

## 開發新功能時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用下列工作流程來開發新功能：

* 當達到中繼里程碑並成功透過AEMas a Cloud ServiceSDK在本機驗證時，將程式碼提交到Git功能分支。 雖然提交至Git是選用專案，但分支不應是主行的一部分。 構成「中繼里程碑」的要素因團隊習慣而異。 範例包括幾行程式碼、半天工作或完成子功能。

* 如果RDE已由其他功能使用且您想要 [將其重設為預設狀態](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->重設需要幾分鐘的時間，而且所有現有內容和程式碼都會被刪除。 您可以使用RDE狀態指令來確認RDE已就緒。 RDE會隨附最新的AEM發行版本。

  >[!IMPORTANT]
  >
  > 如果您的測試環境和生產環境未收到自動AEM版本更新，並且落後於最新的AEM版本版本，則在RDE上執行的程式碼可能與測試環境和生產環境上的程式碼運作方式不符。 在這種情況下，將程式碼部署到生產環境之前，尤其必須在測試環境上執行徹底的程式碼測試。


* 使用RDE命令列介面，將本機程式碼同步至RDE。 選項包括安裝內容套件、特定套件組合、OSGI設定檔案、內容檔案和Apache/Dispatcher設定的zip檔案。 也可以參考遠端內容套件。 另請參閱 [RDE命令列工具](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands) 以取得詳細資訊。 您可以使用status命令來驗證部署是否成功。 或者，使用封裝管理員來安裝內容封裝。

* 在RDE中測試程式碼。 在Cloud Manager中可以使用作者和發佈URL。

* 如果程式碼的行為與預期不符，請使用標準偵錯技巧來瞭解問題並做出適當的變更。 無須認可對Git的程式碼修改（由於尚未驗證），請使用本機CLI將程式碼同步至RDE。 持續反複運算，直到問題解決為止。

* 程式碼如預期運作後，將程式碼提交到Git功能分支。

* 同步至RDE的程式碼不使用Cloud Manager管道，因此現在應使用Cloud Manager非生產管道，將Git功能分支部署至雲端開發環境。 這將驗證計畫碼是否通過Cloud Manager品質關卡，並讓您確信計畫碼稍後會使用Cloud Manager生產管道成功部署。

* 對每個中繼里程碑重複上述步驟，直到功能的所有程式碼準備就緒為止，並在RDE和雲端開發環境中正常運作。

* 透過Cloud Manager生產管道將計畫碼部署到生產環境。

## 使用RDE除錯現有功能 {#use-rde-to-debug-an-existing-feature}

工作流程類似於開發新功能。 差異在於同步至RDE的程式碼會反映推送至發現問題之環境的任何專案的Git標籤。 此外，部署符合上游環境的內容可能會有幫助。 這可透過匯出和匯入內容套件來完成。

## 多位開發人員在同一個RDE上共同作業 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支援一個專案。 由於程式碼會從本機開發環境同步至RDE環境，因此對於一個開發人員而言，在指定時間自行使用程式碼是最自然的事情。

不過，只要仔細協調，多位開發人員就能驗證特定功能或偵錯特定問題。 關鍵是每個開發人員將其本機專案保持同步，以便其他開發人員吸收特定開發人員所做的程式碼變更，否則一個開發人員可能會無意中覆寫另一個開發人員的程式碼。 建議的策略是讓每位開發人員在同步至RDE之前，將其變更提交至共用Git分支，讓其他開發人員在變更前先提取變更。

## RDE指令行工具指令 {#rde-cli-commands}

### 說明/一般資訊 {#help}

* 如需命令清單，請輸入：

  `aio aem:rde`

* 如需命令的詳細說明，請輸入：

  `aio aem rde <command> --help`


### 全域旗標 {#global-flags}

>[!NOTE]
>
> 這些全域旗標尚未開放使用。 這些功能將於6月推出。
> 

* 對於較不詳細的輸出，請使用安靜標幟：

  `aio aem rde <command> --quiet`

  這會移除某些元素，例如旋轉器及進度列，並限制使用者輸入的需求。

* 對於JSON，請使用以下json旗標，而非主控台記錄輸出：

  `aio aem rde <command> --json`

  在隱藏任何主控台輸出時，這會傳回有效的JSON。 請參閱下方的JSON範例。

* 若要避免使用設定指令或任何aio設定建立來設定RDE連線資訊，請使用組織、程式和環境這三個旗標：

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  這仍需要 ```aio login``` 將執行。

### 部署至RDE {#deploying-to-rde}

本節說明如何使用RDE CLI來部署、安裝或更新套件組合、OSGI設定、內容套件、個別內容檔案以及Apache或Dispatcher設定。

一般使用模式為 `aio aem:rde:install <artifact>`.

您可以找到下列一些範例：

<u>部署內容封裝</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的回應如下所示：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

您可以選擇參考遠端存放庫：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

依預設，成品會同時部署至製作層級和發佈層級，但「 — s」標幟可用於鎖定特定層級。

可以部署任何AEM套件，例如包含程式碼、內容或 [容器封裝](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （也稱為「全」套件）。

>[!IMPORTANT]
>
>WKND專案的Dispatcher設定不會透過上述內容套件安裝進行部署。 依照「部署Apache/Dispatcher設定」步驟單獨部署。

<u>部署OSGI設定</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

成功部署的回應類似於以下內容：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署套件組合</u>

若要部署套件組合，請使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

成功部署的回應類似於以下內容：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署內容檔案</u>

若要部署內容檔案，請使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

成功部署的回應類似於以下內容：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher設定</u>

對於此型別的設定，整個資料夾結構必須採用zip檔案的形式。

從 `dispatcher` AEM專案的模組，您可以透過執行以下maven命令來壓縮Dispatcher設定：

`mvn clean package`

或使用以下的zip命令： `src` 目錄 `dispatcher` 模組：

`zip -y -r dispatcher.zip .`

然後使用此命令部署設定：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假設您正在部署 [WKND](https://github.com/adobe/aem-guides-wknd) 專案的Dispatcher設定。 請務必取代 `X.X.X` 具有對應的WKND專案版本編號，或您的專案特定版本編號。

>[!NOTE]
>
>RDE支援「彈性模式」Dispatcher設定，但不支援「舊版模式」Dispatcher設定。 另請參閱 [Dispatcher檔案](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以取得這兩種模式的相關資訊。 您也可以參閱以下檔案： [移轉至彈性模式](/help/implementing/dispatcher/validation-debug.md#migrating)，如果尚未這麼做的話。

成功的部署會產生類似下列的回應：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的程式碼不會通過Cloud Manager管道及其相關品質閘道。 不過，程式碼確實會進行一些分析，這會回報錯誤，如下面的程式碼範例所示：

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

上述程式碼範例說明套件無法解析時的行為。 在此情況下，會將其設為「暫存」，且僅當透過安裝其他程式碼滿足其需求（在此情況下為缺少匯入）時才會安裝。

### 根據網站主題和網站範本部署前端計畫碼 {#deploying-themes-to-rde}

RDE支援的前端程式碼，根據 [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md) 和 [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md). 使用RDE時，這是使用命令列指令來部署前端套件完成的，而不是使用Cloud Manager [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) 用於其他環境型別。

照常使用npm建立您的前端套件：

`npm run build`

應該會產生 `dist/` 資料夾，所以您的前端封裝資料夾應包含 `package.json` 檔案和 `dist` 資料夾：

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
現在您已準備好透過指向前端封裝資料夾來將前端封裝部署到RDE：

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

或者，您也可以壓縮 `package.json` 檔案和 `dist` 資料夾並部署該zip檔案：

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>前端套件中檔案的命名必須符合下列命名慣例：
> * 「dist」資料夾，用於npm build輸出封裝資料夾
> * 「package.json」檔案，用於npm相依性套件

>[!TIP]
>
> 如果您在2023年4月之前建立RDE，並在首次嘗試前端功能時遇到「UNEXPECTED_API_ERROR」錯誤，請嘗試刪除您的環境，然後再次建立。

### 檢查RDE的狀態 {#checking-rde-status}

您可以使用RDE CLI來檢查環境是否已準備好要部署到，以及已透過RDE外掛程式進行了哪些部署。

執行中：

`aio aem:rde:status`

傳回下列專案：

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

如果命令傳回執行個體部署的相關備註，您仍可執行下一次更新，但您的最後一次更新可能尚未在執行個體上顯示。

### 顯示部署歷史記錄 {#show-deployment-history}

您可以透過執行以下動作來檢查建置到RDE的歷史記錄：

`aio aem:rde:history`

這會傳回以下格式的回應：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 從RDE刪除 {#deleting-from-rde}

您可以透過CLI工具刪除先前部署至RDE的組態和組合。 使用 `status` 可刪除專案清單的指令，包括 `bsn` 適用於套件組合和 `pid` 供設定在delete指令中參照。

例如，如果 `com.adobe.granite.demo.MyServlet.cfg.json` 已安裝， `bsn` 只是 `com.adobe.granite.demo.MyServlet`，不使用 **cfg.json** 尾碼。

不支援刪除內容套件或內容檔案。 若要移除它們，RDE應該重設，這會使其回到預設狀態。

如需更多詳細資訊，請參閱下列範例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

如需詳細資訊和示範，請參閱教學課程影片 [如何使用RDE指令(10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html).

## 記錄 {#rde-logging}

>[!NOTE]
>
> 此功能尚無法使用。 它將在六月的某個時候推出。
> 

與其他環境型別類似，記錄層級可以透過修改OSGi設定來設定，儘管如上所述，RDE的部署模型涉及命令列而不是Cloud Manager部署。 檢查 [記錄檔案](/help/implementing/developing/introduction/logging.md) 如需如何檢視、下載和解讀記錄檔的詳細資訊。

RDE CLI也有自己的記錄命令，可用來快速設定應該記錄哪些類別和套裝軟體，以及記錄層級。 這些設定可以視為短暫，因為它們不會修改版本控制中的OSGI屬性。 此功能著重於即時追蹤記錄，而非查詢遙遠的過去記錄。

以下範例說明如何追蹤製作層，其中一個套件設定為偵錯記錄層級，而兩個套件（以空格分隔）設定為資訊偵錯層級。 包含 **驗證** 套件會醒目提示。

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

另請參閱 `aio aem:rde:logs --help` 以取得完整的命令列選項。

功能包含：

* 根據每個套件或類別層級聲明記錄層級
* 自訂記錄輸出格式
* 最多追蹤四個目前的記錄設定，每個設定都在自己的終端機中
* 醒目提示特定記錄

請注意，記錄檔儲存在RDE的記憶體中，這些記錄檔會被回收，因此若未尾隨或網路速度太慢，則會加以捨棄。


## 重設 {#reset-rde}

重設RDE會移除製作和發佈執行個體中的所有自訂程式碼、設定和內容。 例如，如果已使用RDE測試特定功能，而且您想要將其重設為預設狀態，以便測試不同功能時，此重設會很有用。

重設會將RDE設定為最新可用的AEM版本。

<!-- Alexandru: hiding for now, do not delete

Resetting can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code is deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role to use the reset feature. If not, a reset action results in an error.

### Reset the RDE by way of Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

您可以使用Cloud Manager以下列步驟重設您的RDE：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要重設RDE的方案。

1. 在「**概觀**」頁面，按一下畫面頂端的「**環境**」索引標籤。

   ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，按一下「**環境**」卡上的「**全部顯示**」按鈕直接跳到「**環境**」索引標籤。

     ![顯示全部選項](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 此 **環境** 視窗會開啟並列出該計畫的所有環境。

   ![環境索引標籤](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 按一下要重設之RDE的省略符號按鈕，然後選取 **重設**.

   ![檢視環境詳細資訊](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 按一下「 」，確認您要重設RDE **重設** 在對話方塊中。

   ![確認重設](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager會透過橫幅通知來確認重設程式已開始。

   ![重設橫幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重設程式啟動後，通常需要幾分鐘才能完成並將環境恢復為預設狀態。 您可以隨時在檢視重設程式的狀態 **狀態** 的欄 **環境** 卡片或 **環境** 視窗。

![RDE重設狀態](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您也可以使用省略符號按鈕直接從重設RDE **環境** 卡在上 **概觀** 頁面。

![從環境卡重設RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有關如何使用Cloud Manager來管理您的環境的詳細資訊，請參閱 [Cloud Manager檔案](/help/implementing/cloud-manager/manage-environments.md).

## 支援JSON輸出的命令 {#json-commands}

>[!NOTE]
>
> 這些命令尚無法使用。 這些功能將於6月推出。
> 

大部分的命令都支援全域 ```--json``` 此旗標會隱藏主控台輸出，並傳回要在指令碼中處理的有效json。 以下是一些支援的命令，以及json輸出的範例。

### 狀態

<details>
  <summary>展開以檢視狀態範例</summary>

#### 乾淨的RDE

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### 具有某些已安裝套件組合的RDE

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```
</details>

### 安裝

<details>
  <summary>展開以檢視安裝範例</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```
</details>

### 刪除

<details>
  <summary>展開以檢視刪除範例</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### 記錄

<details>
  <summary>展開以檢視歷史記錄範例</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```
</details>

### 重設

<details>
  <summary>展開以檢視重設範例</summary>

#### 開火，忘記，不等待

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### 等待完成

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```
</details>

### 重新啟動

<details>
  <summary>展開以檢視重新啟動範例</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## 執行模式 {#runmodes}

您可以在資料夾名稱上使用尾碼來套用RDE特定的OSGI設定，如以下範例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

請參閱 [執行模式檔案](/help/implementing/deploying/overview.md#runmodes) 以取得關於執行模式的一般資訊。

>[!NOTE]
>
>RDE OSGI設定是唯一的，因為它會繼承套件所宣告的任何OSGI屬性的值。 `dev` 執行模式。

RDE與其他環境不同，因為其內容可安裝在/apps下的install.rde資料夾（或install.author.rde或install.publish.rde）中。 這可讓您使用命令列工具將內容提交到Git並傳遞給RDE。

## 填入內容 {#populating-content}

重設RDE時，會移除所有內容，因此如有需要，必須執行明確動作以新增內容。 作為最佳實務，請考慮組裝一組內容以用作在RDE中驗證或偵錯功能的測試內容。 有幾種可能的策略可將該內容填入RDE：

1. 使用命令列工具將內容套件明確同步至RDE

1. 將範例內容放入/apps下的install.rde資料夾內並提交Git中，然後使用命令列工具將整體內容套件同步到RDE。

1. 使用 [內容複製工具](/help/implementing/developing/tools/content-copy.md) 從prod、stage或dev環境或其他RDE複製已定義的內容集。

1. 使用封裝管理員

同步內容套件時，限製為1 GB。


## RDE與雲端開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在許多方面與雲端開發環境類似，但在架構上有一些細微的差異，可讓程式碼快速同步。 將計畫碼傳入RDE的機制不同 — 對於RDE，一個會從本機開發環境同步計畫碼，而對於Cloud開發環境，一個會透過Cloud Manager部署計畫碼。

基於這些原因，建議您在RDE環境中驗證程式碼後，使用非生產管道將程式碼部署到雲端開發環境。 最後，請在使用生產管道部署之前測試程式碼。

另請注意下列考量事項：

* RDE不包含預覽層
* RDE目前不支援發行前通道。


## 我需要多少RDE？ {#how-many-rds-do-i-need}

RDE可用於每個已授權的解決方案，而Adobe也提供其他RDE，這些可授權用於生產（非沙箱）計畫。

所需的RDE數目取決於組織的組成與處理。 最靈活的模式是組織為每位AEM Cloud Service開發人員購買專屬的RDE。 在此模型中，每個開發人員都可以在RDE上測試其程式碼，而無需與其他團隊成員就RDE環境是否可用進行協調。

在另一個極端，擁有單一RDE的團隊可能會使用內部流程來協調哪些開發人員可以在給定時間使用環境。 這有可能是當開發人員達到中繼功能里程碑，並準備好在雲端環境中進行驗證時，他們可以快速進行所需的變更。

中間模型是指組織購買多個RDE，因此更有可能獲得未使用的RDE。 一種策略可能是針對每個Scrum團隊或主要功能分配RDE。 內部流程可用於協調環境的使用。

## AEM FormsCloud Service快速開發環境(RDE)與其他環境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms開發人員可以使用AEM FormsCloud Service快速開發環境來快速開發最適化Forms、工作流程和自訂專案，例如自訂核心元件、與協力廠商系統的整合等。 AEM FormsCloud Service快速開發環境(RDE)不支援通訊API。 也不支援需要記錄檔案的功能，例如在提交最適化表單時產生記錄檔案。 下列的AEM Forms功能不適用於快速開發環境(RDE)：

* 設定最適化表單的記錄檔案
* 在提交最適化表單時或透過工作流程步驟產生記錄檔案
* 使用電子郵件提交動作或工作流程中的電子郵件步驟將記錄檔案作為附件傳送
* 在最適化表單或工作流程步驟中使用Adobe Sign
* 通訊API

>[!NOTE]
>
> 快速開發環境(RDE)的UI與Forms的其他Cloud Service環境之間沒有差異。 所有與記錄檔案相關的選項（例如為最適化表單選擇記錄檔案範本）會持續出現在UI中。 這些環境沒有通訊API和記錄檔案功能來測試這些選項。 因此，當您選擇需要通訊API或記錄檔案功能的任何選項時，不會執行任何動作，且會顯示錯誤訊息。

## rde教學課程

若要瞭解AEMas a Cloud Service中的RDE，請參閱示範的教學影片 [如何設定、使用及開發生命週期(01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html).

# 疑難排解

## aio RDE外掛程式 {#aio-rde-plugin}

### 有關許可權不足的錯誤

若要使用RDE外掛程式，您必須是Cloud Manager的成員 **開發人員 — Cloud Service** 產品設定檔。 另請參閱 [此頁面](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 以取得更多詳細資料。

或者，如果您可以透過執行此命令登入開發人員主控台，則可以確認您擁有此開發人員角色：

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>如果您看到 `Warning: cloudmanager:* is not a aio command.` 錯誤，您必須安裝 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 透過執行以下命令：
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

執行以驗證登入是否成功完成

`aio cloudmanager:list-programs`

這應該列出您設定之組織下的所有計畫，並確認您已指派正確的角色。
