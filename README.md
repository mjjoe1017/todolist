# Todolist(Angular)

### 在終端機使用Angular命令列介面(CLI)產生、建置、測試、佈署Angular的應用程式。

 開啟終端機輸入:
> D:\todolist_skyChang>npm install -g @angular/cli

若要使用Angular命令列的指令為ng開頭，接著輸入要執行的CLI指令。

將cmd路徑指向創建的資料夾，使用ng new 指令建立todo的應用程式。

> D:\todolist_skyChang>ng new todo --routing=false --style=css

則會開始建立一個初始的Angular應用程式。

* --routing: 導向至...路徑
* --style: 樣式

## 開啟專案

使用cmd開啟專案。
> D:\todolilst_skyChang>cd todo

## 執行專案

使用 ng serve 執行 todolist_skyChang 應用程式。
> D:\todolilst_skyChang\cd todo>ng serve

## 開啟 server 
`http://localhost:4200/`

※若當前正在執行ng serve時，需另開終端機來執行其他指令。

## Angular應用程式 CLI產生的檔案

* app.module.ts : 指定應用程序使用的文件。該文件充當應用程序中其他文件的中心點。
* app.component.ts : class, 包含主頁面的邏輯應用。
* app.component.html : 包含AppComponent的HTML。該檔案則會顯示在瀏覽器看到的畫面。
* app.component.css : 特定元件的樣式，不建議放入將整個應用程式的樣式。
* app.component.spec.ts : 用於元件測試的文件。

本結構將邏輯、介面、樣式分開，增加維護性和延展性。




