## Syntax parser

JS 沒有厲害到讓電腦去了解，是因為有另一個程式把你的 JS 轉成另一種電腦可以讀的語言。

Syntax parser 會先把你的程式碼切成一顆一顆的，比如說 function -> 會被切成好幾個字元。

這個會把你 JS 轉換成給電腦看得程式，通常稱作編譯器和直譯器，在執行的時候一定會有他們的存在。

而 Parser 是其中的一部分

## LEXICAL ENVIRONMENT

儘管不是所有程式碼都這樣，但 JS 的確是那種你把程式碼寫在哪裏，他實際就會在電腦記憶體的哪裏。

所以詞彙環境其實就是在討論這段程式碼被寫在哪裏

## Execution Context

我們有許多的詞彙環境，但是哪些是正在執行的呢？這些就是由執行環境去處理的，當你的程式碼一個部分一個部分被解析，被執行時，EC 還可以多做一些有趣的事情。



