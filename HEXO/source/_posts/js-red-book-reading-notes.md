---
title: JS红宝书读书笔记
date: 2017-09-04 11:24:01
tags: [前端, 随笔]
---
# 第三章 基本概念
## 数据类型
### 非数字转换成数字
有三个方法`Number()`，`parseInt()`，`parseFloat()`（其中一元`+`操作符与`Number()`函数相同）
<!--more-->
- `Number()`规则如下：
  >* 如果是Boolean值，true和false返回1和0
  >* 如果是null，返回0
  >* 如果是undefined，返回NaN
  >* 如果是String，则：
    - 字符串只有数字，`'123'`=>`123`，`'0000012'`=>`12`（前置0会被忽略）
    - 字符串包括浮点格式，则转为对应浮点数（也会忽略前置0）
    - 包含十六进制格式，则转为对应十进制，`'0xf'`=>`15`
    - 空字符串转换为0
    - 除上述格式之外，其他的转换为NaN
  >* 如果是对象，先调用`valueOf()`方法，然后按照前面规则来转换。如果返回结果是NaN，则调用`toString()`方法，然后依照前面的规则来转换返回值。
  >```javascript
  var num1 = Number("Hello World");      // NaN
  var num2 = Number("");                 // 0
  var num3 = Number("00000011");         // 11
  var num4 = Number("true");             // 1
  ```
- `parseInt()`在转换字符串时，更多的时看其是否符合数值模式。会忽略字符串前面的空格，直至找到第一个非空格字符。规则如下：
  >* 如果第一个字符不是数字字符或都负号，`parseInt()`就会返回NaN; 也就是说，用`parseInt()`转换空字符串会返回NaN。
  >* 如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。例如，`"1234blue"`会被转换为`1234`，因为`"blue"`会被完全忽略。类似地`"22.5"`会被转换为`22`，因为小数点不是有效的数字字符。
  >* 如果字符串以`"0x"`开头且后跟数字字符，就会将其当作一个十六进制整数；
  >* 如果字符串以`"0"`开头且后跟数字字符，就会将其当作一个八进制整数；
  >```javascript
  var num1 = parseInt("1234blue");      // 1234
  var num2 = parseInt("");              // NaN
  var num3 = parseInt("0xA");           // 10（十六进制）
  var num4 = parseInt("22.5");          // 22
  var num5 = parseInt("070");           // 56（八进制）
  var num6 = parseInt("70");            // 70（十进制）
  var num7 = parseInt("0xf");           // 15（十六进制）
  ```
  >* `parseInt()`函数增加了第二参数用于指定转换时使用的基数（即多少进制）如：`parseInt("10",16)//按十六进制解析；` `parseInt("10",8)//按八进制解析`
  >```javascript
  var num1 = parseInt("10", 2);         // 2
  var num2 = parseInt("10", 8);         // 8
  var num3 = parseInt("10", 10);        // 10
  var num4 = parseInt("10", 16);        // 16
  ```
- `parseFloat()`与`parseInt()`函数类似
  >* `parseFloat()`也是从第一个字符（位置0）形如解析每个字符，而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数点是有效的，而第二个小数点就是无效的了，因此它后面的字符串将被忽略。例如：`"22.34.5"`将会转换为`22.34`。
  >* `parseFloat()`始终都会忽略前导的零。`parseFloat()`可以识别前面讨论过的所有的浮点数值格式，也包括十进制整数格式。但十六进制格式的字符串则始终会被转换成0。**由于`parseFloat()`只解析十进制值，因此它没有用第二个参数指定基数的用法。**
  >* 另外，如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后面都是零），`parseFloat()`会返回整数。
  >```javascript
  var num1=parseFloat("1234blue");      // 1234
  var num2=parseFloat("0xA");           // 0
  var num3=parseFloat("0908.5");        // 908.5
  var num4=parseFloat("3.125e7");       // 31250000
  ```
### 转换成字符串
可以使用`toString()`，`String()`（其中`+""`与`String()`作用相同）
- 数字，布尔值，对象和字符串都有`toString()`方法，但是`null`和`undefined`没有这个方法。
- 在调用数字的`toString()`方法时，可以传递一个参数，让函数输出二进制、八进制、十六进制等。
- 在有`null`和`undefined`的情况下，可以用`String()`方法。`String(null);  // "null"`
