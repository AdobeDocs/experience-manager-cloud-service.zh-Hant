---
title: 使用核心元件和 Headless 建置吸引人的表單
seo-title: Build Engaging Forms Using Core Components and Headless
description: 使用核心元件和 Headless 建置吸引人的表單
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
exl-id: e1eb0812-c92e-4a18-aabb-5a70b9e6fc7d
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '3358'
ht-degree: 98%

---

# 使用核心元件和 Headless 建置吸引人的表單

## 實驗室概觀

在這個實作實驗室中，您將學習：

如何運用 AEM Forms 使用與 AEM Sites 一致的最新核心元件輕鬆建立最適化表單，透過將最適化表單作為無頭表單交付到 Web、行動裝置和聊天來實施全通路資料擷取體驗。您還將學習有關樣式、自訂和前端開發的最佳實務。

## 關鍵重點

* **業務彈性**：作為業務使用者，我可以輕鬆地為多個通道建立表單體驗。

* **前端開發人員的力量**：作為前端開發人員，我可以使用無頭表單來控制終端使用者體驗。

* **開發人員速度**：作為一名開發人員，我可以輕鬆且一致地自訂 Sites 和 Forms 元件。

## 必備條件


+++AEM Forms as Cloud Service 沙箱



<table>
        <thead>
            <tr><th>實驗室識別碼</th><th>編寫執行個體 URL</th><th>發佈執行個體 URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## 第一課

### 目標

熟悉 AEM Forms as a Cloud Service 環境。

### 課程內容

在本課程中，您將瀏覽使用者介面，熟悉 AEM Forms as a Cloud Service 環境。

### 練習

1. 打開瀏覽器並輸入 Cloud Service 編寫環境的 URL。

1. 登入 Cloud Service 編寫環境。您創作環境的登入憑證會在實驗期間與您共用。

1. 登入後，瀏覽至 AEM Forms UI。點擊 **Forms**。

   ![](/help/forms/assets/screenshot2028113829.png)

1. 點擊&#x200B;**表單和文件**。關閉任何與偏好設定或資訊相關的快顯視窗。

   ![](/help/forms/assets/screenshot2028113929.png)

   顯示所有可用的表格。

   ![](/help/forms/assets/screenshot2028114029.png)

## 第二課

### 目標

使用最新的核心元件編寫最適化表單，設定並提交表單。

### 課程內容

在本課中，作為業務使用者，您將使用最適化表單編寫和用於資料擷取的標準化 OOTB 核心元件，為 Web、移動和聊天等多個通道編寫最適化表單。

### 練習

1. 為表單建立一個提交端點：

   1. 在新的瀏覽器標籤中打開 <https://requestbin.com/>。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. 點選 **Create a public bin** 並複製端點 URL。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. 使用精靈介面編寫最適化表單：

   1. 在第 1 課中使用的瀏覽器標籤中，導覽至 AEM Forms as Cloud Service Web 介面，然後導覽至 Forms and Documents。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 點選 **Create** 並選擇 Adaptive Form。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 從範本選擇畫面中選擇 **Blank with Core Components** 範本，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 點選 **Style** 標籤，選擇&#x200B;**wknd-theme**主題，如下圖：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 點擊 **Submission** 標籤並選擇 **Submit to REST end-point** 卡並在
      **POST 要求的 URL** 欄位如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 按一下&#x200B;**建立**。為表單指定名稱和標題。例如，**聯繫我們**。按一下&#x200B;**建立**。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. 最適化表單編輯器打開。關閉任何與偏好設定或資訊相關的快顯視窗或對話框。點擊左欄上的元件瀏覽器並將 **Footer** 元件新增到空白表單的底部。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. 標頭是最適化表單範本的一部分。這可輕鬆讓所有最適化表單擁有一致的標頭/頁尾。或者，您也可以選擇使其在表單中保持可編輯狀態 - 如下一步中的頁尾元件所示。

   1. 在表單中間新增&#x200B;**標題**元件。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. 在標題元件後新增&#x200B;**文字輸入**元件。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. 新增&#x200B;**數字輸入**元件。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. 將&#x200B;**提交按鈕**元件新增到表單。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 點選&#x200B;**標題**&#x200B;元件，**快顯視窗選單**&#x200B;隨即顯示。點擊選單中的&#x200B;**編輯圖示**以編輯標籤。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 輸入 `Contact Us` 作為標題文字。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 點選&#x200B;**文字輸入**&#x200B;元件，快顯視窗選單隨即顯示。點擊選單中的&#x200B;**編輯圖示**以編輯標籤。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 輸入&#x200B;**全名**作為欄位標籤。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 點選&#x200B;**數字輸入**&#x200B;元件，快顯視窗選單隨即顯示。點擊選單中的&#x200B;**編輯圖示**以編輯標籤。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 輸入&#x200B;**電話號碼** 作為欄位標籤。
      ![](/help/forms/assets/screenshot2028123829.png)


1. 將驗證新增至表單：

   1. 點選&#x200B;**電話號碼**&#x200B;元件，快顯視窗選單隨即顯示。點擊選單中的&#x200B;**扳手圖示**以設定欄位。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. 打開&#x200B;**驗證標籤**，標記欄位&#x200B;**必要**，然後點擊&#x200B;**完成**。成功訊息隨即顯示。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 點擊&#x200B;**預覽**，從終端使用者的角度預覽表單。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. 用虛擬資料填寫表格
      ![](/help/forms/assets/screenshot2028125629.png)

   1. 提交表單
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 在 Request Bin 標籤中，檢查提交的資料。
      ![](/help/forms/assets/screenshot2028125829.png)

現在為了完成剩餘的練習，請使用預先建立的註冊表單。

1. 打開 AEM Forms 管理介面，例如 `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`，然後選擇註冊表單。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 點擊&#x200B;**發佈**。

   ![](/help/forms/assets/screenshot2028115629.png)

   成功訊息隨即顯示。

   ![](/help/forms/assets/screenshot2028115729.png)

   表單的發佈 URL 會類似於 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`。

1. 要查看已發佈的表單，請將上述 URL 中的程序 ID (pXXXXXX) 和環境 ID (eXXXXXX) 取代為您環境的 ID。

## 第三課

### 目標

使用前端開發最佳實務更新樣式。

### 課程內容

在本課中，作為前端開發人員，您將學習如何輕鬆地更新先前建立的最適化表單的樣式。

### 練習

設定主題的本機存放庫：

1. 使用管理員權限打開命令提示字元或殼層：

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示字元中，使用以下命令瀏覽到 **c:\git** 資料夾

   ```Shell
   cd c:\git
   ```

1. 使用以下命令複製主題前端程式碼：

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 按照列出的順序使用以下命令瀏覽到 **aem-forms-theme-canvas** 目錄並打開 Visual Studio Code。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 選取&#x200B;**信任上層資料夾中所有文件的作者**，並點選&#x200B;**是的，我信任作者**。

   ![](/help/forms/assets/screenshot2028116229.png)

1. 要呈現在您的雲端服務發佈環境中託管的表單，請重新命名 `env_template` 文件。若要重新命名檔案，請用滑鼠右鍵按一下 **環境範本** 檔案並選取 **重新命名** 選項。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. 為 .env 檔案中的變數設定以下值並儲存檔案：

   * **AEM_URL**：指定您的雲端服務發佈環境。例如 `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**：指定表單的路徑。例如，如果表單路徑為 `/content/forms/af/registration`，則此變數的值將為 `registration`。

   ![](/help/forms/assets/screenshot2028116429.png)


1. 在命令提示字元視窗中，執行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * 如果您收到要求透過 `npm notice Run npm nstall -g npm@9.6.0` 命令更新 npm 的訊息，請忽略該訊息。
   > * 除非活頁簿中有指示，否則不要執行其他 npm 命令。

1. 現在執行以下命令來預覽表單。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   執行上述命令後，等待 `webpack compiled` 訊息。表單會顯示在瀏覽器標籤中。

   >[!NOTE]
   >
   >如果您在執行 `npm run live` 命令超過 3-4 分鐘後瀏覽器出現黑畫面，請將瀏覽器 URL 中的 `localhost` 變更為 127.0.0.1，並點擊&#x200B;**輸入**。


   ![](/help/forms/assets/screenshot2028115129.png)


1. 在 Visual Studio Code 中，打開 `PROJECT\src\site\_variables.scss` 檔案。請注意，`$error` 顏色是紅色陰影。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 在瀏覽器中，提交表單以在&#x200B;**名字**&#x200B;欄位中看到紅字。

   ![](/help/forms/assets/screenshot2028120829.png)

1. 將 **$error** 顏色設定為 **#5736eb** 並儲存檔案。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 重新整理瀏覽器並提交表單。請注意，名字欄位上的錯誤顏色已跟著更改。

   ![](/help/forms/assets/screenshot2028121129.png)

1. 在命令提示字元中，按 **CTRL+C**，輸入 **Y**，然後按 **Enter** 鍵終止 npm 程序。停止 npm 伺服器很重要，這樣就不會與下一組練習發生衝突。
1. 關閉 Visual Studio Code 和命令提示字元視窗。

## 第四課

### 目標

將表單作為無頭表單呈現在 Web/行動裝置和其他介面。

### 課程內容

在本課程中，作為前端開發人員，您將學習如何使用 React Spectrum 設計框架，將之前建立的最適化表單呈現為無頭表單。

### 練習

使用 React 啟動專案設定本機存放庫：

1. 使用管理員權限打開命令提示字元。

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示字元中，使用以下命令瀏覽到 **c:\git** 資料夾

   ```Shell
   cd c:\git
   ```

1. 使用以下命令複製最適化表單 React 啟動專案：

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 按照列出的順序使用以下命令瀏覽到 **react-starter-kit-aem-headless-forms** 目錄，並打開 Visual Studio Code。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Visual Studio Code 視窗隨即開啟。

   ![](/help/forms/assets/screenshot2028117429.png)

要呈現在您的雲端服務發佈環境中託管的表單：

1. 將 env_template 檔案重新命名為 .env 檔案。要重新命名，請用右鍵按一下 **env_template** 檔案，然後選擇&#x200B;**重新命名**&#x200B;選項。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. 為 .env 檔案中的變數設定以下值。更新變數後，儲存檔案。

   * **AEM_URL**：指定雲端服務發佈環境的 URL。例如 `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**：指定上節課程所建最適化表單的路徑。例如 `/content/forms/af/registration/`

     ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. 打開命令視窗，確認您位於 react-starter-kit-aem-headless-forms 目錄中，然後執行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. 在命令提示字元視窗中，執行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上面的命令會啟動本機開發伺服器，該伺服器將使用 react-spectrum 前端庫以無頭方式呈現從 AEM 擷取的表單定義。

   >[!NOTE]
   >
   > 
   > 如果您在執行 `npm start` 命令超過 3-4 分鐘後瀏覽器出現黑畫面，請將瀏覽器 URL 中的 `localhost` 變更為 127.0.0.1，並點擊&#x200B;**輸入**。

   ![](/help/forms/assets/screenshot2028118229.png)

讓我們確認一下這種無頭形式的規則執行情況：

1. 選取&#x200B;**勾選此項以享受 5% 折扣**&#x200B;選項。隨後申請信用卡的選項會停用。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 取消選取&#x200B;**勾選此項以享受 5% 折扣**&#x200B;以啟用信用卡選項。

   ![](/help/forms/assets/screenshot2028126329.png)

讓我們以業務使用者的身份對伺服器上的表單進行變更，並自動查看反映在無頭表單中的變更。

1. 在瀏覽器中打開 AEM Forms 管理介面。\
1. 選取&#x200B;**註冊**&#x200B;表單，然後點選&#x200B;**編輯。**&#x200B;這會在最適化表單編輯器中打開表單。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 選取&#x200B;**電話號碼**&#x200B;欄位，然後點選工具列中的&#x200B;**編輯圖示 (鉛筆圖示)**。如果您工具列沒有跳出來，請點擊右上角的&#x200B;**編輯**&#x200B;按鈕切換到編輯模式，然後點擊左上角的 **預覽**&#x200B;按鈕。

   ![](/help/forms/assets/screenshot2028119629.png)

1. 將標籤變更為手機號碼。點擊表單中的任何空白區域將儲存對表單所做的變更。

   ![](/help/forms/assets/screenshot2028119729.png)

讓我們發佈更新的表單以將變更散佈到發佈環境。

1. 在 AEM Forms 管理介面標籤中，選擇註冊表單，然後點擊&#x200B;**取消發佈**。如果您沒有看到&#x200B;**取消發佈**&#x200B;按鈕，請跳至第 3 步直接發佈變更。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 點擊&#x200B;**取消發佈**。在相應的對話框中點擊&#x200B;**關閉**。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. 瀏覽器重新整理後，選擇註冊表單，然後點擊&#x200B;**發佈**。

   ![](/help/forms/assets/screenshot2028120129.png)


1. 點擊&#x200B;**發佈**。在相應的對話框中點擊&#x200B;**關閉**。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. 重新整理顯示無頭表單的瀏覽器標籤。請注意，電話號碼標籤已變更為手機號碼。

   ![](/help/forms/assets/screenshot2028120529.png)

1. 打開用於啟動 **react-starter-kit-aem-headless-forms** 專案的命令提示字元視窗，**按 CTRL+C**，然後輸入 **Y**，並按 Enter 鍵終止 npm 程序。停止 npm 伺服器很重要，這樣就不會與下一組練習發生衝突。

1. 關閉 Visual Studio Code 和命令提示字元視窗。


## 第五課

### 目標

使用 Google Material UI 將表單呈現為無頭表單

### 課程內容

在本課程中，作為前端開發人員，您將學習如何使用 Google Material UI 將之前建立的最適化表單呈現為無頭表單。

### 練習

使用 Material UI 啟動專案設定本機存放庫：

1. 使用管理員權限打開命令提示字元。

   ![](/help/forms/assets/screenshot2028115829.png)


1. 在命令提示字元中，使用以下命令瀏覽到 **c:\git** 資料夾：

   ```Shell
   cd c:\git
   ```

1. 按列出的順序執行以下命令以建立名為 mui 的資料夾，並使用以下命令瀏覽到 mui 資料夾：

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 使用以下命令複製最適化表單 React 啟動專案：

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 按照列出的順序使用以下命令瀏覽到 **react-starter-kit-aem-headless-forms** 資料夾，並打開 Visual Studio Code 中的程式碼：

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

要呈現在您的雲端服務發佈環境中託管的表單：

1. 將 **env_template** 檔案重新命名為 **.env** 檔案。要重新命名，請用右鍵按一下 **env_template** 檔案，然後選擇&#x200B;**重新命名**。

   ![](/help/forms/assets/screenshot2028126629.png)

1. 為 .env 檔案中的變數設定以下值。更新變數後，儲存檔案。使用 **CTRL + S** 切換組合以儲存檔案。

   * **AEM_URL**：指定雲端服務發佈環境的 URL。

   * **AEM_FORM_PATH**：指定上節課程所建最適化表單的路徑。例如 /content/forms/af/registration/

     ![](/help/forms/assets/screenshot2028126929.png)

1. 打開命令視窗，確認您位於 **react-starter-kit-aem-headless-forms** 目錄中，然後執行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. 在命令提示字元視窗中，執行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   該命令會啟動本機開發伺服器，並使用 Google Material UI 前端庫以無頭方式呈現從 AEM 擷取的表單定義。

   >[!NOTE]
   >
   >如果您在執行 `npm start` 命令超過 3-4 分鐘後瀏覽器出現黑畫面，請將瀏覽器 URL 中的 `localhost` 變更為 127.0.0.1，並點擊&#x200B;**輸入**。

   ![](/help/forms/assets/screenshot2028127229.png)

1. 若要評估此表單轉譯中相同商業邏輯的執行情況：

   選取&#x200B;**勾選此項以享受 5% 折扣**。後續選項&#x200B;**您想申請 We Finance 公司信用卡表單嗎？**&#x200B;將會停用。

   ![](/help/forms/assets/screenshot2028127329.png)

## 第六課

### 目標

使用 Material UI 元件變體建立無頭表單的替代外觀

### 課程內容

在本課程中，作為前端開發人員，您將學習如何使用 Material UI 為業務使用者之前建立的最適化表單建立不同元件的替代外觀。

### 練習

更新無頭專案中元件的變體。將 Material UI 文字輸入元件的變體變更為 `OutlinedInput`：

1. 在 Visual Code 中，透過打開位於 `src/components/textinput/index.tsx` 的 `index.tsx` 檔案瀏覽到文字輸入元件。

1. 在程式碼 103 行的開頭新增 `//`。這會將行轉換為註解。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 在第 104 行新增以下內容以使用不同的元件變體，然後儲存檔案。使用 **CTRL + S** 切換組合以儲存檔案。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   &#39;OutlinedInput&#39; 變體必須使用正確的大寫字母，否則編譯會失敗。本機開發環境編譯會在命令提示字元中自動開始。等到您看到以下訊息

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 如果沒有自動重新整理，請手動重新整理瀏覽器，您就可以看到文字輸入元件使用不同的變體。

   ![](/help/forms/assets/screenshot2028127729.png)


   此變更適用於終端使用者，無需對 AEM Forms Server 中的表單定義進行任何變更，且是針對考慮中的無頭通道。例如，本實驗室中的 Web 通道。

   ![](/help/forms/assets/screenshot2028127529.png)


1. 關閉 Visual Studio Code 和命令提示字元視窗。

## 常見問題集 (FAQ)

+++ 最適化表單精靈是否已正式推出？

是的，AEM Forms as Cloud Service 已提供最適化表單精靈。

+++


+++ 核心元件是否已正式推出？

是的，AEM Forms as a Cloud Service 已提供 Adaptive Forms 核心元件。

+++

+++ Headless 表單是否已正式推出？

是的，AEM Forms as a Cloud Service 已提供 Headless 表單。

+++

+++ Headless 表單是否需要單獨授權？

不用，Headless 表單使用相同的授權值量度，即表單提交次數。

+++

+++ AEM 6.5 Forms 是否提供核心元件和 Headless 表單？

是的，AEM Forms 6.5 Service Pack 16 及更高版本均提供最適化表單核心元件和無頭表單。

+++


## 後續步驟

現在您已經了解如何建置最適化表單，並使用無頭表單將它們傳送到多個通道，接下來您應該嘗試將新技能付諸實踐。請繼續為您的終端使用者大規模建立和提供卓越的資料擷取體驗！

## 資源

* [最適化表單核心元件簡介](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [使用核心元件建立最適化表單](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [更新核心元件型 AF 的樣式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Headless 最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [使用 Headless React 入門套件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)
