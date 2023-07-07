---
title: 使用 Universal Visual Editor 發佈內容
description: 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 0f62245d31074ab7a64d86b97ef3b1a8d7533001
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 88%

---


# 使用 Universal Visual Editor 發佈內容 {#publishing}

了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。

## 與 AEM 的相似之處 {#similarities}

對於 AEM 使用者來說，使用 Universal Visual Editor 發佈內容的流程您已經很熟悉：在 AEM 中發佈時，內容會從作者層複製到發佈層。

## 差異 {#differences}

使用 Universal Visual Editor 進行發佈的差異不在於編輯器本身，而是 Universal Editor 可讓應用程式進行外部託管。

進行外部託管時，Web 應用程式需要確保當作者在編輯器中打開應用程式時，從作者層載入內容，並在訪客存取應用程式時，從發佈層載入內容。

## 偵測應用程式中的層 {#detecting}

可透過應用程式中的簡單條件陳述式來決定是否應存取作者層或發佈層，以便在偵測到編輯器中開啟層時，選擇適當的作者或發佈端點。

另一種選擇是將應用程式部署到設定不同的兩個環境，然後讓一個環境從作者層擷取其內容，另一個環境從發佈層擷取。若要允許作者在通用編輯器中開啟已發佈的URL，可以建立一個小型指令碼，將發佈端URL「轉換」成作者環境上的等同專案(例如，在前面加上 `author` 子網域)，如此作者便會自動重新導向。

## 摘要 {#summary}

Universal Editor 的目標是不強加任何特定模式，以完全低耦合的方式達成實施的目標，同時仍保持實施簡單和直接的特性。

同樣地，Universal Editor 不會要求特定專案用哪種方法決定要從哪一層傳遞內容。相反，它支援多種可能性，可讓專案自行決定最符合其需求的解決方案。
