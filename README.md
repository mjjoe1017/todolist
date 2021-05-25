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

# 建立Angular待辦事項

#### 使用元件來組成應用程式

這個待辦事項應用程式有兩個元件:
1. 作為應用程式基底。
2. 用來處理待辦事項。

#### 使用 *ngIf 與 *ngFor 動態改變UI
1. *ngFor : 根據陣列中項目動態建立DOM元素。
2. *ngIf : 根據某個條件來對DOM進行添加或移除元素。

#### 元件之間共用資料
1. @Input : 允許資料輸入
2. @Output : 允許資料輸出

## 定義項目
再app目錄中建立item.ts
```typescript=
    export interface Item {
        description : string;
        done : boolean;
    }
```

這個Item interface 用來建立一個item物件模組。對於dotolist來說，item物件說明是否已完成兩個屬性。

## 將邏輯加入AppComponent
app.component.ts 內容修改如下:
```typescript=
    // 用Javascript import 匯入 Angular
    import { Component } from '@angular/core';
    
    // @Component() 指定關於AppComponent 的資料(metadata)
    @Component({
        // selector : 表示使用在範本內的CSS選擇器名稱，實體化元件，此處為'app-root'。
        // 當產生應用程式時，於index.html檔案中的body標籤內，Angular CLI就加入了<app-root></app-root>
        selector: 'app-root',
        // 指定與這個元件相關的HTML檔案
        templateUrl: './app.component.html',
        // 提供要套用在這個元件的樣式表的檔案位址與名稱
        styleUrls: ['./app.component.css']
    })
    
    export class AppComponent {
        title = 'todo';
        
        // filter屬性為union型態，表示filter的值可能為all、active、done
        // 因此若輸入錯誤的值，TypeScript會顯示錯誤訊息
        filter: 'all' | 'active' | 'done' = 'all';
        
        // allItems 陣列包含所有代辦項目，其中也包含項目是否已完成(done)屬性，如:eat done的值為true
        allItems = [
            { description: 'eat', done: true },
            { description: 'sleep', done: false },
            { description: 'play', done: false},
            { description: 'laugh', done: false},
        ];
        
        // 當filter等於all時，get items()會由allItems陣列中獲取所有的項目，否則get items()會回傳done的項目或是取決於使用者如何篩選未完成項目
        get items() {
            if(this.filter === 'all') {
                return this.allItems;
            }
            return this.allItems.filter(item => this.filter === 'done' ? item.done : !item.done);
        }
    }
```

## 將HTML加入至AppComponent的範例
app.component.html 內容修改為:
```htmlmixed=
    <div class="main">
        <h1>My To Do List</h1>
        <h2>What would you like to do today?</h2>
        
        <ul>
            <liz *ngFor="let item of items"> {{ item.description }} </li>
        </ul>
    </div>
```
畫面如下:

![](https://i.imgur.com/Beabbh1.png)



## 將項目加入至列表
app.component.ts 加入以下方法:
```typescript=
    export class AppComponent {
    // ...略...

    // 將項目加入至列表
    // (此處修正:description參數需加入any類型)
    addItem(description: any) {
      this.allItems.unshift({
          description,
          done: false
      })
    }
}
```

addItem()方法，在使用者點擊Add按鈕時將要新增的項目加入陣列中。
1. unshift(): 新增項目到陣列的開頭位置與列表的頂端。
2. push(): 新增項目到陣列的最後位置與列表的尾端。


app.component.html 修改為:
```htmlmixed=
    <label for ="addItemInput">What would you like to do today?</label>
    
    <input #newItem placeholder="add an item" (keyup.enter)="addItem(newItem.value); newItem.value=''" class="lg-text-input" />
    
    <button class="btn-primary" (click)="addItem(newItem.value)">
        Add
    </button>
```


