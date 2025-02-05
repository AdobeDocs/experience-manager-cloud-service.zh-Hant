---
title: 使用Edge Delivery Services透過DAM Assets發佈頁面
description: 瞭解確保將您頁面的DAM資產無縫發佈到Edge Delivery Services所需的設定。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---

# 使用Edge Delivery Services透過DAM Assets發佈頁面 {#dam-assets}

瞭解確保將您頁面的DAM資產無縫發佈到Edge Delivery Services所需的設定。

## 通用編輯器、DAM Assets和Edge Delivery {#overview}

針對通用編輯器編輯內容時，您當然可以從DAM中選取資產。 當您發佈內容至Edge Delivery Services時，也會發佈相關的DAM內容。

為確保這種順暢的行為，AEM和Edge Delivery Services必須擁有適當的DAM存取權才能發佈。 其中包括：

* [確定資產資料夾可以存取](#accessible)。
* [確定資產資料夾已指派適當的設定（視需要）](#configuration)。

## 確保Assets資料夾可供存取 {#accessible}

從AEM發佈頁面至Edge Delivery Services時，使用[技術帳戶](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)。 當您第一次發行使用通用編輯器建立的頁面時，此帳戶會由Cloud Manager在AEM中自動建立為使用者，其名稱格式為`<hash>@techacct.adobe.com`。

![技術帳戶](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

此技術帳戶必須具有所有DAM資料夾的存取許可權，才能發佈其內容。 您可以執行下列兩個動作中的一個:

* 請勿使用私人DAM資料夾。
* 授予技術帳戶使用者對DAM資料夾的存取權。

## 確保為Assets資料夾指派正確的設定 {#configuration}

通常可確保您的技術帳戶擁有您在DAM中資產的存取權，這足以將您的資產與頁面發佈到Edge Delivery Services。

但在其他兩種情況下需要額外設定：

* 如果您想要將含有PDF或影片等非影像資產的頁面發佈至Edge Delivery Services。
* 如果您想要將影像資產發佈到Edge Delivery Services，而不受頁面影響。

若要支援這兩個使用案例，必須將[設定](/help/implementing/developing/introduction/configurations.md)指派給DAM資料夾。

1. 登入您的AEM編寫環境。
1. 在「**網站**」下，選取您要發佈資產的網站或是與資產關聯的網站。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在屬性視窗的&#x200B;**進階**&#x200B;索引標籤上，記下&#x200B;**雲端設定**&#x200B;欄位中的設定。
   * 當您以`/conf/<site-name>`格式建立您的網站時，會自動建立此專案。
1. 在屬性視窗中，點選或按一下「**取消**」，並導覽至&#x200B;**Assets** -> **檔案**，然後選取您的DAM資料夾。
1. 在工具列中點選或按一下&#x200B;**屬性**。
1. 在屬性視窗的&#x200B;**Cloud Service**&#x200B;標籤上，在&#x200B;**雲端組態**&#x200B;欄位中，選取您先前指出的相同組態。
1. 點選或按一下「**儲存並關閉**」。
