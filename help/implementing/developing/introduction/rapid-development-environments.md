---
title: 快速開發環境
description: 瞭解如何使用快速開發環境在雲端環境中進行快速開發反複專案。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: eb87467b1cd3338a409c2aeded74b3bb38d2e58c
workflow-type: tm+mt
source-wordcount: '5446'
ht-degree: 3%

---

# 快速開發環境 {#rapid-development-environments}

若要部署變更，目前的雲端開發環境需要使用採用廣泛程式碼安全性和品質規則（稱為CI/CD管道）的程式。 對於需要快速反複變更的情況，Adobe已推出快速開發環境（簡稱RDE）。

RDE可讓開發人員快速部署和檢閱變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

在RDE中測試變更後，可以透過Cloud Manager管道將其部署到一般雲端開發環境。

開發環境和快速開發環境應僅限於開發、錯誤分析和功能測試，且不應設計為處理高工作負載或大量內容。

>[!NOTE]
> 快速開發環境應該限制在開發、錯誤分析和功能測試，並且不是為了處理高工作負載或大量內容而設計的。

>[!NOTE]
> 與RDE開發人員聯絡Adobe的[不和諧頻道](https://discord.com/channels/1131492224371277874/1245304281184079872)。 歡迎您針對RDE主題提出任何問題或給予回饋。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以看到其他示範[如何設定](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup)、[如何使用它](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use)以及使用RDE的[開發生命週期](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle)的影片。

## 簡介 {#introduction}

RDE可用於程式碼、內容以及Apache或Dispatcher設定。 不像一般的雲端開發環境，開發人員可以使用本機命令列工具，將本機建置的程式碼同步到RDE。

每個方案都布建了RDE。 如果存在沙箱帳戶，則會在不使用數小時後休眠。

建立後，RDE會設定為最新可用的Adobe Experience Manager (AEM)版本。 RDE重設(可使用Cloud Manager執行)會循環RDE並將其設定為最新可用的AEM版本。

通常，單一開發人員在指定時間會使用RDE來測試和偵錯特定功能。 當開發工作階段完成時，RDE可以重設為預設狀態以供下次使用。

其他RDE可授權用於生產（非沙箱）計畫。

## 在程式中啟用RDE {#enabling-rde-in-a-program}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要新增RDE的計畫以顯示其詳細資訊。

   * RDE可新增至[沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)和[生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。

1. 從&#x200B;**計畫總覽**&#x200B;頁面，在&#x200B;**環境**&#x200B;卡片上按一下&#x200B;**新增環境**。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

     ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在「**新增環境**」對話框中，執行下列操作：

   * 在&#x200B;**選取環境型別**&#x200B;標題下選取&#x200B;**快速開發**。
      * 可用/已使用環境的數量會顯示在環境型別後面的括弧中。
   * 提供環境的&#x200B;**名稱**。
   * 為環境提供選用的&#x200B;**描述**。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

**總覽**&#x200B;畫面現在會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。

建立後，RDE會設定為最新可用的AEM版本。 RDE重設(也可以使用Cloud Manager執行)會循環RDE並將其設定為最新可用的AEM版本。

如需有關使用Cloud Manager建立環境、管理誰有權存取環境以及指派自訂網域的詳細資訊，請參閱Cloud Manager檔案中的[程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

## 安裝RDE命令列工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager為程式新增RDE後，您可以透過設定命令列工具與其互動，如以下步驟所述：

>[!IMPORTANT]
>
>請確定您已為Adobe I/O (AIO) CLI和相關外掛程式安裝[的](https://nodejs.org/en/download/)節點和NPM版本20，以便正常運作。


1. 依照此[程式](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/tools/cli-install)安裝AIO CLI工具。
1. 安裝AIO CLI工具AEM RDE外掛程式：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 使用Adobe I/O (AIO)使用者端登入。

   ```
   aio login
   ```

   登入資訊（代號）儲存在全域aio設定中，因此僅支援一個登入和組織。 如果您想要使用需要不同登入或組織的多個RDE，請遵循以下範例來介紹內容。

   <details><summary>請依照此範例為其中一個RDE登入設定本機內容</summary>
   若要將登入資訊本機儲存在特定內容目前目錄的'.aio'檔案中，請執行下列步驟。 設定上下文也是設定CI/CD環境或指令碼的聰明方法。  若要使用此功能，請確定至少使用aio-cli 10.3.1版。請使用'npm install -g @adobe/aio-cli'進行更新。

   現在，在呼叫登入命令之前，先建立名為m`ycontext`的前後關聯（您使用auth外掛程式設定為預設的前後關聯）。

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > 包含`--no-open`選項的登入命令會在終端機中輸出URL，而不是開啟預設瀏覽器。 您可以使用瀏覽器的&#x200B;**無痕視窗**&#x200B;來複製並開啟它。 此功能可確保主瀏覽器視窗中的目前工作階段不受影響，讓您以工作所需的特定帳戶和組織登入。

   第一個命令會在您的本機`mycontext`組態檔中建立新的登入內容組態，稱為`.aio` （視需要建立檔案）。 第二個命令會將內容`mycontext`設定為「目前」內容；亦即預設值。

   設定好此組態後，登入命令會自動將登入權杖儲存在內容`mycontext`中，因此可保持其本機狀態。

   將本機設定儲存在多個資料夾中，即可管理多個內容。 或者，也可以在單一組態檔案中設定多個前後關聯，並透過變更「目前」前後關聯在它們之間切換。
   </details>

1. 設定RDE外掛程式以使用您的組織、程式和環境。 以下的設定指令會以互動方式為使用者提供其組織中的程式清單，並顯示該程式中可供選擇的RDE環境。

   ```
   aio aem:rde:setup
   ```

   如果您使用指令碼式環境，則可跳過設定步驟。 在這種情況下，請直接在每個命令中包含組織、程式和環境值。 [如需詳細資訊，請參閱下面的RDE命令](#rde-cli-commands)。

### 互動式設定 {#installing-the-rde-command-line-tools-interactive}

setup指令會詢問所提供的組態應儲存在本機還是全域。

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

選擇`no`以

* 在您的aio設定中，將組織、計畫和環境全域儲存。
* 僅適用於單一RDE。

選擇`yes`以執行下列動作：

* 將組織、程式和環境儲存在目前目錄的本機`.aio`檔案中。 如果您想要將檔案提交至版本控制，讓其他複製Git存放庫的人可以使用此檔案，此方法相當方便。
* 能夠使用許多RDE，因此切換至其他目錄時會改用該組態。
* 在程式化前後關聯中使用組態，例如可參照它的指令碼。


選取本機或全域組態後，setup命令會嘗試從您目前的登入讀取組織id，然後讀取組織的程式。 如果找不到組織，您可以手動輸入，並附上一些指引。

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

擷取程式後，使用者可以從清單中選取，也可以鍵入以進行篩選。 選取方案時，會列出可供選擇的RDE環境清單。 如果只有一個程式，或只有一個RDE環境可用，或兩者都可用，則會自動選取它。

若要檢視目前的環境內容，請執行下列動作：

```aio aem rde setup --show```

指令會以類似下列的結果回應：

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### 在非互動式環境中手動設定程式 {#manual-setup}

在任何使用者無法以互動方式執行設定命令（例如CI/CD或指令碼）的環境中，都需要手動設定。 您可以使用以下步驟設定組織、方案和環境引數。


<details>
  <summary>展開以尋找有關如何手動設定的詳細資訊</summary>

1. 設定組織ID，並將英數字串取代為您自己的組織ID。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * 您可以使用[檢視您的組織ID](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)下記錄的方法查詢您自己的組織ID。

1. 接下來，設定您的程式ID：

   `aio config:set cloudmanager_programid 12345`

1. 然後，設定要附加RDE的環境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 完成外掛程式的設定後，請透過執行

   `aio login`

   這些步驟需要您成為Cloud Manager **開發人員 — Cloud Service**&#x200B;產品設定檔的成員。 檢視[將團隊成員指派給Cloud Manager產品設定檔 — 指派開發人員產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)以取得詳細資訊。

如需詳細資訊和示範，請觀看教學課程影片[如何設定RDE (06:24)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup)。
</details>

## 開發新功能時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用下列工作流程來開發新功能：

* 當達到中繼里程碑並成功透過AEM as a Cloud Service SDK在本機驗證時，請將程式碼提交到Git功能分支。 雖然提交至Git是選用專案，但分支不應是主行的一部分。 構成「中繼里程碑」的要素因團隊習慣而異。 範例包括幾行程式碼、半天工作或完成子功能。

* 如果另一個功能已使用RDE，而且您要[將它重設為預設狀態](#reset-rde)，請重設它。 <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->重設需要幾分鐘的時間，而且所有現有內容和程式碼都會被刪除。 您可以使用RDE狀態指令來確認RDE已就緒。 RDE會隨附最新的AEM發行版本。

  >[!IMPORTANT]
  >
  >如果您的測試和生產環境未收到自動的AEM版本更新，並且落後於最新版本，則RDE可能會執行其他版本的AEM。 因此，RDE中的程式碼行為可能不符合其在中繼和生產中的運作方式。 在這種情況下，將程式碼部署到生產環境之前，務必要先在中繼環境上執行徹底的測試。


* 使用RDE命令列介面，將本機程式碼同步至RDE。 您可以安裝各種型別的檔案，包括：

   * 內容封裝
   * 特定組合
   * OSGi設定檔案
   * 內容檔案
   * 包含Apache/Dispatcher設定的ZIP檔案

  也可以參考遠端內容套件。 如需詳細資訊，請參閱[RDE命令列工具](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands)。 您可以使用status命令來驗證部署是否成功。 或者，使用封裝管理員來安裝內容封裝。

* 在RDE中測試程式碼。 在Cloud Manager中可以使用作者和發佈URL。

* 如果程式碼的行為與預期不符，請使用標準偵錯技巧來瞭解問題並做出適當的變更。 無須將程式碼修改提交至Git （因為這些修改尚未經過驗證），請使用本機CLI將程式碼同步至RDE。 持續反複運算，直到問題解決為止。

* 程式碼如預期運作後，將程式碼提交到Git功能分支。

* 同步至RDE的程式碼不會使用Cloud Manager管道，因此現在應使用Cloud Manager非生產管道，將Git功能分支部署到雲端開發環境。 此程式會驗證程式碼是否通過Cloud Manager品質門檻，並讓您放心稍後會使用Cloud Manager生產管道成功部署程式碼。

* 對每個中繼里程碑重複上述步驟，直到功能的所有程式碼準備就緒為止，並在RDE和雲端開發環境中正常運作。

* 透過Cloud Manager生產管道將程式碼部署到生產環境。

## 使用RDE來偵錯現有功能 {#use-rde-to-debug-an-existing-feature}

工作流程類似於開發新功能。 差異在於同步至RDE的程式碼會反映推送至發生問題之環境的Git標籤。 此工作流程有助於確保在調查或重製問題時的一致性。 此外，部署符合上游環境的內容可能會有幫助。 此方法可透過匯出和匯入內容套件來達成。

## 多位開發人員在同一個RDE上共同作業 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支援一個專案。 由於程式碼會從本機開發環境同步至RDE環境，因此對於一個開發人員而言，在指定時間自行使用程式碼是最自然的事情。

不過，只要仔細協調，多位開發人員就能驗證特定功能或偵錯特定問題。 關鍵是每個開發人員將其本機專案保持同步，以便其他開發人員吸收特定開發人員所做的程式碼變更。 否則，某位開發人員可能會不慎覆寫其他開發人員的程式碼。 建議的策略是讓每位開發人員在同步至RDE前，將其變更提交至共用的Git分支，讓其他開發人員在變更前先提取變更。

## RDE指令行工具指令 {#rde-cli-commands}

### 說明/一般資訊 {#help}

* 如需命令清單，請輸入：

  `aio aem:rde`

* 如需命令的詳細說明，請輸入：

  `aio aem rde <command> --help`

### 全域旗標 {#global-flags}

* 對於較不詳細的輸出，請使用安靜標幟：

  `aio aem rde <command> --quiet`

  此標幟會移除某些元素，例如旋轉軸和進度列，並限制使用者輸入的需求。

* 對於JSON，請使用以下json旗標，而非主控台記錄輸出：

  `aio aem rde <command> --json`

  抑制任何主控台輸出時，此旗標會傳回有效的JSON。 請參閱下方的JSON範例。

* 若要避免使用設定指令或任何aio設定建立來設定RDE連線資訊，請使用組織、程式和環境這三個旗標：

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  需要執行```aio login```。

### 部署至RDE {#deploying-to-rde}

本節說明如何使用RDE CLI來部署、安裝或更新各種資源。 這些資源包括：

* 內容封裝
* OSGi 設定
* 組合
* 內容檔案
* Apache或Dispatcher設定

一般使用模式為`aio aem:rde:install <artifact>`。

您可以找到下列一些範例：

#### 部署內容封裝 {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的回應如下所示：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

您可以選擇參考遠端存放庫：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

依預設，成品會同時部署至製作與發佈階層，但`-s`旗標可用於鎖定特定階層。

可以部署任何AEM套件，例如包含程式碼、內容的套件或[容器套件](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （也稱為「全」套件）。

>[!IMPORTANT]
>
>上述內容套件安裝不會為WKND專案部署Dispatcher設定。 依照「部署Apache/Dispatcher設定」步驟單獨部署。

#### 部署OSGI設定 {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

成功部署的回應類似於以下內容：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### 部署套件組合 {#deploy-bundle}

若要部署套件組合，請使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

成功部署的回應類似於以下內容：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### 部署內容檔案 {#deploy-content-file}

若要部署內容檔案，請使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

成功部署的回應類似於以下內容：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### 部署Apache/Dispatcher設定 {#deploy-apache-config}

對於此型別的設定，整個資料夾結構必須採用zip檔案的形式。

從AEM專案的`dispatcher`模組，您可以透過執行以下maven命令來壓縮Dispatcher設定：

`mvn clean package`

或從`src`模組的`dispatcher`目錄使用下列zip命令：

`zip -y -r dispatcher.zip .`

然後使用此命令部署設定：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假設您正在部署[WKND](https://github.com/adobe/aem-guides-wknd)專案的Dispatcher設定。 部署專案的Dispatcher設定時，請務必以對應的WKND專案版本號碼或專案特定版本號碼取代`X.X.X`。

>[!NOTE]
>
>RDE支援「彈性模式」Dispatcher設定，但無法支援「舊版模式」Dispatcher設定。 如需這兩種模式的詳細資訊，請參閱[Dispatcher檔案](/help/implementing/dispatcher/disp-overview.md#validation-debug)。 您也可以參閱有關[移轉至Flexible模式](/help/implementing/dispatcher/validation-debug.md#migrating)的檔案（如果尚未這樣做）。

成功的部署會產生類似下列的回應：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署至RDE的計畫碼不會通過Cloud Manager管道及其相關品質閘道。 不過，程式碼確實會進行一些分析，這會回報錯誤，如下面的程式碼範例所示：

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

#### 部署設定管道相關設定（yaml設定） {#deploy-config-pipeline}

在[使用設定管道](/help/operations/config-pipeline.md)一文中說明的環境特定設定（一或多個yaml檔案）可以部署如下：

`aio aem:rde:install -t env-config ./my-config-folder`
其中`my-config-folder`是包含yaml設定的上層資料夾。

或者，您也可以安裝包含設定資料夾樹狀結構的zip檔案：

`aio aem:rde:install -t env-config config.zip`

請注意，yaml檔案的envTypes陣列包含值`rde`，如下列範例所示：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### 根據網站主題和網站範本部署前端計畫碼 {#deploying-themes-to-rde}

RDE支援使用[網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)和[網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)建置的前端程式碼。 RDE不使用像其他環境型別一樣的Cloud Manager [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)，而是使用命令列指令來部署前端套件。

照常使用npm建立您的前端套件：

`npm run build`

它會產生`dist/`資料夾，所以您的前端封裝資料夾包含`package.json`檔案和`dist`資料夾：

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```

現在，您可以透過以下方式指向前端套件資料夾，將前端套件部署到RDE：

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

或者，您可以壓縮`package.json`檔案和`dist`資料夾，並部署該zip檔案：

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
>
> * `dist`資料夾，用於npm組建輸出封裝資料夾
> * `package.json`檔案，用於npm相依性套件

>[!TIP]
>
>如果您在2023年4月之前建立RDE，並且在首次使用前端功能時遇到`UNEXPECTED_API_ERROR`，可能是由於設定過時。 若要解決此問題，請刪除環境並建立新環境。

### 檢查RDE的狀態 {#checking-rde-status}

您可以使用RDE CLI來檢查環境是否已準備好要部署到，以及已透過RDE外掛程式進行了哪些部署。

執行下列動作：

`aio aem:rde:status`

傳回以下內容：

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

您可以使用CLI工具來刪除先前部署至RDE的組態和組合。 使用`status`命令以取得可刪除專案的清單，包括要在刪除命令中參考的套件組合的`bsn`和設定的`pid`。

例如，如果已安裝`com.adobe.granite.demo.MyServlet.cfg.json`，則`bsn`只是`com.adobe.granite.demo.MyServlet`，沒有&#x200B;**cfg.json**&#x200B;尾碼。

不支援刪除內容套件或內容檔案。 若要移除它們，請重設RDE，使其回到預設狀態。

如需更多詳細資訊，請參閱下列範例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

如需詳細資訊和示範，請參閱教學影片[如何使用RDE命令(10:01)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use)。


## 從外部Git提供者部署至RDE {#deploy-to-rde}

>[!NOTE]
>
>此功能可透過Beta程式取得。 如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[CloudManager_BYOG@adobe.com](mailto:cloudmanager_byog@adobe.com)。 請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。

使用[自備Git (BYOG)設定](/help/implementing/cloud-manager/managing-code/external-repositories.md)時，Cloud Manager支援直接從外部Git提供者將程式碼部署到RDE。

從外部Git存放庫部署到RDE需要下列專案：

* 使用與Cloud Manager （BYOG設定）整合的外部Git存放庫。
* 您的專案必須布建一或多個RDE環境。
* 如果您使用`github.com`，則必須檢閱並接受更新的GitHub應用程式安裝，以授與必要的新許可權。

**使用說明**

* 目前僅支援AEM內容和Dispatcher套件部署至RDE。
* 尚不支援部署其他套件型別(例如完整的AEM應用程式套件)。
* 目前不支援使用註解重設RDE環境。 您必須改用現有的AIO CLI重設命令，如[此處所述](/help/implementing/developing/introduction/rapid-development-environments.md#reset-the-rde-command-line)。

**運作方式**

1. **程式碼品質驗證訊息。**

   當提取請求(PR)觸發程式碼品質管道執行時，驗證結果會指出部署能否繼續前往RDE環境。

   在GitHub Enterprise上的外觀：
   GitHub Enterprise上的![程式碼品質驗證訊息](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   在GitLab上的外觀：
   GitLab上的![程式碼品質驗證訊息](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   在Bitbucket上的外觀：
   位元貯體![上的](/help/implementing/developing/introduction/assets/rde-bitbucket-code-quality-validation-message.png)程式碼品質驗證訊息

1. **使用註解觸發部署。**

   若要啟動部署，請以下列格式將註解新增至PR： `deploy on rde-environment-<envName>`

   ![使用註解觸發部署](/help/implementing/developing/introduction/assets/rde-trigger-deployment-using-comment.png)

   `<envName>`必須符合現有RDE環境的名稱。 如果找不到名稱，則會傳回指出環境無效的註解。

   如果環境狀態尚未就緒，您會收到以下註解：

   ![環境未準備好部署](/help/implementing/developing/introduction/assets/rde-environment-not-ready.png)

1. **環境檢查和成品部署。**

   如果RDE準備就緒，Cloud Manager會張貼新支票給PR。

   在GitHub Enterprise上的外觀：

   GitHub上的![環境狀態](/help/implementing/developing/introduction/assets/rde-github-environment-status-is-ready.png)

   在GitLab上的外觀：

   GitLab上的![環境狀態](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-1.png)

   在Bitbucket上的外觀：

   ![位元貯體上的環境狀態](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-1.png)

1. **部署訊息成功。**

   部署完成時，Cloud Manager會張貼成功訊息，概述部署至目標環境的成品。

   在GitHub Enterprise上的外觀：

   GitHub上環境的![部署狀態](/help/implementing/developing/introduction/assets/rde-github-environment-deployed-artifacts.png)

   在GitLab上的外觀：

   ![GitLab上環境的部署狀態](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-2.png)

   在Bitbucket上的外觀：

   ![位元貯體上環境的部署狀態](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-2.png)




## 記錄 {#rde-logging}

與其他環境型別類似，記錄層級可透過修改OSGi設定來設定，不過如上所述，RDE的部署模型涉及命令列而非Cloud Manager部署。 請檢視[記錄檔案](/help/implementing/developing/introduction/logging.md)，以取得如何檢視、下載及解譯記錄的詳細資訊。

RDE CLI也有自己的記錄命令，可用來快速設定記錄哪些類別和套裝程式，以及記錄層級。 這些設定可以視為短暫，因為它們不會修改版本控制中的OSGI屬性。 此功能著重於即時追蹤記錄，而非查詢遙遠的過去記錄。

以下範例說明如何追蹤製作層，其中一個套件設定為偵錯記錄層級，而兩個套件（以空格分隔）設定為資訊偵錯層級。 包含&#x200B;**驗證**&#x200B;封裝的輸出會反白顯示。

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>如果您在播放作者服務的記錄檔命令時看到錯誤`RDECLI:UNEXPECTED_API_ERROR`，請重設您的環境，然後再試一次。 如果您的最新重設作業是在2024年5月底之前，則會擲回此錯誤。
>
>```
>aio aem:rde:reset
>```

如需完整的命令列選項集，請參閱`aio aem:rde:logs --help`。

功能包括：

* 根據每個套件或類別層級聲明記錄層級
* 自訂記錄輸出格式
* 最多追蹤四個目前的記錄設定，每個設定都在自己的終端機中
* 醒目提示特定記錄

請注意，記錄檔儲存在RDE的記憶體中，這些記錄檔會被回收，因此若未尾隨或網路速度太慢，則會加以捨棄。


## 重設RDE {#reset-rde}

重設RDE會移除製作和發佈執行個體中的所有自訂程式碼、設定和內容。 當您完成一項功能的測試並想要在測試另一項功能之前將環境恢復為預設狀態時，重設RDE會很有幫助。

重設會將RDE設定為最新可用的AEM版本。

您可以使用[Cloud Manager](#reset-the-rde-cloud-manager)或[命令列](#reset-the-rde-command-line)重設RDE。 重設需要幾分鐘的時間，而且所有現有內容和程式碼都會從RDE中刪除。

>[!NOTE]
>
>使用重設功能之前，請確定您已獲派Cloud Manager開發人員角色。 否則，重設動作會因錯誤而失敗。

### 使用命令列重設RDE {#reset-the-rde-command-line}

您可以執行下列動作，重設RDE並將其恢復為預設狀態：

`aio aem:rde:reset`

此程式通常需要幾分鐘的時間，並在成功時報告```Environment reset.```或報告錯誤```Failed to reset the environment.```。 如需結構化輸出，請參閱以下有關```--json```輸出的章節。

使用[status命令](#checking-rde-status)來檢查環境何時再次準備就緒。

### 在Cloud Manager中重設RDE {#reset-the-rde-cloud-manager}

您可以使用Cloud Manager來重設RDE，步驟如下：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要重設RDE的方案。

1. 在「**概觀**」頁面，按一下畫面頂端的「**環境**」索引標籤。

   ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，按一下「**環境**」卡上的「**全部顯示**」按鈕直接跳到「**環境**」索引標籤。

     ![顯示全部選項](/help/implementing/cloud-manager/assets/environment-showall.png)

1. **環境**&#x200B;視窗會開啟並列出程式的所有環境。

   ![環境索引標籤](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 按一下要重設之RDE的省略符號按鈕，然後選取&#x200B;**重設**。

   ![檢視環境詳細資訊](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 按一下對話方塊中的&#x200B;**重設**，確認您要重設RDE。

   ![確認重設](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager會透過橫幅通知確認重設程式已開始。

   ![重設橫幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重設開始後，通常需要幾分鐘才能完成並將環境還原成預設狀態。 您隨時可以在&#x200B;**環境**&#x200B;卡片或視窗的&#x200B;**狀態**&#x200B;欄中檢視重設狀態。

![RDE重設狀態](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您也可以直接從&#x200B;**總覽**&#x200B;頁面上的&#x200B;**環境**&#x200B;卡片中使用省略符號按鈕來重設RDE。

![從環境卡重設RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

如需有關如何使用Cloud Manager管理環境的詳細資訊，請參閱[Cloud Manager檔案](/help/implementing/cloud-manager/manage-environments.md)。

## 支援JSON輸出的命令 {#json-commands}

大多數命令支援全域```--json```旗標，該旗標會隱藏主控台輸出，並傳回要在指令碼中處理的有效json。 以下是一些支援的命令，以及json輸出的範例。

### 狀態 {#status}

<details>
  <summary>展開以檢視狀態範例</summary>

#### 乾淨的RDE {#clean-rde}

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

#### 具有某些已安裝套件組合的RDE {#rde-installed-bundles}

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

### 安裝 {#install}

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

### 刪除 {#delete}

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

### 歷史記錄 {#history}

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

### 重設 {#reset}

<details>
  <summary>展開以檢視重設範例</summary>

#### 開火，忘記，不等待 {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### 等待完成，已成功重設 {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### 等候完成，重設失敗 {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
}
```

</details>

### 重新啟動 {#restart}

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

如需有關執行模式的一般資訊，請參閱[執行模式檔案](/help/implementing/deploying/overview.md#runmodes)。

>[!NOTE]
>
>RDE OSGI組態是唯一的，因為它會繼承套件組合的`dev`執行模式所宣告的任何OSGI屬性的值。

RDE與其他環境不同，因為內容可以安裝在`install.rde`下的`install.author.rde`資料夾（或`install.publish.rde`或`/apps`）中。 此功能可讓您使用命令列工具將內容提交到Git並將其傳遞到RDE。

## 填入內容 {#populating-content}

重設RDE時，會移除所有內容，因此如有需要，必須執行明確動作以新增內容。 作為最佳實務，請考慮組裝一組內容以用作在RDE中驗證或偵錯功能的測試內容。 有幾種可能的策略可將該內容填入RDE：

1. 使用命令列工具將內容套件明確同步至RDE

1. 將範例內容放入`install.rde`下的`/apps`資料夾內並提交Git中，然後使用命令列工具將整體內容套件同步到RDE。

1. 使用[內容複製工具](/help/implementing/developing/tools/content-copy.md)，從生產、階段或開發環境或其他RDE複製已定義的內容集。

1. 使用封裝管理員

同步內容套件時，限製為1 GB。


## RDE與雲端開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在許多方面與雲端開發環境類似，但在架構上有一些細微的差異，可讓程式碼快速同步。 將程式碼傳入RDE的機制不同 — 對於RDE，一個會從本機開發環境同步程式碼，而對於雲端開發環境，則會透過Cloud Manager部署程式碼。

基於這些原因，建議您在RDE環境中驗證程式碼後，使用非生產管道將程式碼部署到雲端開發環境。 最後，請在使用生產管道部署之前測試程式碼。

另請注意下列考量事項：

* RDE不包含預覽層
* RDE目前不支援發行前通道。


## 我需要多少RDE？ {#how-many-rds-do-i-need}

RDE可用於每個已授權的解決方案，Adobe也提供其他RDE，這些可授權用於生產（非沙箱）計畫。

所需的RDE數目取決於組織的組成與處理。 最靈活的模式是組織為每位AEM Cloud Service開發人員購買專屬的RDE。 在此模型中，每個開發人員都可以在RDE上測試他們的計畫碼，而無需與其他團隊成員協調是否有RDE環境可用。

在另一個極端，只有一個RDE的團隊可能會依賴內部協調，以決定哪些開發人員在給定時間使用環境。 當開發人員達到功能里程碑，且需要在雲端環境中驗證其工作，並有彈性進行快速變更時，此方法即可正常運作。

中間模型是指組織購買多個RDE，因此更有可能獲得未使用的RDE。 一種策略可能是針對每個Scrum團隊或主要功能分配RDE。 內部流程可用於協調環境的使用。

## AEM Forms Cloud Service RDE與其他環境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms開發人員可使用AEM Forms Cloud Service快速開發環境來快速開發最適化Forms、工作流程和自訂專案，例如自訂核心元件、與協力廠商系統的整合等。 AEM Forms Cloud Service快速開發環境(RDE)不支援通訊API。 也不支援需要記錄檔案的功能，例如在提交最適化表單時產生記錄檔案。 下列的AEM Forms功能不適用於快速開發環境(RDE)：

* 設定最適化表單的記錄檔案
* 在提交最適化表單時或透過工作流程步驟產生記錄檔案
* 使用電子郵件提交動作或工作流程中的電子郵件步驟將記錄檔案作為附件傳送
* 在最適化表單或工作流程步驟中使用Adobe Sign
* 通訊API

>[!NOTE]
>
> 快速開發環境(RDE)的UI與Forms的其他Cloud Service環境之間沒有差異。 所有與記錄檔案相關的選項（例如為最適化表單選擇記錄檔案範本）會持續出現在UI中。 這些環境沒有通訊API和記錄檔案功能來測試這些選項。 因此，如果您選擇需要通訊API或記錄檔案功能的選項，系統不會執行動作。 相反地，它會顯示錯誤訊息。

## rde教學課程

若要瞭解AEM as a Cloud Service中的RDE，請觀看示範[如何設定、如何使用以及開發生命週期(01:25)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/developing/rde/overview)的影片教學課程。

## 疑難排解 {#troubleshooting}

### 疑難排解RDE (#rde-troublehooting)

#### 如何取得現有RDE適用的最新AEM版本 {#get-latest-aem-version}

建立後，RDE會設定為最新可用的Adobe Experience Manager (AEM)版本。 可以使用Cloud Manager或[命令執行的](#reset-rde)RDE重設`aio aem:rde:reset`會循環RDE並將其設定為最新可用的AEM版本。

### 疑難排解aio RDE外掛程式 {#aio-rde-plugin-troubleshooting}

#### 有關許可權不足的錯誤 {#insufficient-permissions}

若要使用RDE外掛程式，您必須是Cloud Manager **開發人員 — Cloud Service**&#x200B;產品設定檔的成員。 檢視[將團隊成員指派給Cloud Manager產品設定檔 — 指派開發人員產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)以取得詳細資訊。

或者，如果您透過執行以下命令登入開發人員主控台，則可以確認您具有此開發人員角色：

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>如果看到`Warning: cloudmanager:* is not a aio command.`錯誤，您必須執行下列命令以安裝[aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)：
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

執行下列動作，驗證登入是否成功完成：

`aio cloudmanager:list-programs`

此程式會列出您設定之組織下的所有程式，並確認您已指派正確的角色。

#### 使用已棄用的內容`aio-cli-plugin-cloudmanager` {#aio-rde-plugin-troubleshooting-deprecatedcontext}

由於`aio-cli-plugin-aem-rde`的歷程記錄，內容名稱`aio-cli-plugin-cloudmanager`已使用一段時間。 RDE外掛程式現在會使用IMS方法管理內容資訊，讓您以全域或本機方式儲存內容。 您也可以設定預設內容，以自動套用至所有AIO呼叫。 設定的預設前後關聯儲存在本機，可讓開發人員追蹤及使用資料夾內的個別前後關聯及其資訊。 如需詳細資訊，請閱讀[以上設定本機內容的範例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)。

同時使用外掛程式、`aio-cli-plugin-cloudmanager`和`aio-cli-plugin-aem-rde`且想要將所有資訊儲存在相同內容的開發人員，現在必須選擇下列選項：

##### 繼續使用內容`aio-cli-plugin-cloudmanager`

內容仍可使用。 RDE外掛程式中會顯示棄用警告。 使用```--quiet```模式可省略此警告。 較新版本的RDE外掛程式不再提供用於讀取內容`aio-cli-plugin-cloudmanager`的遞補功能。 若要繼續使用，只需將預設內容設定為`aio-cli-plugin-cloudmanager`即可。 請參閱[以上設定本機內容](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)的範例。

##### 將任何其他內容名稱也用於Cloud Manager外掛程式

Cloud Manager外掛程式提供引數，可定義要使用的內容。 目前尚不支援IMS預設內容設定。 若要這麼做，請使用[範例設定RDE外掛程式以設定本機內容](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)，並告訴Cloud Manager外掛程式在每次呼叫它時都使用`myContext` （例如```--imsContextName=myContext```）。
