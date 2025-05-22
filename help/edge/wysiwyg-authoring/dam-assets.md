---
title: 使用 Edge Delivery Services 發佈包含 DAM 資產的頁面
description: 了解需要哪些設定才能確保您頁面的 DAM 資產順暢無礙地發佈至 Edge Delivery Services。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# 使用 Edge Delivery Services 發佈包含 DAM 資產的頁面 {#dam-assets}

了解需要哪些設定才能確保您頁面的 DAM 資產順暢無礙地發佈至 Edge Delivery Services。

## 通用編輯器、DAM 資產以及 Edge Delivery {#overview}

編輯通用編輯器的內容時，您當然可以從 DAM 中選取資產。當您將內容發佈至 Edge Delivery Services 時，相關的 DAM 內容也會發佈。

若要確保此流暢的行為，AEM 和 Edge Delivery Services 必須具有 DAM 的適當存取權才能發佈。其中包括：

* [確保資產資料夾可存取](#accessible)。
* [確保資產資料夾已指派至正確的設定 (視需要)](#configuration)。

## 確保資產資料夾可存取 {#accessible}

將頁面從 AEM 發佈至 Edge Delivery Services 時，需要使用[技術帳戶](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。每當您首次發佈使用通用編輯器建立的頁面時，Cloud Manager 會自動將此帳戶 (名稱格式為 `<hash>@techacct.adobe.com`) 建立為 AEM 的使用者。

![技術帳戶](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

此技術帳戶必須具有所有 DAM 資料夾的存取權才能發佈其內容。下列兩個動作您可以擇一執行：

* 不使用私人 DAM 資料夾。
* 授予此技術帳戶使用者 DAM 資料夾的存取權。

## 確保對資產資料夾已指派正確的設定 {#configuration}

通常，確保您的技術帳戶可以存取 DAM 中的資產，便可以將您的資產和頁面一起發佈至 Edge Delivery Services。

不過，在另外兩種情況下，需要進行額外設定：

* 如果您希望發佈包含非影像資產 (例如 PDF 或影片) 的頁面發佈至 Edge Delivery Services。
* 如果您希望將影像資產獨立發佈至 Edge Delivery Services 而不包含頁面。

若要支援此兩種使用案例，必須將[設定](/help/implementing/developing/introduction/configurations.md)指派至 DAM 資料夾。

1. 登入您的 AEM 製作環境。
1. 於 **Sites** 下方選取您要發佈資產的網站，或是將與資產建立關聯的網站。
1. 點選或按一下工具列中的「**屬性**」。
1. 在「屬性」視窗中的「**進階**」索引標籤，記下「**雲端設定**」欄位中的設定。
   * 當您以 `/conf/<site-name>` 格式建立網站時，此設定會自動建立。
1. 在「屬性」視窗中點選或按一下「**取消**」，並導覽至「**資產**」->「**檔案**」，然後選取您的 DAM 資料夾。
1. 點選或按一下工具列中的「**屬性**」。
1. 在「屬性」視窗的「**雲端服務**」索引標籤上，在「**雲端設定**」欄位中，選取與之前相同的設定。
1. 點選或按一下「**儲存並關閉**」。
