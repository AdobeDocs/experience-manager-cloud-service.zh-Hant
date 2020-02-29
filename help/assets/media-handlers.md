---
title: 使用媒體處理常式和工作流程處理資產
description: 瞭解各種媒體處理常式，以及如何在工作流程中使用它們來執行資產上的工作。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# 使用媒體處理常式和工作流程處理資產 {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager(AEM)Assets隨附一組預設工作流程和媒體處理常式，以處理資產。 工作流程會定義要在資產上執行的一般工作，然後將特定工作委派給媒體處理常式，例如縮圖產生或中繼資料擷取。

可以定義工作流程，當特定類型的資產上傳至伺服器時，工作流程會自動執行。 處理步驟是依一系列AEM Assets媒體處理常式來定義。 AEM提供一些內 [建的處理常式](#default-media-handlers) ，其他的處理常式可 [以自訂開發](#creating-a-new-media-handler) ，或借由將程式委派至命令列工 [具來定義](#command-line-based-media-handler)。

媒體處理常式是AEM Assets內的服務，可對資產執行特定動作。 例如，當MP3音訊檔案上傳至AEM時，工作流程會觸發MP3處理常式，以擷取中繼資料並產生縮圖。 媒體處理常常與工作流程搭配使用。 AEM支援最常見的MIME類型。 特定工作可透過擴充／建立工作流程、擴充／建立媒體處理常式或停用／啟用媒體處理常式，對資產執行。

>[!NOTE]
>
>請參閱「資 [產支援的格式](file-format-support.md) 」頁面，以取得AEM Assets支援的所有格式以及每種格式支援的功能的說明。

## 預設媒體處理常式 {#default-media-handlers}

AEM Assets中提供下列媒體處理常式，並處理最常見的MIME類型：

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>處理常式名稱</td>
   <td>服務名（在系統控制台中）</td>
   <td>支援的MIME類型</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>image/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>image/png</p> <p>application/photoshop</p> <p>image/jpeg</p> <p>image/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPowerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms-powerpoint<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordprocessingml.document<br /> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.presentation<br /><br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>回退，以備找不到其他處理常式來擷取資產的資料</td>
  </tr>
 </tbody>
</table>

所有處理程式都執行下列任務：

* 從資產擷取所有可用的中繼資料。
* 從資產建立縮圖影像。

可以查看活動媒體處理程式：

1. 在瀏覽器中，導覽至 `http://localhost:4502/system/console/components`。
1. 按一下連結 `com.day.cq.dam.core.impl.store.AssetStoreImpl`。
1. 將顯示包含所有活動媒體處理程式的清單。

## 在工作流程中使用媒體處理常式來執行資產上的工作 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒體處理常式是通常與工作流程結合使用的服務。

AEM有一些處理資產的預設工作流程。 要查看它們，請開啟「工作流」(Workflow)控制台，然後按一下「模 **[!UICONTROL 型」(Models]** )頁籤：以AEM Assets開頭的工作流程標題是資產特定標題。

可擴充現有的工作流程，並建立新的工作流程，以根據特定需求處理資產。

下列範例說明如何增強 **[!UICONTROL AEM Assets Synchronization]**  (AEM Assets同步化) 工作流程，以便為除PDF檔案外的所有資產產生子資產。

### 禁用／啟用媒體處理程式 {#disabling-enabling-a-media-handler}

媒體處理常式可以透過Apache Felix Web Management Console停用或啟用。 停用媒體處理常式時，不會對資產執行其工作。

要啟用／禁用媒體處理程式：

1. 在瀏覽器中，導覽至 `https://<host>:<port>/system/console/components`。
1. 按一下 **[!UICONTROL 媒體處理程式名稱旁邊的「禁用]** 」。 For example: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 重新整理頁面：媒體處理常式旁會顯示圖示，指出其已停用。
1. 若要啟用媒體處理常式，請按一 **[!UICONTROL 下媒體處理常式]** 名稱旁的「啟用」。

### 建立新的媒體處理常式 {#creating-a-new-media-handler}

要支援新介質類型或對資產執行特定任務，必須建立新介質處理程式。 本節說明如何繼續。

#### 重要類別和介面 {#important-classes-and-interfaces}

開始實施的最佳方式是繼承所提供的抽象實施，以處理大部分事物並提供合理的預設行為：班 `com.day.cq.dam.core.AbstractAssetHandler` 級。

此類已提供抽象服務描述符。 因此，如果您繼承此類別並使用maven-sling-plugin，請確定您將inherit標幟設為 `true`。

實施下列方法：

* `extractMetadata()`:擷取所有可用的中繼資料。
* `getThumbnailImage()`:在傳遞的資產中建立縮圖影像。
* `getMimeTypes()`:傳回資產MIME類型。

以下是範例範本：

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增支援特定MIME類型的服務。 要添加新的MIME類型，必須實施此介面。 介麵包含匯入和匯出特定檔案、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：
   * 此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。
   * 開始實施的最佳方式是繼承所提供的抽象實施，以處理大部分事物並提供合理的預設行為：com.day.cq.dam.core.AbstractAssetHandler類別。
   * 此類已提供抽象服務描述符。 因此，如果您繼承此類別並使用maven-sling-plugin，請確定您將inherit標幟設為true。

需要實施下列方法：

* `extractMetadata()`:此方法會擷取所有可用的中繼資料。
* `getThumbnailImage()`:此方法會從傳遞的資產中建立縮圖影像。
* `getMimeTypes()`:此方法會傳回資產MIME類型。

以下是範例範本：

封裝my.own.stuff;/&amp;ast;&amp;ast;&amp;ast;@scr.component inherit=&quot;true&quot; &amp;ast;@scr.service &amp;ast;/ public class myMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement relevant parts }

介面和類包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增支援特定MIME類型的服務。 要添加新的MIME類型，必須實施此介面。 介麵包含匯入和匯出特定檔案、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：此類別可做為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## 基於命令行的媒體處理程式 {#command-line-based-media-handler}

AEM可讓您在工作流程中執行任何命令列工具，以轉換資產（例如ImageMagick）並將新的轉譯新增至資產。 您只需要在AEM伺服器所在的磁碟上安裝命令列工具，並新增及設定工作流程的程式步驟。 調用的程式( `CommandLineProcess`稱為)也可以根據特定MIME類型進行篩選，並根據新轉譯建立多個縮圖。

下列轉換可自動執行並儲存在AEM Assets中：

* 使用 [ImageMagick和Ghostscript進行EPS](https://www.imagemagick.org/script/index.php) 和AI [轉換](https://www.ghostscript.com/)
* 使用FFmpeg的FLV視訊轉 [碼](https://ffmpeg.org/)
* 使用 [LAME的MP3編碼](http://lame.sourceforge.net/)
* 使用 [SOX的音訊處理](http://sox.sourceforge.net/)

>[!NOTE]
>
>在非Windows系統上，FFMpeg工具會傳回錯誤，因為視訊資產的檔案名稱中有單引號(&#39;)，所以會產生轉譯。 如果您的視訊檔案名稱包含單引號，請先將其移除，然後再上傳至AEM。

該 `CommandLineProcess` 進程按列出順序執行以下操作：

* 根據特定MIME類型（如果已指定）篩選檔案。
* 在代管AEM伺服器的磁碟上建立暫存目錄。
* 將原始檔案流到臨時目錄。
* 執行由步驟的參數定義的命令。 在執行AEM之使用者的權限下，在臨時目錄內執行命令。
* 將結果串流回AEM伺服器的轉譯檔案夾。
* 刪除臨時目錄。
* 根據這些轉譯（如果已指定）建立縮圖。 縮圖的編號和尺寸由步驟的參數定義。

### 使用ImageMagick的範例 {#an-example-using-imagemagick}

以下範例說明如何設定命令列處理步驟，以便每當在AEM伺服器上將具有mime-type gif或tiff的資產新增至/content/dam時，原始影像的翻轉影像會與另外三個縮圖（140x100、48x48和10x250）一起建立。

若要這麼做，您將使用ImageMagick。 ImageMagick是一套免費的軟體套件，可用來建立、編輯和合成點陣圖影像，而且通常是從命令列使用。

首先在AEM伺服器所在的磁碟上安裝ImageMagick:

1. 安裝ImageMagick:請參閱 [ImageMagick檔案](https://www.imagemagick.org/script/download.php)。
1. 設定工具，以便在命令行上運行轉換。
1. 要查看工具是否已正確安裝，請在命令行上運 `convert -h` 行以下命令。

   它會顯示說明畫面，內含轉換工具的所有可能選項。

   >[!NOTE]
   >
   >在某些Windows版本（例如Windows SE）中，轉換命令可能無法運行，因為它與Windows安裝中的本機轉換實用程式衝突。 在這種情況下，請提及將影像檔案轉換為縮圖的ImageMagick公用程式的完整路徑。 For example, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. 若要查看工具是否正常運行，請將。jpg影像新增至工作目錄，然後在命令列上執 `<image-name>.jpg -flip <image-name>-flipped.jpg` 行命令convert。

   翻轉的影像會新增至目錄。

然後，將命令列處理步驟新增至 **[!UICONTROL DAM更新資產工作流程]** :

1. 前往「工作 **[!UICONTROL 流程]** 」主控台。
1. 在「模 **[!UICONTROL 型]** 」標籤中，編 **[!UICONTROL 輯「DAM更新資產模型]** 」。
1. 變更啟用Web的轉 **[!UICONTROL 譯步驟的設定]** ，如下所示：

   **引數**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. 儲存工作流程。

若要測試修改後的工作流程，請新增資產至 `/content/dam`。

1. 在檔案系統中，取得您所選擇的。tiff影像。 例如， `myImage.tiff` 使用WebDAV將其重 `/content/dam`新命名並複製至。
1. 例如， **[!UICONTROL 前往CQ5 DAM]** Console `http://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 開啟資產 **[!UICONTROL myImage.tiff]** ，並確認已建立翻轉的影像和三個縮圖。

#### 配置CommandLineProcess步驟 {#configuring-the-commandlineprocess-process-step}

本節介紹如何設定 **CommandLineProcess的Process****參數**。

「進程參 **數」的值** ，必須用逗號分隔，且不能以空格開頭。

<table>
 <tbody>
  <tr>
   <td> 參數格式</td>
   <td>說明</td>
  </tr>
  <tr>
   <td> mime:&lt;mime-type&gt;</td>
   <td><p>可選引數。 如果資產與其中一個引數的MIME類型相同，則會套用此程式。</p> <p>可定義數種MIME類型。</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;width&gt;:&lt;height&gt;</td>
   <td><p>可選引數。 該過程建立具有在參數中定義的尺寸的縮略圖。</p> <p>可定義數個縮圖。<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd:&lt;command&gt;</td>
   <td><p>定義將執行的命令。 語法取決於命令行工具。</p> <p>只能定義一個命令。</p> <p>以下變數可用於建立命令：<br/></p> <p><code>${filename}</code>:輸入檔案的名稱，例如「original.jpg」<br/><code>${file}</code>:輸入檔的完整路徑名稱，例如「/tmp/cqdam0816.tmp/original.jpg'<br/><code>${directory}</code>:輸入檔案的目錄，例如「/tmp/cqdam0816.tmp」。<br/> <code>${basename}</code>:未加上副檔名的輸入檔案名稱，例如原始<br/><code>${extension}</code>:輸入檔案的副檔名，例如JPG<br/></p></td>
  </tr>
 </tbody>
</table>

例如，如果ImageMagick已安裝在AEM伺服器的磁碟上，且您使用 **CommandLineProcess** as Implementation，並使用下列值作為 **Process Arguments建立處理步驟**:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然後，當工作流程執行時，此步驟僅會套用至具有image/gif或mime:image/tiff作為mime-types的資產，它會建立原始影像的翻轉影像，並將其轉換為。jpg，並建立三個尺寸縮圖：140x100、48x48和10x250。

使用下列 **Process Arguments** ，使用ImageMagick建立三個標準縮圖：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用下列 **處理參數** ，使用ImageMagick建立啟用Web的轉譯：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>CommandLineProcess **步驟僅適用於資產(類型的節**`dam:Asset`點)或資產的後代。
