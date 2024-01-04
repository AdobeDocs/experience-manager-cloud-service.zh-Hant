---
title: 使用 Universal Editor 發佈內容
description: 瞭解Universal Editor如何發佈內容，以及您的應用程式如何處理發佈的內容。
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 55%

---


# 使用 Universal Editor 發佈內容 {#publishing}

瞭解Universal Editor如何發佈內容，以及您的應用程式如何處理發佈的內容。

{{universal-editor-status}}

## 與 AEM 的相似之處 {#similarities}

使用AEM時，使用Universal Editor發佈內容的程式會依您慣用的方式運作：在AEM中發佈時，內容會從製作層級複製到發佈層級。

## 差異 {#differences}

是什麼讓使用通用編輯器發佈有些不同，與其說在於編輯器本身，不如說在於外部託管應用程式，讓通用編輯器成為可能。

進行外部託管時，Web 應用程式需要確保當作者在編輯器中打開應用程式時，從編寫層載入內容，並在訪客存取應用程式時，從發佈層載入內容。

## 偵測應用程式中的層 {#detecting}

可透過應用程式中的簡單條件陳述式來決定是否應存取編寫層或發佈層，以便在偵測到編輯器中開啟層時，選擇適當的編寫或發佈端點。

另一種選擇是將應用程式部署到設定不同的兩個環境，然後讓一個環境從編寫層擷取其內容，另一個環境從發佈層擷取。若要讓作者在通用編輯器中開啟已發佈的URL，可以建立一個小型指令碼，將發佈端URL「轉換」成其在製作環境中的同等專案(例如，在前端加上 `author` 子網域)，如此作者便會自動重新導向。

## 摘要 {#summary}

Universal Editor 的目標是不強加任何特定模式，以完全低耦合的方式達成實施的目標，同時仍保持實施簡單和直接的特性。

同樣地，Universal Editor 不會要求特定專案用哪種方法決定要從哪一層傳遞內容。相反地，它提供了多種可能性，並允許專案決定最適合自身需求的解決方案。
