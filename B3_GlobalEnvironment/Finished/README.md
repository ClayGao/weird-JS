## EC

不論何時執行，JS 一定會在執行環境，把正在執行的程式碼包在執行環境裡。

## 基礎執行環境就是 Global 執行環境

1. GC 創造了 Global Object，與 `this`

## 試試看

對 index.html 執行 Live preview，輸入 `this`

![01](../../static/images/01.png)

現在的 `this` 是 `window`，代表我現在運行的這個瀏覽器視窗，當然，如果是在 node.js 執行，則會是 `global`

每個分頁都會有他自己的 `window`

這些東西就是執行環境幫我們創造的，這就是全域物件

`this === window`

window 和 this 不需要程式碼就會被創造，他們不在函式裡

在 global 寫點 code，他們會在 window 裏面。

當程式被執行時，如果不在函式裏面，就會在 window 裏面，也就是在 global 裏面，所以以 app.js 來說，this.a === window.a

因為已經在最外面了，所以 Outer Environment 會是 `null`

## Hoisting

提昇的現象就不多說了，這邊講一下 Weird JS 是怎麼說的

「網路上解釋 Hoisting 是函式和變數被提升到程式碼最上面，但這不是完全正確的，因為如果是這樣的話，下面這個案例就不會是 `undefined`。」

```js

console.log(a) // -> undefined

var a = 'hello world' 

```

## 執行環境被分為兩階段創造，也就是編譯與執行

創造階段時，會建立 Global EC，this，與 Outer Environment，會設定變數和函式在記憶體裡，這就是提升，不單單只是把程式碼提升到最上面而已。

當我賦予值之前，JS Engine 已經先預留了記憶體空間給函式和變數了。

這就是屬於創造階段，也就是編譯。

## JS 與 undefined

`undefined` 的定義是屬於，宣告過了，有記憶體位置了但沒有被設定，但他也算是值的一種。

如果今天是顯示 `is not defined`，那要記得他是不一樣的東西，這代表「從未宣告過變數」

記得如果是 `undefined` 代表 JS 已經留一個記憶體給他了，就概念上或許他很像「無」，但事實是你還是要把它當作一個值才對。

另外，千萬不要把值設置為 undefined，因為這樣很難去分辨這是你自己去設定的，還是 JavaScript Engine 自己去幫你設定的。

## 執行環境被分為兩階段創造，之執行階段

這邊因為已經是會的提升的部分，所以就不多提了，這邊只要知道執行的確是逐行執行的就好。

## 單執行緒與同步執行

### 單執行緒

表示，一次執行一次指令，瀏覽器中，並不是只有 JavaScript Engine

### 同步

與單執行序很像，同步表示的意思是「一次一個」，不是一次兩個或一次三個，並且他是「照順序的」「一次執行一行」

### Call Stack 與 Callback queue

invocation，表示是「執行」函式，如 `foo()`，這樣的行為稱為 invocation

```js

function b() {

}

function a() {
    b()
}

a()
```

當這樣的程式碼在執行時，首先被創造的會是：

```
{
    Global EC, this, (window or global)
}
```

接著

```
{
    a()
}

{
    Global EC, this, (window or global)
}
```

接著

```
{
    b()
}

{
    a()
}

{
    Global EC, this, (window or global)
}
```

Call Stack 是一個 FILO 的環境

要注意，JavaScript 是同步執行的，就算`b()` 底下有 `var c`，他也會等 `b()` 執行完之後才去宣告 `var c`

## 函數，環境，與變數環境 (Scope)

```js
function b() {
    var myVar
}

function a() {
    var myVar = 2
    b()
}

var myVar = 1
a()
```

`myVar` 的值會是什麼？

最外層的會是 `1`，`a` 裡面的會是 `2`，`b` 裡面的會是 `undefined`

`var` 宣告的變數，會以 function 為 Scope

所以雖然 `myVar` 被宣告三次，但是他們彼此是不會互相影響的。

