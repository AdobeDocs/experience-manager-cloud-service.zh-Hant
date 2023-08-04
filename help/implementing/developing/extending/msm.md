---
title: 擴充多站點管理員
description: 瞭解如何擴充多站點管理員的功能。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---


# 擴充多站點管理員 {#extending-the-multi-site-manager}

本檔案可協助您瞭解如何延伸「多站點管理員」的功能，並涵蓋下列主題。

* 瞭解MSM Java API的主要成員
* 建立可用於轉出設定的新同步化動作
* 修改預設語言和國家/地區代碼

>[!TIP]
>
>在檔案的內容中更容易理解此頁面 [重複使用內容：多網站管理員。](/help/sites-cloud/administering/msm/overview.md)

>[!CAUTION]
>
>多網站管理員及其API用於製作網站，因此僅供製作環境使用。

## Java API概觀 {#overview-of-the-java-api}

「多網站管理」包含下列套件：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要MSM API物件的互動如下（另請參閱一節） [使用的辭彙](/help/sites-cloud/administering/msm/overview.md#terms-used))：

![主要MSM API物件](assets/msm-api-interaction.png)

* **`Blueprint`** - A `Blueprint` （如所示） [Blueprint設定](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations))指定即時副本可以繼承內容的頁面。

  ![藍圖](assets/msm-blueprint-interaction.png)

   * 使用Blueprint設定( `Blueprint`)為選用，但：

      * 它可讓作者使用 **轉出** 選項來明確推送修改至從此來源繼承的即時副本。
      * 它允許作者使用 **建立網站**，可讓使用者輕鬆選取語言並設定即時副本的結構。
      * 它會定義任何結果即時副本的預設轉出設定。

* **`LiveRelationship`** - `LiveRelationship` 指定即時副本分支中的資源與其對等來源/Blueprint資源之間的連線（關係）。

   * 在實作繼承和轉出時會使用這些關係。
   * `LiveRelationship` 物件提供轉出組態的存取（參照） ( `RolloutConfig`)， `LiveCopy`、和 `LiveStatus` 與關係相關的物件。

   * 例如，即時副本建立於 `/content/copy/us` 從來源/Blueprint於 `/content/wknd/language-masters`. 資源 `/content/wknd/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 形成一種關係。

* **`LiveCopy`** - A `LiveCopy` 保留關係的設定詳細資料(`LiveRelationship`)，位於即時副本資源及其來源/Blueprint資源之間。

   * 使用 `LiveCopy` 類別以存取頁面的路徑、來源/Blueprint頁面的路徑、轉出設定以及子頁面是否也包含在 `LiveCopy`.

   * A `LiveCopy` 每次都會建立節點 **建立網站** 或 **建立即時副本** 已使用。

* **`LiveStatus`** - `LiveStatus` 物件可讓您存取的執行階段狀態 `LiveRelationship`. 用於查詢即時副本的同步狀態。

* **`LiveAction`** - A `LiveAction` 是在轉出涉及的每個資源上執行的動作。

   * `LiveAction`s僅由產生 `RolloutConfig`s.

* **`LiveActionFactory`** - A `LiveActionFactory` 建立 `LiveAction` 物件已指定 `LiveAction` 設定。 設定會儲存為存放庫中的資源。

* **`RolloutConfig`** - `RolloutConfig` 儲存清單 `LiveActions`，以便在觸發時使用。 此 `LiveCopy` 會繼承 `RolloutConfig` 而結果會顯示在 `LiveRelationship`.

   * 第一次設定即時副本時也會使用 `RolloutConfig` (會觸發 `LiveAction`s)。

## 建立新同步化動作 {#creating-a-new-synchronization-action}

您可以建立自訂同步動作以與轉出設定一起使用。 這在下列情況下相當實用： [已安裝的動作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) 不符合您特定的應用程式需求。

若要這麼做，請建立兩個類別：

* 的實作 [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 執行此動作的介面。
* 實作的OSGi元件 [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 介面並建立您的執行個體 `LiveAction` 類別

此 `LiveActionFactory` 建立 `LiveAction` 指定設定的類別：

* `LiveAction` 類別包含下列方法：

   * `getName`  — 傳回動作名稱

      * 例如，在轉出設定中，會使用名稱來參照動作。

   * `execute`  — 執行動作的工作

* `LiveActionFactory` 類別包括下列成員：

   * `LIVE_ACTION_NAME`  — 包含關聯欄位名稱的欄位 `LiveAction`

      * 此名稱必須與 `getName` 方法 `LiveAction` 類別。

   * `createAction`  — 建立 `LiveAction`

      * 選填 `Resource` 引數可用來提供設定資訊。

   * `createsAction`  — 傳回關聯專案的名稱 `LiveAction`

### 存取LiveAction設定節點 {#accessing-the-liveaction-configuration-node}

使用 `LiveAction` 存放庫中的設定節點，用於儲存影響執行階段行為的資訊 `LiveAction` 執行個體。 存放庫中儲存 `LiveAction` 組態適用於 `LiveActionFactory` 物件。 因此，您可以將屬性新增至設定節點，並在中使用 `LiveActionFactory` 視需要實施。

例如， `LiveAction` 需要儲存Blueprint作者的名稱。 設定節點的屬性包含儲存資訊的Blueprint頁面的屬性名稱。 在執行階段， `LiveAction` 從設定中擷取屬性名稱，然後取得屬性值。

的引數 [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法是 `Resource` 物件。 這個 `Resource` 物件代表 `cq:LiveSyncAction` 轉出設定中此即時動作的節點。

請參閱檔案 [建立轉出設定](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) 以取得詳細資訊。

如同使用設定節點時一般，您應將其調整為 `ValueMap` 物件：

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

### 存取目標節點、來源節點和LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

下列物件是作為 `execute` 方法 `LiveAction` 物件：

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) 代表即時副本來源的物件
* A `Resource` 代表即時副本目標的物件。
* 此 [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 即時副本的物件
   * 此 `autoSave` 值會指出您的 `LiveAction` 應儲存對存放庫進行的變更
   * 此 `reset` 值表示轉出重設模式。

您可以透過這些物件取得 `LiveCopy`. 您也可以使用 `Resource` 要取得的物件 `ResourceResolver`， `Session`、和 `Node` 物件。 這些物件對於操控存放庫內容很有用：

在以下程式碼的第一行，來源為 `Resource` 來源頁面的物件：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>此 `Resource` 引數可以是 `null` 或 `Resources` 不適應的物件 `Node` 物件，例如 [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 物件。

## 建立新的轉出設定 {#creating-a-new-rollout-configuration}

當安裝的轉出組態不符合您的應用程式需求時，您可以建立轉出組態，請遵循下列兩個步驟：

* [建立轉出設定](#create-the-rollout-configuration)
* [將同步動作新增到轉出設定](#add-synchronization-actions-to-the-rollout-configuration)

然後，當您在Blueprint或即時副本頁面上設定轉出設定時，可以使用新的轉出設定。

>[!TIP]
>
>另請參閱 [自訂轉出的最佳實務](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### 建立轉出設定 {#create-the-rollout-configuration}

若要建立新的轉出設定：

1. 開啟CRXDE Lite於 `https://<host>:<port>/crx/de`.

1. 瀏覽至 `/apps/msm/<your-project>/rolloutconfigs`，您的專案自訂版本的 `/libs/msm/wcm/rolloutconfigs`.

   * 如果這是您的第一個設定，則 `/libs` 分支必須用作範本，才能在下建立新分支 `/apps`.

1. 在此位置下，建立具有以下屬性的節點：

   * **名稱**：轉出設定的節點名稱，例如 `contentCopy` 或 `workflow`
   * **型別**： `cq:RolloutConfig`

1. 將下列屬性新增至此節點：

   * **名稱**: `jcr:title`
     **型別**： `String`
     **值**：將顯示在UI中的識別標題

   * **名稱**: `jcr:description`
     **型別**： `String`
     **值**：選用的說明。

   * **名稱**: `cq:trigger`
     **型別**： `String`
     **值**：此 [轉出觸發器](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) 將使用
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下 **全部儲存**.

### 將同步動作新增至轉出設定 {#add-synchronization-actions-to-the-rollout-configuration}

轉出設定儲存在 [轉出設定節點](#create-the-rollout-configuration) 您已在下建立的 `/apps/msm/<your-project>/rolloutconfigs` 節點。

新增型別的子節點 `cq:LiveSyncAction` 以將同步化動作新增至轉出設定。 同步化動作節點的順序會決定動作發生的順序。

1. 在CRXDE Lite中，選取 [轉出設定](#create-the-rollout-configuration) 節點，例如 `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. 建立具有下列節點屬性的節點：

   * **名稱**：同步動作的節點名稱
      * 名稱必須與 **動作名稱** 在表格中的 [同步化動作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) 例如 `contentCopy` 或 `workflow`.
   * **型別**： `cq:LiveSyncAction`

1. 新增並設定您所需的同步化動作節點數目。

1. 重新排列動作節點，使其順序符合您要動作節點發生的順序。
   * 最上層的動作節點會先出現。

## 建立和使用簡單LiveActionFactory類別 {#creating-and-using-a-simple-liveactionfactory-class}

請依照本節中的程式來開發 `LiveActionFactory` 並用於轉出設定。 程式使用Maven和Eclipse來開發和部署 `LiveActionFactory`：

1. [建立Maven專案](#create-the-maven-project) 並將其匯入Eclipse。
1. [新增相依性](#add-dependencies-to-the-pom-file) 至POM檔案。
1. [實作 `LiveActionFactory` 介面](#implement-liveactionfactory) 並部署OSGi套件組合。
1. [建立轉出設定](#create-the-example-rollout-configuration).
1. [建立即時副本](#create-the-live-copy).

[Maven專案和Java類別的原始碼](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) 可用於公共Git存放庫。

### 建立Maven專案 {#create-the-maven-project}

下列程式要求您已新增 `adobe-public` 設定檔至您的Maven設定檔。

* 如需adobe-public設定檔的相關資訊，請參閱 [取得內容套件Maven外掛程式](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* 如需Maven設定檔案的相關資訊，請參閱Maven [設定參考](https://maven.apache.org/settings.html).

1. 開啟終端機或命令列工作階段，並變更目錄以指向建立專案的位置。
1. 輸入下列命令：

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示時指定下列值：

   * **`groupId`**： `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. 啟動Eclipse和 [匯入Maven專案。](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)

### 將相依性新增至POM檔案 {#add-dependencies-to-the-pom-file}

新增相依性，讓Eclipse編譯器可以參考在 `LiveActionFactory` 程式碼。

1. 從Eclipse專案總管中，開啟檔案 `MyLiveActionFactory/pom.xml`.

1. 在編輯器中，按一下 `pom.xml` 標籤並找到 `project/dependencyManagement/dependencies` 區段。

1. 將下列XML新增至 `dependencyManagement` 元素，然後儲存檔案。

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

1. 從開啟套件組合的POM檔案 **專案總管** 在 `MyLiveActionFactory-bundle/pom.xml`.

1. 在編輯器中，按一下 `pom.xml` 索引標籤並找出專案/相依性區段。 在相依性元素內新增下列XML，然後儲存檔案：

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

### 實作LiveActionFactory {#implement-liveactionfactory}

下列專案 `LiveActionFactory` 類別實作 `LiveAction` 會記錄有關來源和目標頁面的訊息，並複製 `cq:lastModifiedBy` 屬性從來源節點到目標節點。 即時動作的名稱為 `exampleLiveAction`.

1. 在Eclipse專案總管中，以滑鼠右鍵按一下 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 封裝並按一下 **新增** -> **類別**.

1. 對於 **名稱**，輸入 `ExampleLiveActionFactory` 然後按一下 **完成**.

1. 開啟 `ExampleLiveActionFactory.java` 檔案，使用下列程式碼取代內容，然後儲存檔案。

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

1. 使用終端機或命令工作階段，將目錄變更為 `MyLiveActionFactory` 目錄（Maven專案目錄）。 然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM `error.log` 檔案應該會指出該套件組合已啟動，並顯示在的記錄中 `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立轉出設定範例 {#create-the-example-rollout-configuration}

建立使用的MSM轉出設定 `LiveActionFactory` 您所建立的：

1. 建立及設定 [使用標準程式轉出組態](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) 使用屬性：

   * **標題**：轉出設定範例
   * **名稱**： exampleerolloutconfig
   * **cq：trigger**： `publish`

### 將即時動作新增至範例轉出設定 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在前一個程式中建立的轉出組態，使其使用 `ExampleLiveActionFactory` 類別。

1. 開啟CRXDE Lite。

1. 在下建立以下節點 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`：

   * **名稱**: `exampleLiveAction`
   * **型別**： `cq:LiveSyncAction`

1. 按一下 **全部儲存**.

1. 選取 `exampleLiveAction` 節點並新增屬性以向 `ExampleLiveAction` 類別 `cq:LastModifiedBy` 屬性應該從來源復寫到目標節點。

   * **名稱**: `repLastModBy`
   * **型別**： `Boolean`
   * **值**: `true`

1. 按一下 **全部儲存**.

### 建立即時副本 {#create-the-live-copy}

[建立即時副本](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) ，位於WKND參考網站的英文/產品分支中（使用您的轉出設定）：

* **來源**： `/content/wknd/language-masters/en/products`

* **轉出設定**：轉出設定範例

啟動 **產品** （英文）頁面，並觀察以下記錄訊息： `LiveAction` 類別會產生：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## 變更語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

AEM會使用一組預設的語言與國家/地區代碼。

* 預設語言程式碼為ISO-639-1所定義的小寫、雙字母程式碼。
* 預設的國家代碼是小寫或大寫、雙字母的代碼，如ISO 3166所定義。

MSM會使用儲存的語言和國家/地區代碼清單，來判斷與頁面語言版本名稱相關聯的國家/地區名稱。 您可以視需要變更清單的下列方面：

* 語言標題
* 國家/地區名稱
* 語言預設國家/地區（針對下列程式碼） `en`， `de`，等等)

語言清單儲存在 `/libs/wcm/core/resources/languages` 節點。 每個子節點代表一種語言或一個語言國家：

* 節點的名稱是語言代碼(例如 `en` 或 `de`)或language_country程式碼(例如 `en_us` 或 `de_ch`)。

* 此 `language` 節點的屬性會儲存程式碼語言的完整名稱。
* 此 `country` 節點的屬性會儲存程式碼所在國家/地區的完整名稱。
* 當節點名稱僅包含語言代碼(例如 `en`)，country屬性為 `*`，以及另一個 `defaultCountry` 屬性會儲存language-country的程式碼，以指出要使用的國家/地區。

![語言定義](assets/msm-language-manager.png)

若要修改語言：

1. 開啟CRXDE Lite。
1. 選取 `/apps` 資料夾並按一下 **建立**，然後 **建立資料夾。**

1. 命名新資料夾 `wcm`.

1. 重複上一步驟以建立 `/apps/wcm/core` 資料夾樹狀結構。 建立型別節點 `sling:Folder` 在 `core` 已呼叫 `resources`.

1. 用滑鼠右鍵按一下 `/libs/wcm/core/resources/languages` 節點並按一下 **複製**.
1. 用滑鼠右鍵按一下 `/apps/wcm/core/resources` 資料夾並按一下 **貼上**. 視需要修改子節點。
1. 按一下 **全部儲存**.
1. 按一下 **工具**， **作業** 則 **網頁主控台**. 從此主控台按一下 **osgi**，然後 **設定**.
1. 找到並按一下 **Day CQ WCM語言管理員**，並變更的值 **語言清單** 至 `/apps/wcm/core/resources/languages`，然後按一下 **儲存**.

   ![Day CQ WCM語言管理員](assets/msm-language-manager.png)

## 在頁面屬性上設定MSM鎖定 {#configuring-msm-locks-on-page-properties}

建立自訂頁面屬性時，您可能需要考慮新屬性是否應該有資格轉出至任何即時副本。

例如，如果要新增兩個新頁面屬性：

* 連絡人電子郵件:

   * 此屬性不需要推出，因為每個國家/地區（或品牌等）都有不同。

* 關鍵視覺樣式：

   * 專案要求是推出此屬性，因為此屬性（通常）對所有國家/地區（或品牌等）都是通用的。

之後，您需要確保：

* 連絡人電子郵件:

   * 已從轉出屬性中排除。
   * 請參閱檔案 [設定即時副本同步](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) 以取得詳細資訊。

* 關鍵視覺樣式：

   * 請確定除非取消繼承，否則不允許編輯此屬性。
   * 同時也請確定您之後可以恢復繼承。 這可透過按一下切換以指示連線對狀態的鏈/斷鏈連結來控制。

頁面屬性是否應推出（因此在編輯時可能會取消/恢復繼承），由對話方塊屬性控制：

* `cq-msm-lockable`

   * 這會在對話方塊中建立鏈結符號。
   * 僅當取消繼承時（鏈結中斷），才允許編輯。
   * 這僅適用於資源的第一個子層級
      * **型別**： `String`
      * **值**：保留考量中的屬性名稱，且可比較屬性的值 `name`
         * 例如，請參閱
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

時間 `cq-msm-lockable` 已定義，中斷/關閉鏈結將以下列方式與MSM互動：

* 如果 `cq-msm-lockable` 為：

   * **相對** (例如， `myProperty` 或 `./myProperty`)

      * 中斷鏈結將會從新增和移除屬性 `cq:propertyInheritanceCancelled`.

   * **絕對** (例如， `/image`)

      * 中斷鏈結將會透過新增 `cq:LiveSyncCancelled` mixin至 `./image` 和設定 `cq:isCancelledForChildren` 至 `true`.

      * 關閉鏈結將會回覆繼承。

>[!NOTE]
>
>`cq-msm-lockable` 會套用至要編輯之資源的第一個子項層級，且不論值是否定義為絕對或相對，都無法用於任何更深入的層級上階。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與來源屬性同步。 如果需要，您可以手動要求同步。
