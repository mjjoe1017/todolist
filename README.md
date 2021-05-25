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
![](https://i.imgur.com/Xh3Uw1Z.png)


※若當前正在執行ng serve時，需另開終端機來執行其他指令。

## Angular應用程式 CLI產生的檔案

1. app.module.ts : 指定應用程序使用的文件。該文件充當應用程序中其他文件的中心點。
2. app.component.ts : class, 包含主頁面的邏輯應用。
3. app.component.html : 包含AppComponent的HTML。該檔案則會顯示在瀏覽器看到的畫面。
4. app.component.css : 特定元件的樣式，不建議放入將整個應用程式的樣式。
5. app.component.spec.ts : 用於元件測試的文件。

本結構將邏輯、介面、樣式分開，增加維護性和延展性。

## Angular應用程序的結構

Angular是使用[TypeScript](https://www.typescriptlang.org/)建構。

component(元件)包含一個TypeScript的class，裡面會有@Component()這裡面會在有HTML模板和樣式。


## Class

在class中，可放置在專案中需要的邏輯，包括函數(functions)、事件監聽(event listeners)、屬性(properties)、服務(services)。

比如說:
1. feature.component.ts (feature是元件的名稱)
2. signup.component.ts
3. feed.component.ts

建立@Component()元件，在其中預設HTML、CSS的檔案設定

```typescript=
    import { Component } from '@angular/core';
    
    @Compoment({
        selector: 'app-item',
        // the following metadata specifies the location of the other parts of the component
        templateUrl: './item.component.html',
        styleUrls: ['./item.component.css']
    })
    
    export class ItemComponent {
        // your code goes here
    }
```

## HTML 模板(template)

引用外部的HTML檔案，使用templateUrl。
```typescript=
    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html'
    })
    
    export class AppComponent {
    
    }
```

編寫內部的HTML，使用template。
```typescript=
    @Component({
        selector: 'app-root',
        template: `<h1>Hello</h1>`,
    })
    
    export class AppComponent {
    
    }
```

Angular語法加入HTML，可從元件(Component)插入動態值。每當元件中狀態更改時，Angular會自動更新DOM內的值。
```htmlembedded=
    <h1> {{ title }} </h1>
```

Example:
```typescript=
    import { Component } from '@angular/core';
    
    @Component ({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
    })
    
    export class AppComponent {
        title = 'To do application';
    }
```

## Styles

元件(Component)可從Styles.css繼承全域樣式，也可自定義樣式來擴展或覆蓋。
可以直接在@Component()中編譯特定樣式，或指定CSS檔案路徑。

引用外部的CSS檔案，使用styleUrls。
```typescript=
    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
    })
```

編寫內部的CSS，使用styles。
```typescript=
    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styles: ['h1 { color: red; }']
    })
```