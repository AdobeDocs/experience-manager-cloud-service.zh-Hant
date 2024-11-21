---
title: 如何在預覽或發佈執行個體上發佈或取消發佈表單？
description: 瞭解如何從AEM製作環境發佈或取消發佈表單，以預覽或發佈執行個體。 無論您是在預備環境中測試表單，還是為一般使用者即時部署，AEM都能提供簡化的工具，讓您有效率地管理此程式。
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# 在Experience Manager Forms中管&#x200B;理發佈

作為Adobe Experience Manager Forms管理員，您可以從作者執行個體發佈表單至Experience Manager Forms。 您可以排程在稍後的日期或時間發佈表單或資料夾。 發佈後，使用者即可存取及填寫表單。

您可以使用Publish或Experience Manager Forms介面中可用的管理發布選項來發佈或取消發佈表單。 如果您對Experience Manager Forms中的原始表單或資料夾進行後續修改，則在您從Experience Manager Forms重新發佈前，這些變更不會反映在發佈執行個體中。 它可確保發佈執行個體中不會出現進行中變更。 發佈執行個體中只能使用管理員發佈的變更。

## 使用Publish選項的Publish表單

發佈選項可讓您立即發佈表單。 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要發佈的表單。 按一下工具列中的「Publish」選項，檢視將隨表單發佈的所有參考資產，然後按一下「Publish」。

電腦熒幕擷圖

說明已自動產生

## 使用管理發布來Publish或取消發佈表單


管理出版物可讓您向選定目標發佈內容或從中取消發佈內容、在表單與檔案資料夾中將內容新增到發佈清單、選取要發佈的引用，以及排程發佈到更晚的日期或時間。


從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要發佈的表單。 從工具列按一下管理出版物選項。


電腦熒幕擷圖

說明已自動產生



「管理出版物」介面中有以下選項：

* 動作

   * Publish： Publish表單至選取的目的地
   * 取消發佈：從目的地取消發佈表單

* 目的地

   * Publish： Publish forms轉Experience Manager Forms (AEM) Publish例項。
   * 預覽： Publish forms至Experience Manager Forms (AEM)預覽例項。

* 排程

   * 現在：立即Publish表單
   * 稍後：根據啟用日期或時間的Publish表單



若要繼續，請按一下[下一步] ****。 在「範圍」標籤中，使用「新增內容」選項來新增更多發佈內容。 例如，您可以新增更多Forms或記錄檔案檔案。

### 新增內容

發佈至Experience Manager Forms可讓您進一步新增更多內容（表單、資產和資料夾）至發佈清單。 您可以從formsanddocuments資料夾新增更多表單、資產或資料夾至清單。 但您無法一次從多個資料夾新增資產。

電腦熒幕擷圖

說明已自動產生

按一下「**新增內容**」按鈕以新增更多內容。 您可以從資料夾中新增多個資產，或一次新增多個資料夾。 但您無法一次從多個資料夾新增資產。

若要設定要發佈或不發佈表單或其他資產的引用，請選取表單或資產，然後按一下「已發佈引用」 。

電腦熒幕擷圖

說明已自動產生

在「已發佈參考」對話方塊中，取消勾選您計畫不發佈的資產，然後按一下完成。


電腦熒幕擷圖

說明已自動產生


## Publish或稍後取消發佈表單


除了可讓您在稍後日期和時間發佈或取消發佈表單外，稍後發佈或取消發佈選項也可讓您設定工作流程。 在工作流程完成後，會發佈或取消發佈表單。 若要排程表單以供發佈或取消發佈：

1. 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要排程發佈的表單。
1. 從工具列按一下管理出版物選項。
1. 按一下Publish或「從動作中取消發佈」 ，然後選取您要發佈或取消發佈內容的目的地。

   * 預覽：使用「預覽」選項可發佈或取消發佈至Experience Manager Forms預覽環境。 Experience Manager Forms預覽環境用於測試開發表單。
   * Publish：使用Experience Manager Forms Publish選項可在表單準備好用於生產環境後，將表單傳送至Experience Manager Forms發佈環境。


1. 在「排程」中選取「稍後」。

1. 選取啟用日期並指定日期和時間。 按一下「下一步」。

   電腦熒幕擷圖

   說明已自動產生

1. 在「範圍」索引標籤中，視需要新增內容。 按一下「下一步」。

   電腦熒幕擷圖

   說明已自動產生

1， （選用）在「工作流程」標籤中，指定「工作流程」標題。 按一下稍後的Publish。

電腦熒幕擷圖

說明已自動產生

## 決定發佈狀態

有多種方式可判斷發佈狀態：

* 登入目的地執行個體以驗證發佈的表單和其他資產（取決於排定的日期或時間）。

* 使用時間軸檢視來判斷出版物狀態。

* 使用最適化Forms編輯器中的頁面資訊選單。