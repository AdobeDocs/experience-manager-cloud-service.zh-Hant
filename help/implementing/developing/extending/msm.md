---
title: 擴充多網站管理員
description: 了解如何擴充多網站管理員的功能。
exl-id: 4b7a23c3-65d1-4784-9dea-32fcceca37d1
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2336'
ht-degree: 92%

---

# 擴充多網站管理員 {#extending-the-multi-site-manager}

本文件會協助您了解如何擴充多網站管理員的功能，並介紹下列主題。

* 了解 MSM Java API 的主要成員
* 建立可用於推出設定中的全新同步動作
* 修改預設的語言和國家/地區代碼

>[!TIP]
>
>在檔案[重複使用內容：多網站管理員](/help/sites-cloud/administering/msm/overview.md)的內容中，更容易理解此頁面。

>[!CAUTION]
>
>編寫網站內容時會使用多網站管理員及其 API，因此僅適用於作者環境。

## Java API 的概觀 {#overview-of-the-java-api}

多網站管理由以下套件組成：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要 MSM API 物件互動方式如下 (另請參閱[「使用的術語」](/help/sites-cloud/administering/msm/overview.md#terms-used)一節)：

![主要 MSM API 物件](assets/msm-api-interaction.png)

* **`Blueprint`**- `Blueprint` (如[藍圖設定](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)中所示) 會指定 Live Copy 可以繼承內容的頁面。

  ![藍圖](assets/msm-blueprint-interaction.png)

   * 藍圖設定 (`Blueprint`) 的使用為選用，但是：

      * 這可讓作者使用來源上的「**推出**」選項，將修改內容明確地推送到繼承自此來源的 Live Copy。
      * 這讓作者可使用「**建立網站**」，使用者因此可以輕鬆地選取語言並設定 Live Copy 的結構。
      * 它會定義任何合成的 Live Copy 的預設推出設定。

* **`LiveRelationship`**- `LiveRelationship` 會指定 Live Copy 分支中的資源與其同等來源/藍圖資源之間的連結 (關係)。

   * 實現繼承和推出時會使用此關係。
   * `LiveRelationship` 物件會針對和該關係相關之推出設定 (`RolloutConfig`)、`LiveCopy` 以及 `LiveStatus` 物件提供存取 (參照)。

   * 例如，在 `/content/copy/us` (來自 `/content/wknd/language-masters` 的來源/藍圖) 中會建立 Live Copy。 資源 `/content/wknd/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 會建立關係。

* **`LiveCopy`**- `LiveCopy` 會保存 Live Copy 資源與其來源/藍圖資源之間關係 (`LiveRelationship`) 的設定詳細資料。

   * 使用 `LiveCopy` 類別存取頁面的路徑、來源/藍圖頁面的路徑、推出設定，而子頁面是否也包含在 `LiveCopy` 中。

   * `LiveCopy` 節點會在每次使用「**建立網站**」或者「**建立 Live Copy**」時建立。

* **`LiveStatus`** - `LiveStatus` 物件會提供對 `LiveRelationship` 的執行階段狀態的存取。 用於查詢 Live Copy 的同步狀態。

* **`LiveAction`** - `LiveAction` 是指在推出中所包含的每個資源上執行的動作。

   * `LiveAction` 只會由 `RolloutConfig` 產生。

* **`LiveActionFactory`** - `LiveActionFactory` 會建立 `LiveAction` 物件 (如果是 `LiveAction` 設定)。設定會在存放庫中儲存為資源。

* **`RolloutConfig`** - `RolloutConfig` 會保存 `LiveActions` 清單，以便在觸發時使用。`LiveCopy` 會繼承 `RolloutConfig`，而結果會在 `LiveRelationship` 中顯示。

   * 第一次設定 Live Copy 還會使用 `RolloutConfig` (這會觸發 `LiveAction`)。

## 建立新的同步動作 {#creating-a-new-synchronization-action}

您可以建立自訂的同步動作，以搭配您的推出設定一起使用。[安裝的動作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions)不符合您的特定應用程式需求時，這可能派得上用場。

為此，請建立兩個類別：

* 執行動作的 [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 介面的實作。
* 實作 [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 介面並建立您 `LiveAction` 類別的執行個體之 OSGi 元件

`LiveActionFactory` 會針對以下特定設定建立 `LiveAction` 類別的執行個體：

* `LiveAction` 類別會包括以下方法：

   * `getName` - 傳回動作的名稱

      * 此名稱是用來參照動作，例如在轉出設定中。

   * `execute` - 執行動作的任務

* `LiveActionFactory` 類別會包括以下項目：

   * `LIVE_ACTION_NAME` - 包含相關聯 `LiveAction` 的名稱之欄位

      * 此名稱必須和由 `getName` 方法 (屬於 `LiveAction` 類別) 傳回的值相符。

   * `createAction` - 建立 `LiveAction` 的執行個體

      * 選用的 `Resource` 參數可用於提供設定資訊。

   * `createsAction` - 傳回相關聯 `LiveAction` 的名稱

### 存取 LiveAction 設定節點 {#accessing-the-liveaction-configuration-node}

使用存放庫中的 `LiveAction` 設定節點，以儲存會影響 `LiveAction` 執行個體執行階段行為的資訊。儲存 `LiveAction` 設定的存放庫中的節點可用於執行階段時的 `LiveActionFactory` 物件。因此，您可以對設定節點新增屬性，且必要時在您的 `LiveActionFactory` 實作中使用這些屬性。

例如，`LiveAction`必須儲存Blueprint作者的名稱。 設定節點的屬性包括儲存該資訊的藍圖頁面屬性名稱。在執行階段時，`LiveAction` 會從設定中擷取屬性名稱，然後獲取屬性值。

[`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法的參數是一種 `Resource` 物件。此 `Resource` 物件在推出設定中代表這項即時動作的 `cq:LiveSyncAction` 節點。

如需詳細資訊，請參閱[建立轉出設定](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration)。

和平常一樣，使用設定節點時，您應該將其調整為 `ValueMap` 物件：

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### 存取目標節點、來源節點和 LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

下列物件會以 `LiveAction` 物件之 `execute` 方法的參數提供：

* 代表 Live Copy 來源的 [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) 物件
* 代表 Live Copy 目標的 `Resource` 物件。
* Live Copy 的 [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 物件
   * `autoSave` 值表示您的 `LiveAction` 是否應該儲存對存放庫所做的變更
   * `reset` 值表示推出重設模式。

您可以從這些物件取得有關`LiveCopy`的資訊。 您還可以使用 `Resource` 物件獲取 `ResourceResolver`、`Session` 和 `Node` 物件。這些物件對於操作存放庫內容非常有用：

在以下程式碼的第一行中，來源是指來源頁面的 `Resource` 物件：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource` 引數可能是 `null` 或者 `Resources` 物件 (不適應於 `Node` 物件，例如 [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 物件)。

## 建立新的推出設定 {#creating-a-new-rollout-configuration}

安裝的推出設定不符合您的應用程式需求時，您可以透過以下兩個步驟建立推出設定：

* [建立推出設定](#create-the-rollout-configuration)
* [將同步動作新增到推出設定中](#add-synchronization-actions-to-the-rollout-configuration)

然後，在藍圖或 Live Copy 頁面上設定推出設定時，您即可使用新的推出設定。

>[!TIP]
>
>另請參閱「[自訂推出的最佳做法](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts)」。

### 建立「推出設定」 {#create-the-rollout-configuration}

若要建立轉出設定：

1. 在 `https://<host>:<port>/crx/de` 開啟 CRXDE Lite。

1. 導覽至 `/apps/msm/<your-project>/rolloutconfigs` (您的專案的 `/libs/msm/wcm/rolloutconfigs` 自訂版本)。

   * 如果這是您的第一個設定，則必須將此 `/libs` 分支用為範本，以便在 `/apps` 下面建立新分支。

1. 在此位置下，建立一個具有以下屬性的節點：

   * **名稱**：轉出設定的節點名稱，例如`contentCopy`或`workflow`
   * **類型**：`cq:RolloutConfig`

1. 將以下屬性新增至此節點：

   * **名稱**：`jcr:title`
     **類型**：`String`
     **值**：會在 UI 中顯示的識別標題

   * **名稱**：`jcr:description`
     **類型**：`String`
     **值**：選用的說明。

   * **名稱**：`cq:trigger`
     **類型**：`String`
     **值**：所要使用的[推出觸發器](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers)
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下&#x200B;**「儲存全部」**。

### 將「同步動作」新增到「推出設定」中 {#add-synchronization-actions-to-the-rollout-configuration}

推出設定會儲存在您已在 `/apps/msm/<your-project>/rolloutconfigs` 節點下建立的[推出設定節點](#create-the-rollout-configuration)下方。

新增類型 `cq:LiveSyncAction` 的子節點，以將同步動作新增到推出設定中。同步動作節點的順序會決定動作發生的順序。

1. 在CRXDE Lite中，選取您的[轉出設定](#create-the-rollout-configuration)節點，例如`/apps/msm/myproject/rolloutconfigs/myrolloutconfig`。

1. 建立具有下列節點屬性的節點：

   * **名稱**：同步動作的節點名稱
      * 此名稱必須和在[同步動作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions)下的資料表中的&#x200B;**動作名稱**&#x200B;相同，例如 `contentCopy` 或是 `workflow`。
   * **類型**：`cq:LiveSyncAction`

1. 依您需要的數量新增並設定同步動作節點。

1. 重新排列動作節點，使其顯示的順序和您希望它們出現的順序相符。
   * 最頂端的動作節點會先出現。

## 建立並使用簡單的 LiveActionFactory 類別 {#creating-and-using-a-simple-liveactionfactory-class}

依照本節中說明的程序開發一個 `LiveActionFactory` 並用於推出設定中。此程序會使用 Maven 和 Eclipse 來開發和部署 `LiveActionFactory`：

1. [建立 maven 專案](#create-the-maven-project)並將其匯入到 Eclipse 中。
1. [新增相依性](#add-dependencies-to-the-pom-file)到 POM 檔案。
1. [實作 `LiveActionFactory` 介面](#implement-liveactionfactory)並部署 OSGi 套件組合。
1. [建立推出設定](#create-the-example-rollout-configuration)。
1. [建立 Live Copy](#create-the-live-copy)。

[Maven 專案和 Java 類別的原始碼](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)可在公用 Git 存放庫中取得。

### 建立 Maven 專案 {#create-the-maven-project}

以下程序會要求您已將 `adobe-public` 設定檔新增到您的 Maven 設定檔案中。

* 如需 adobe-public 設定檔的資訊，請參閱[獲取內容套件 Maven 外掛程式](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* 如需 Maven 設定檔案的資訊，請參閱 Maven [設定參考](https://maven.apache.org/settings.html)。

1. 開啟終端機或命令列工作階段，並將目錄變更為指向建立專案的位置。
1. 輸入以下命令：

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示處指定下列值：

   * **`groupId`**: `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. 啟動Eclipse並[匯入Maven專案](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)。

### 新增相依性到 POM 檔案 {#add-dependencies-to-the-pom-file}

新增相依性，以便 Eclipse 編譯器可以參照在 `LiveActionFactory` 程式碼中使用的類別。

1. 從 Eclipse 專案總管開啟檔案 `MyLiveActionFactory/pom.xml`。

1. 在編輯器中，按一下 `pom.xml` 索引標籤並找到 `project/dependencyManagement/dependencies` 區段。

1. 在 `dependencyManagement` 元素裡面新增以下 XML，然後儲存檔案。

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. 從&#x200B;**專案總管** (在 `MyLiveActionFactory-bundle/pom.xml`) 開啟套件組合的 POM 檔案。

1. 在編輯器中，按一下 `pom.xml` 索引標籤並找到「專案/相依性」區段。在相依性元素裡面新增以下 XML，然後儲存檔案：

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### 實作 LiveActionFactory {#implement-liveactionfactory}

以下 `LiveActionFactory` 類別會實作一項 `LiveAction`，這會記錄來源和目標頁面的訊息，並將 `cq:lastModifiedBy` 屬性從來源節點複製到目標節點。即時動作的名稱為 `exampleLiveAction`。

1. 在Eclipse專案總管中，用滑鼠右鍵按一下`MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm`封裝，然後按一下&#x200B;**新增** > **類別**。

1. 對於&#x200B;**名稱**，請輸入 `ExampleLiveActionFactory` 然後按一下「**完成**」。

1. 開啟 `ExampleLiveActionFactory.java` 檔案，將內容更換為以下程式碼，然後儲存檔案。

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. 使用終端機或命令工作階段，將目錄變更為 `MyLiveActionFactory` 目錄 (Maven 專案目錄)。然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM `error.log` 檔案應該會指出套件組合已啟動，並顯示在 `https://<host>:<port>/system/console/status-slinglogs` 的紀錄中。

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立推出設定範例 {#create-the-example-rollout-configuration}

建立使用您所建立 `LiveActionFactory` 的 MSM 推出設定：

1. 建立並設定[使用標準程序的推出設定](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration)，並使用屬性：

   * **標題**：推出設定範例
   * **名稱**：examplerolloutconfig
   * **cq:trigger**： `publish`

### 將即時動作新增到推出設定範例中 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在前一個程序中建立的推出設定，以便該設定使用 `ExampleLiveActionFactory` 類別。

1. 開啟 CRXDE Lite。

1. 在 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content` 下面建立以下節點：

   * **名稱**：`exampleLiveAction`
   * **類型**：`cq:LiveSyncAction`

1. 按一下&#x200B;**「儲存全部」**。

1. 選取 `exampleLiveAction` 節點並新增屬性，以便對 `ExampleLiveAction` 類別顯示 `cq:LastModifiedBy` 屬性應該從來源複製到目標節點。

   * **名稱**：`repLastModBy`
   * **類型**：`Boolean`
   * **值**：`true`

1. 按一下&#x200B;**「儲存全部」**。

### 建立 Live Copy {#create-the-live-copy}

使用您的以下設定[建立 Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) (WKND 參考網站的英文/產品分支)：

* **來源**：`/content/wknd/language-masters/en/products`

* **推出設定**：推出設定範例

啟動來源分支的&#x200B;**產品** (英文) 頁面並觀察 `LiveAction` 類別所產生的紀錄訊息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## 變更語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

AEM 會使用一組預設的語言和國家/地區代碼。

* 預設的語言代碼根據 ISO-639-1 定義的兩個字母小寫代碼。
* 預設的國家/地區代碼是根據 ISO 3166 定義的兩個字母小寫或大寫代碼。

MSM 會使用儲存的語言和國家/地區代碼清單來確定和頁面語言版本名稱相關聯的國家/地區名稱。您可以視需要變更清單的下列方面：

* 語言標題
* 國家/地區名稱
* 語言的預設國家/地區 (例如 `en`、`de` 等代碼)

語言清單會儲存在 `/libs/wcm/core/resources/languages` 節點下方。每個子節點即代表一種語言或一種語言國家：

* 節點的名稱為語言代碼 (例如 `en` 或 `de`)，或「語言_國家」代碼 (例如 `en_us` 或 `de_ch`)。

* 節點的 `language` 屬性會儲存代碼語言的完整名稱。
* 節點的 `country` 屬性會儲存代碼國家/地區的完整名稱。
* 當節點名稱僅包含語言代碼時 (例如 `en`)，國家/地區屬性為 `*`，會有額外的 `defaultCountry` 屬性儲存語言-國家/地區的代碼，以顯示要使用的國家/地區。

![語言定義](assets/msm-language-manager.png)

若要修改語言：

1. 開啟 CRXDE Lite。
1. 選取 `/apps` 資料夾並按一下&#x200B;**「建立」**，然後再按一下&#x200B;**「建立資料夾」。**

1. 命名新資料夾`wcm`。

1. 重複上一個步驟以建立 `/apps/wcm/core` 資料夾樹狀結構。在稱之為 `resources` 的 `core` 中建立類型 `sling:Folder` 的節點。

1. 在 `/libs/wcm/core/resources/languages` 節點上按一下右鍵，然後按一下「**複製**」。
1. 在 `/apps/wcm/core/resources` 資料夾上按一下右鍵，然後按一下「**貼上**」。根據需要修改子節點。
1. 按一下&#x200B;**「儲存全部」**。
1. 按一下「**工具**」、「**操作**」，然後再按一下「**Web 主控台**」。在此主控台上，按一下 **OSGi**，然後按一下「**設定**」。
1. 找到並按一下 **Day CQ WCM 語言管理員**，然後將&#x200B;**語言清單**&#x200B;的值變更為 `/apps/wcm/core/resources/languages`，然後再按一下「**儲存**」。

   ![Day CQ WCM 語言管理員](assets/msm-language-manager.png)

## 在頁面屬性上設定 MSM 鎖 {#configuring-msm-locks-on-page-properties}

建立自訂頁面屬性時，您可能需要考慮新屬性是否適合推出到任何 Live Copy。

例如，如果正要新增兩個新的頁面屬性：

* 連絡人電子郵件：

   * 此屬性不需要推出，因為每個國家/地區（或品牌等）都有不同。

* 索引鍵視覺樣式：

   * 專案要求是推出此屬性，因為此屬性（通常）對所有國家/地區（或品牌等）都是通用的。

那麼您需要確保：

* 連絡人電子郵件：

   * 從推出的屬性中排除。
   * 如需詳細資訊，請參閱[設定即時副本同步處理](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)。

* 索引鍵視覺樣式：

   * 確保除非取消繼承，否則您無權編輯此屬性。
   * 還要確保您接著可以恢復繼承。按一下可切換以顯示連線狀態的鏈/斷裂鍊連結，即可控制此功能。

頁面屬性是否需要推出，以及因此在編輯時是否需要取消/恢復繼承，會由對話框屬性控制：

* `cq-msm-lockable`

   * 這會在對話框中建立鍊連結符號。
   * 這只有在取消繼承 (鏈連結斷裂) 時才允許編輯。
   * 這僅適用於資源的第一個子層級
      * **類型**：`String`
      * **值**：持有考慮中的屬性名稱，並相當於屬性 `name` 的值
         * 如需範例，請參閱
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

若已定義 `cq-msm-lockable`，則毀損/關閉鏈會以下列方式和 MSM 互動：

* 如果 `cq-msm-lockable` 的值為：

   * **相對值** (例如，`myProperty` 或是 `./myProperty`)

      * 毀損鏈會從 `cq:propertyInheritanceCancelled` 新增和移除屬性。

   * **絕對值** (例如，`/image`)

      * 毀損鏈會將 `cq:LiveSyncCancelled` 混合新增到 `./image`，並將 `cq:isCancelledForChildren` 設定為 `true`，使得繼承取消。

      * 關閉鏈會回復繼承。

>[!NOTE]
>
>`cq-msm-lockable` 適用於要編輯的資源的第一個子層級，並且無論將該值定義為絕對值或是相對值，它在任何更深入的上階層級上都不起作用。

>[!NOTE]
>
>重新啟用繼承時，Live Copy 頁面屬性不會和來源屬性自動同步。如有需要，您可以手動要求同步。
