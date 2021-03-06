# TypeScript
https://www.tslang.cn/docs/handbook/basic-types.html

## ES5, ES2015（ES6） 和 TypeScript的关系
![ES5, ES2015（ES6） 和 TypeScript的关系](http://p8.qhimg.com/t01e695dbf2438846f7.gif)
ES5,ES2015(ES6)都是JavaScript的标准,JavaScript是实现。
ES5代指实现了ES5的JavaScript，即上一代JavaScript。
ES6代指实现了ES6的JavaScript，即下一代JavaScript。

TypeScript是ES6的超集,扩展了 JavaScript 的语法，因此现有的 JavaScript 代码可与 TypeScript 一起工作无需任何修改，
TypeScript 通过类型注解提供编译时的静态类型检查。

TypeScript 是一种给 JavaScript 添加特性的语言扩展。增加的功能包括：
- 类型批注和编译时类型检查
- 类型推断
- 类型擦除
- 接口
- 枚举
- Mixin
- 泛型编程
- 名字空间
- 元组
- Await

以下功能是从 ECMA 2015 反向移植而来：
- 类
- 模块
- lambda 函数的箭头语法
- 可选参数以及默认参数


### 类型批注和编译时类型检查
TS通过类型批注提供静态类型，在编译时进行类型检查。类型批注并不是必须的。
类型批注语法  变量名:类型 
```javacsript
// let num:number = "10";
// error TS2322: Type '"10"' is not assignable to type 'number'.
let num:number = 10;
let str:string = "10";
let obj:Object = "10";
let anyType:any = "10";
```

### 元组
元组和数组的区别是元组允许存放不同数据类型的数据。
元组必须事先确定元素个数，以及各元素的类型。
```javascript
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
Type 'number' is not assignable to type 'string'.
Type 'string' is not assignable to type 'number'.

x[3] = "world"; // Error, Property '3' does not exist on type '[string, number]'.

console.log(x[5].toString()); // Error, Property '5' does not exist on type '[string, number]'.
```

### 枚举
enum类型和C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。
```javascript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```
默认情况下，从0开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从 1开始编号：
```javascript
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
```
或者，全部都采用手动赋值：
```javascript
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```
枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：
```javascript
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
```

### 接口
TypeScript的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 
在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

```javascript
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
// printLabel(size: 10, label: "Size 10 Object");
// Object literal may only specify known properties, and 'label' does not exist in type 'LabelledValue'
// 对于匿名对象会进行额外的属性检查？
```
类型检查器会查看printLabel的调用。 printLabel有一个参数，并要求这个对象参数有一个名为label类型为string的属性。
当该属性不存在，或者类型不为string将会报错。

可选属性
可选属性定义就是在属性名字后面加一个?符号。
```javascript
interface SquareConfig {
  color?: string;
  width?: number;
}
```
可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。 

只读属性
一些对象属性只能在对象刚刚创建的时候修改其值。定义只读属性，用`readonly`
```javascript
interface Point {
    readonly x: number;
    readonly y: number;
}

let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!

function printValue(p:Point) {
	// p.x = "15";
	// Cannot assign to 'x' because it is a read-only property.
	console.log(p.x);
	console.log(p.y);
};
```
额外的属性检查




















































