---
title: 快速開發環境
description: 瞭解如何利用快速開發環境在雲環境中快速開發迭代。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: 5bfa5a1df940b8903acd08f4c3cb7443adb897d8
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 5%

---

# 快速開發環境 {#rapid-development-environments}

為了部署更改，當前雲開發環境需要使用採用廣泛代碼安全和質量規則的流程，稱為CI/CD管道。 對於需要快速、反複更改的情況，Adobe引入了快速開發環境（簡稱RDE）。

RDE允許開發人員快速部署和審查更改，從而最大限度地減少test經過驗證可以在本地開發環境中工作的功能所需的時間。

在RDE中測試更改後，可以通過Cloud Manager管道將其部署到常規雲開發環境中。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以參閱其他視頻演示 [如何設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)。 [如何使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)的 [開發生命週期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) 使用RDE。

## 簡介 {#introduction}

RDE可用於代碼、內容和Apache或Dispatcher配置。 與常規雲開發環境不同，開發人員可以使用本地命令行工具將本地構建的代碼同步到RDE。

每個程式都配有RDE。 對於沙盒帳戶，在幾小時不使用後它們將被休眠。

建立時，RDE將設定為最新可用AEM版本。 RDE重置（可使用雲管理器執行）將循環RDE並將其設定為最新可用AEM版本。

通常，RDE將由單個開發人員在指定時間用於測試和調試特定功能。 完成開發會話後，RDE可重置為預設狀態以用於下次使用。

可以為生產（非沙盒）程式授予其他RDE許可。

## 在程式中啟用RDE {#enabling-rde-in-a-program}

按照以下步驟使用Cloud Manager為程式建立RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要添加RDE的程式以顯示其詳細資訊。

   * RDE可添加到兩者 [沙盒程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [製作程式。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. 在&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**新增環境**&#x200B;以新增環境。

   ![環境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **新增環境**&#x200B;選項也可在&#x200B;**環境**&#x200B;索引標籤上找到。

      ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 由於缺少權限或根據授權的資源，**新增環境**&#x200B;選項可能會停用。

1. 在出現的&#x200B;**新增環境**&#x200B;對話框中：

   * 選擇 **快速發展** 下 **選擇環境類型** 的子菜單。
      * 可用/已用環境的數量顯示在環境類型後面的括弧中。
   * 提供 **名稱** 環境。
   * 提供可選 **說明** 環境。
   * 選取&#x200B;**雲端區域**。

   ![新增環境對話框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 按一下&#x200B;**儲存**，以新增指定的環境。

現在&#x200B;**總覽**&#x200B;畫面會在&#x200B;**環境**&#x200B;卡中顯示您的新環境。

建立時，RDE將設定為最新可用AEM版本。 RDE重置（也可使用雲管理器執行）將循環RDE並將其設定為最新可用AEM版本。

有關使用雲管理器建立環境、管理誰有權訪問環境以及分配自定義域的詳細資訊，請參閱 [雲管理器文檔。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安裝RDE命令行工具 {#installing-the-rde-command-line-tools}

使用雲管理器為程式添加RDE後，您可以通過設定命令行工具與其進行交互，如以下步驟所述：

>[!IMPORTANT]
>
>確保您有最新版本 [已安裝節點和NPM](https://nodejs.org/en/download/) Adobe I/OCLI和相關插件可正常工作。


1. 按照以下步驟安裝Adobe I/OCLI工具 [這裡](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)。
1. 安裝Adobe I/OCLI工具雲管理器插件，並按說明配置它們 [這裡](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
1. 通過運行以下命AEM令安裝Adobe I/OCLI工具RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 為組織ID配置雲管理器插件：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   並用您自己的組織ID替換字母數字字串，可使用策略查找 [這裡](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)。

1. 接下來，配置程式ID:

   `aio config:set cloudmanager_programid 12345`

1. 然後，配置RDE將附加到的環境ID:

   `aio config:set cloudmanager_environmentid 123456`

1. 配置完插件後，通過執行

   `aio login`

   成功登錄時的響應應與下面的輸出類似，但您可以忽略顯示的值。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   請注意，此步驟要求您成為雲管理器的成員 **開發人員 — Cloud Service** 產品配置檔案。 請參閱 [此頁](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 的子菜單。

   或者，如果可以通過運行以下命令登錄到開發人員控制台，則可以確認您具有此開發人員角色：

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >如果你看到 `Warning: cloudmanager:list-programs is not a aio command.` 錯誤，您需要安裝 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 運行以下命令：
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. 通過運行驗證登錄是否成功完成

   `aio cloudmanager:list-programs`

   這應列出您所配置組織下的所有程式。


有關詳細資訊和演示，請參見 [如何設定RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) 視頻教程。

## 在開發新特徵時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用以下工作流來開發新功能：

* 當使用AEMas a Cloud ServiceSDK到達中間里程碑並在本地成功驗證時，應將代碼提交到尚未成為主行一部分的git功能分支，儘管提交git是可選的。 &quot;中間里程碑&quot;的構成因團隊習慣而異。 示例包括幾行新代碼、半天工作或完成子功能。

* 如果RDE已被其他特徵使用，並且您希望 [將其重置為預設狀態](#reset-rde)。 <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重置將需要幾分鐘時間，所有現有內容和代碼都將被刪除。 可以使用RDE狀態命令確認RDE已就緒。 RDE將提供最新版本AEM。

   >[!IMPORTANT]
   >
   > 如果您的暫存和生產環境未收到自動AEM發佈更新，並且遠遠落後於最新的發AEM布版本，請注意，在RDE上運行的代碼可能與代碼在暫存和生產上的運行方式不匹配。 在這種情況下，在將代碼部署到生產環境之前，對代碼執行徹底的轉移測試尤為重要。


* 使用RDE命令行介面將本地代碼同步到RDE。 選項包括安裝Apache/Dispatcher配置的內容包、特定包、OSGI配置檔案、內容檔案和zip檔案。 也可以引用遠程內容包。 查看 [RDE命令行工具](#rde-cli-commands) 的子菜單。 您可以使用status命令驗證部署是否成功。 （可選）使用包管理器安裝內容包。

* TestRDE中的代碼。 Cloud Manager中提供作者和發佈URL。

* 如果代碼的行為不如預期，請使用標準調試技術來瞭解問題並做出適當的更改。 不將代碼修改提交到git（因為這些修改尚未驗證），請使用本地CLI將代碼同步到RDE。 繼續迭代直到問題解決。

* 一旦代碼按預期的方式運行，將代碼提交到git功能分支。

* 同步到RDE的代碼不使用Cloud Manager管道，因此現在您應使用Cloud Manager非生產管道將git功能分支部署到雲開發環境。 這將驗證代碼是否通過Cloud Manager質量門，並讓您確信稍後將使用Cloud Manager生產管道成功部署代碼。

* 對每個中間里程碑重複上述步驟，直到該功能的所有代碼都準備就緒，並且在RDE和雲開發環境上都運行良好。

* 通過Cloud Manager生產管道將代碼部署到生產環境。

## 使用RDE調試現有特徵 {#use-rde-to-debug-an-existing-feature}

工作流類似於開發新功能。 區別在於，與RDE同步的代碼將反映已推送到發現問題的環境的任何內容的git標籤。 此外，部署與上游環境匹配的內容可能很有用。 這可以通過導出和導入內容包來實現。

## 多個開發人員在同一RDE上協作 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支援單個項目。 由於代碼從本地開發環境同步到RDE環境，因此在給定時間由一個開發人員自己使用代碼是最自然的。

但是，通過謹慎的協調，多個開發人員可以驗證特定功能或調試特定問題。 關鍵是每個開發人員都保持其本地項目的同步，這樣特定開發人員所做的代碼更改就會被其他開發人員吸收，否則某個開發人員可能會無意中覆蓋另一開發人員的代碼。 建議的策略是，每個開發人員在同步到RDE之前將其更改提交到共用的Git分支，以便其他開發人員在進行自己的更改之前先提取更改。

## RDE命令行工具命令 {#rde-cli-commands}

### 幫助/一般資訊 {#help}

* 對於命令清單，鍵入：

   `aio aem:rde`

* 有關命令的詳細幫助，請鍵入：

   `aio aem rde <command> --help`

### 部署到RDE {#deploying-to-rde}

本節介紹使用RDE CLI部署、安裝或更新捆綁包、OSGI配置、內容包、單個內容檔案以及Apache或Dispatcher配置。

一般使用模式是 `aio aem:rde:install <artifact>`。

您可以找到以下一些示例：

<u>部署內容包</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的響應如下所示：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

（可選）您可以引用遠程儲存庫：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

預設情況下，對象會部署到作者層和發佈層，但「 — s」標誌可用於針對特定層。

可以AEM部署任何包，如包含代碼、內容或 [容器包裝](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （也稱為「全部」包）。

>[!IMPORTANT]
>
>WKND項目的調度程式配置未通過上述內容包安裝進行部署。 您需要按照「部署Apache/Dispatcher配置」步驟單獨部署它。

<u>部署OSGI配置</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

其中成功部署的響應如下所示：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署捆綁包</u>

要部署捆綁包，請使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

其中成功部署的響應如下所示：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署內容檔案</u>

要部署內容檔案，請使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

其中成功部署的響應如下所示：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher配置</u>

對於此類配置，整個資料夾結構需要採用zip檔案的形式。

從 `dispatcher` 模組，可AEM以通過運行以下maven命令來壓縮調度程式配置：

`mvn clean package`

或使用以下的zip命令 `src` 目錄 `dispatcher` 模組：

`zip -y -r dispatcher.zip .`

然後，通過以下命令部署配置：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>以上命令假定您正在部署 [WKND](https://github.com/adobe/aem-guides-wknd) 項目的調度程式配置。 請確保替換 `X.X.X` 在部署項目的調度程式配置時使用相應的WKND項目版本號或項目特定的版本號。

>[!NOTE]
>
>RDE支援「靈活模式」調度程式配置，但不支援「傳統模式」調度程式配置。 請參閱 [調度程式文檔](/help/implementing/dispatcher/disp-overview.md#validation-debug) 的子菜單。 您還可以查閱 [遷移到靈活模式](/help/implementing/dispatcher/validation-debug.md#migrating)的雙曲餘切值。

成功部署將生成如下響應：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的代碼不會經歷Cloud Manager管道及其關聯的質量門，但該代碼確實會經過一些分析，這些分析將報告錯誤，如下面的代碼示例所示：

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

上面的代碼示例說明了如果捆綁包未解析，則該行為是「轉移」的，只有在通過安裝其他代碼滿足其要求（在本例中缺少導入）時才會安裝。

### 檢查RDE的狀態 {#checking-rde-status}

您可以使用RDE CLI檢查環境是否已準備好部署到，因為已通過RDE插件進行了哪些部署。

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

如果命令返回有關實例部署的注釋，您仍然可以繼續執行下一次更新，但您的最後一次更新可能尚未在實例上顯示。

### 顯示部署歷史記錄 {#show-deployment-history}

您可以通過運行以下命令來檢查對RDE的部署歷史：

`aio aem:rde:history`

返回以下形式的響應：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 從RDE刪除 {#deleting-from-rde}

您可以通過CLI工具刪除以前部署到RDE的配置和捆綁包。 使用 `status` 命令，列出可刪除的內容，其中包括 `bsn` 用於捆綁和 `pid` 以在delete命令中引用配置。

例如，如果 `com.adobe.granite.demo.MyServlet.cfg.json` 已安裝， `bsn` 只是 `com.adobe.granite.demo.MyServlet`的 **cfg.json** 尾碼。

不支援刪除內容包或內容檔案。 為了刪除它們，應重置RDE，這將使RDE返回預設狀態。

有關詳細資訊，請參閱以下示例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

有關詳細資訊和演示，請參見 [如何使用RDE命令](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) 視頻教程。

## 重設 {#reset-rde}

重置RDE將從作者和發佈實例中刪除所有自定義代碼、配置和內容。 這很有用，例如，如果RDE已用於test特定特徵，並且您希望將其重置為預設狀態以test其他特徵，則可以。

重置將將RDE設定為最新可用AEM版本。

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

您可以通過以下步驟使用Cloud Manager重置RDE:

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 按一下要重置RDE的程式。

1. 在&#x200B;**總覽**&#x200B;頁面，按一下畫面頂端的&#x200B;**環境**&#x200B;索引標籤。

   ![「環境」索引標籤](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，按一下&#x200B;**環境**&#x200B;卡上的&#x200B;**全部顯示**&#x200B;按鈕直接跳到&#x200B;**環境**&#x200B;索引標籤。

      ![顯示全部選項](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 的 **環境** 開啟並列出程式的所有環境。

   ![環境索引標籤](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 按一下要重置的RDE的省略號按鈕，然後選擇 **重置**。

   ![檢視環境詳細資訊](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 通過按一下 **重置** 的子菜單。

   ![確認重置](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. 雲管理器通過標題通知確認重置進程已啟動。

   ![重置標題通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重置過程一旦啟動，通常需要幾分鐘才能完成並將環境返回到其預設狀態。 可以在中的任何時間查看重置進程的狀態 **狀態** 列 **環境** 或 **環境** 的子菜單。

![RDE重置狀態](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

也可以直接從 **環境** 卡 **概述** 的子菜單。

![從環境卡重置RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有關如何使用雲管理器管理環境的詳細資訊，請參閱 [雲管理器文檔。](/help/implementing/cloud-manager/manage-environments.md)

## 執行模式 {#runmodes}

RDE特定的OSGI配置可通過在資料夾名稱上使用尾碼來應用，如下例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

查看 [運行模式文檔](/help/implementing/deploying/overview.md#runmodes) 的子菜單。

>[!NOTE]
>
>RDE OSGI配置是唯一的，因為它繼承了捆綁包聲明的任何OSGI屬性的值 `dev` 運行模式。

RDE與其他環境不同，因為內容可以安裝在/apps下的install.rde資料夾（或install.author.rde或install.publish.rde）中。 這允許您使用命令行工具將內容提交到git並將其提交到RDE。

## 填充內容 {#populating-content}

重置RDE時，所有內容都會被刪除，因此，如果需要，必須採取顯式操作來添加內容。 作為最佳做法，請考慮組裝一組內容，以用作RDE中驗證或調試功能的test內容。 在RDE中填充該內容有幾種可能的策略：

1. 使用命令行工具將內容包顯式同步到RDE

1. 將示例內容放在/apps下的install.rde資料夾中，並提交到git中，然後使用命令行工具將總體內容包同步到RDE。

1. 使用 [內容拷貝工具](/help/implementing/developing/tools/content-copy.md) 從prod、stage或dev環境或從其他RDE復制定義的內容集。

1. 使用包管理器

請注意，同步內容包時，限制為1GB。

## 記錄 {#logging}

可以通過修改OSGi配置來設定日誌級別。 檢查 [文檔](/help/implementing/developing/introduction/logging.md) 的子菜單。

## RDE與雲開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在很多方面與雲開發環境類似，但是為了允許快速同步代碼，RDE還存在一些較小的體系結構差異。 將代碼傳輸到RDE的機制不同 — 對於RDE，一個從本地開發環境中同步代碼，而對於雲開發環境，一個通過雲管理器部署代碼。

出於這些原因，建議在驗證RDE環境上的代碼後，您應使用非生產管道將代碼部署到雲開發環境。 最後，在使用生產流水線部署之前test代碼。

另請注意以下注意事項：

* RDE不包括預覽層
* RDE當前不支援使用Cloud Manager前端管道部署的查看和調試前端代碼。
* RDE當前不支援預發行通道。


## 我需要多少RDE? {#how-many-rds-do-i-need}

RDE適用於每個許可的解決方案，Adobe還提供額外的RDE，這些RDE可用於生產（非沙盒）程式。

需要的RDE數量取決於組織的組成和流程。 最靈活的模型是組織為其每個AEM Cloud Service開發人員購買專用RDE。 在此模型中，每個開發人員都可以在RDE上test其代碼，而無需與其他團隊成員協調RDE環境是否可用。

在另一個極端，具有單個RDE的團隊可以使用內部流程來協調哪些開發人員可以在給定時間使用環境。 這可能是開發人員在達到中間功能里程碑並準備在雲環境中驗證時所做的，在雲環境中他們可以快速進行所需的更改。

中間模型是組織購買多個RDE的模型，因此使用未使用的RDE的可能性更大。 一種策略是分配RDE/scrum團隊或主要功能。 內部進程可用於協調環境的使用。

## AEM FormsCloud Service快速開發環境(RDE)與其他環境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms開發人員可以使用AEM FormsCloud Service快速開發環境快速開發自適應Forms、工作流和定制，如定制核心元件、與第三方系統的整合等。 AEM FormsCloud Service快速開發環境(RDE)不支援通信API以及需要記錄文檔的特性和功能，例如在提交自適應表單時生成記錄文檔。 以下列出的AEM Forms功能在快速開發環境(RDE)中不可用：

* 為自適應表單配置記錄文檔
* 在提交自適應表單或使用工作流步驟時生成記錄文檔
* 將記錄文檔作為附件發送，並在工作流中執行「電子郵件提交」操作或「電子郵件」步驟
* 在自適應表單或工作流步驟中使用Adobe Sign
* 通信API

>[!NOTE]
>
> 快速開發環境(RDE)的UI與Forms的其他Cloud Service環境沒有區別。 所有與「記錄文檔」相關的選項（如為自適應表單選擇記錄模板的文檔）繼續顯示在UI中。 這些環境沒有通信API和記錄文檔功能來test這些選項。 因此，當您選擇需要通信API或記錄文檔功能的任何選項時，不執行任何操作，並且顯示或返回錯誤消息。

## RDE教程

要瞭解RDE在AEMas a Cloud Service中的資訊，請參閱 [視頻教程，演示如何設定它、如何使用它以及開發生命週期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
