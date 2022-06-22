# LeetCode 刷题预备知识



## 时间复杂度

### 一. 大 O 表示法

关于复杂度的计算，我们采用的是 **大 O 表示法** ，它用来描述算法性能和复杂程度

常见的表示

| 符号大O标记法  | 名称       |
| -------------- | ---------- |
| **O(1)**       | 常数       |
| **O(log N)**   | 对数       |
| **O(N)**       | 线性       |
| **O(N log N)** | 对数多项式 |
| **O(N^2)**     | 二次       |
| **O(2^N)**     | 指数       |
| **O(N!)**      | 阶乘       |

大 O 表示法一般考虑的是 `CPU` 占用时间，它可以粗略的了解代码运行的时间效率

例如

```js
function test(num){
	return ++num;
}
```

我们调用这个函数一次，执行时间是 `t` ，我们再调用一次，执行时间还是 `t`，和传入的参数无关， `test` 函数的性能都一样，因此它的复杂度为 `O(1)`

当循环 `n` 次时，就是 `O(n)`

### 二. 时间复杂度

大 `O` 表示法表明的是该段代码执行时间随数据规模增大的变化趋势，它的特点是

- 只关注量级最大的时间复杂度

常见的时间复杂度量级 `O(1) < O(logn) < O(n) < O(n^2)`

对于 `O(2)、O(3)` 这些，我们都叫做 `O(1)` 常数级

例如：

#### 1. O(1)

```js
let i = 0;
i += 1;
// 每次执行代码只执行一次 O(1)
```

这段代码每次只执行一次，因此为 `O(1)`

#### 2. O(n)

```js
for (let j = 0; j < n; j++) {
    console.log(j);
}
```

再上面这段代码中，我们每次都需要执行 `n` 次的 `log` ，因此我们可以把它看作 `O(n)`

同样的我们再来看一个

```js
let i = 0;
i += 1;
for (let j = 0; j < navigator; j++) {
    console.log(j);
}
```

这种代码我们经常写，前面是我们刚刚计算的 `O(1)`，后面是 `O(n)` ，它们并行排列，时间复杂度相加，取最大的那个

- 因此它的时间复杂度同样是 `O(n)`

#### 3. O(log(n))

```js
while (i < n) {
    console.log(i);
    i *= 2;
}
```

对于 `log(n)` 的情况，在个时间复杂度是很好的，当然 `O(1)` 是最好的，但是在解题的时候，如果能优化到 `log(n)` 也是很不错的了

那它是如何计算的呢？

我们可以看到，这里采用了 变量`i`来控制循环的终止，每次循环体中，都需要 `2 * i` 的操作

因此对于时间复杂度的计算 `2^t = n` 解得 `t = log(n)`

#### 4. O(n^2)

```js
for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
        console.log(i);
    }
}
```

对于这种嵌套排列，时间复杂度是 `n^2` ，外面一层 `n` ，里面一层 `n` 乘一下就是 `n^2`，冒泡排序的时间复杂度就是 `O(n^2)`

关于时间复杂度就介绍这么多，其他的思路都差不多

![image-20211029161002646](https://ljcimg.oss-cn-beijing.aliyuncs.com/img/image-20211029161002646.png)


## 空间复杂度

空间复杂度表示的是：存储空间随数据规模的增长趋势，在 `LeetCode` 中最直接的反应就是**内存消耗**

例如

#### 1. O(1)

```js
let i = 0;
```


在这里我们申请了单个变量的内存空间，为 `O(1)`

#### 2. O(n)

```js
let arr = []
for(let i = 0;i < n;i++) {
    arr.push(i)
}
```



像这样的一个数组，并给它填满值，`n` 越大，它需要分配的空间就越多，它的空间复杂度就是 `O(n)`

#### 3. O(n^2)

```js
int arr = [][]
// 遍历赋值
```



声明一个二维数组，填满值，它的空间复杂度就是 `O(n^2)` ，你可以理解为一个矩阵，`n*n` 为 `n^2`

### 📌 总结

1. 复杂度计算按最高阶来计算
2. 时间、空间复杂度描述的都是随数据规模的变化趋势
3. 时间复杂度的重点在于循环嵌套
4. 空间复杂度关注于内存


## 链表基础知识

- 链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。
- 链表由一系列结点（链表中每一个元素称为结点）组成，结点可以在运行时动态生成。每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。 
- 相比于线性表顺序结构，操作复杂。由于不必须按顺序存储，链表在插入的时候可以达到O(1)的复杂度，比另一种线性表顺序表快得多，但是查找一个节点或者访问特定编号的节点则需要O(n)的时间，而线性表和顺序表相应的时间复杂度分别是O(logn)和O(1)。

- 使用链表结构可以克服数组链表需要预先知道数据大小的缺点，链表结构可以充分利用计算机内存空间，实现灵活的内存动态管理。
- 但是链表失去了数组随机读取的优点，同时链表由于增加了结点的指针域，空间开销比较大。链表最明显的好处就是，常规数组排列关联项目的方式可能不同于这些数据项目在记忆体或磁盘上顺序，数据的存取往往要在不同的排列顺序中转换。
- 链表允许插入和移除表上任意位置上的节点，但是不允许随机存取。
- 链表有很多种不同的类型：单向链表，双向链表以及循环链表。

## 二叉树(BT,Binary Tree)

### 满二叉树(Full Binary Tree)

- 叶子结点只能出现在最下层，其他层所有结点均有左子树和右子树，且所有层都达到该层能拥有的最大结点树数。它是完全二叉树的一种特殊情况。

**官方定义：** 如果一颗二叉树的结点要么是叶子结点，要么他有两个子结点，这样的树就是满二叉树。

### 完全二叉树(Complete Binary Tree)

- 叶子结点只能出现在最下层和次下层，其他层所有结点均有左子树和右子树，且最下层的叶子结点集中在树的左部。

**官方定义：** 一颗深度为h的有n个结点的二叉树，对树中的结点按从上至下、从左到右的顺序进行编号，如果编号为i的结点与满二叉树中编号为i的结点在二叉树中的位置相同，则这颗二叉树称为完全二叉树。

## 二叉搜索树(BST,Binary Search Tree)

- 每个结点的左子树中所有结点的值均小于该结点的值，右子树中所有结点的值均大于该结点。

## 二分搜索基础知识

**练习：** 

给定一个 `n`个元素有序的（升序）整型数组 `nums` 和一个目标值 `target ` ，写一个函数搜索 `nums` 中的` target`，如果目标值存在返回下标，否则返回 -1。

**示例 1:**

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

**示例 2:**

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

### 法一：

```javascript
var search = function(nums, target) {
    //定义左指针和右指针分别指向开头和结尾
    let left =0, right = nums.length - 1;
    //当left<=right
    while(left <= right){
        //mid=(left+right)/2,之所以写成下面的形式是防止超出整型范围，防止溢出。
        mid = Math.floor(left + (right - left)/2);
        //如果找到了，就输出
        if(nums[mid] == target){
            return  mid;
            //如果目标比mid小，要把右半边舍弃
        }else if(target < nums[mid]){
            right = mid - 1;//mid以及mid右边都舍弃
        //如果目标比mid大，要把左半边舍弃
        }else{
            left = mid + 1;//mid以及mid左半边都舍弃
        }
    }
    //没找到输出-1
    return -1;
};
```

## Set基础知识

```javascript
//创建一个Set
const numberSet = new Set();
//添加，set不会添加重复的值
numberSet.add(1);
//删除,成功返回ture，失败返回false
numberSet.delete(1);
//判断set里是否有这个值，有返回ture，没有返回false
numberSet.has(1);
//输出set里有几个元素
numberSet.size
//遍历set中所有元素
numberSet.forEach(number=> console.log(number))
//
console.log(numberSet);
```

**练习：** 

```javascript
//1.判断下面这段代码最终输出的值
const set = new Set();
set.add(1);
set.add(1);
set.add("1");
console.log(set)
输出：{1,"1"}
```

## Map基础知识

```javascript
//创建一个Map
const person = new Map();
//添加,如果重复set，会覆盖原来的值
person.set("name","milo");
person.set("age",18);
person.set("hooby",["看老毕和鱼皮的视频","睡觉","打CSGO"])
//删除,成功返回ture，失败返回false
person.delete("age")
//获取Map里的某个值
person.get("name");
//判断set里是否有这个值，有返回ture，没有返回false
person.has("age");
//输出set里有几个元素
person.size
//遍历set中所有元素
person.forEach(person=> console.log(person))
//
console.log(person);
```

**练习：** 

```javascript
//2.创建一个map，并且添加如下数据：1:“北京”，2:“上海”，3:“杭州”，（0，1，2均为数字）。然后删除掉第一个元素。
const cities = new Map();
cities.set(1,"北京");
cities.set(2,"上海");
cities.set(3,"杭州");
console.log(cities);
输出：{1 => '北京', 2 => '上海', 3 => '杭州'}
cities.delete(1);
console.log(cities);
输出：{2 => '上海', 3 => '杭州'}
```

## let和const

#### let和const的区别：

Let可以重新赋值，Const不可以。

```javascript
var a = 1;
console.log(a);

var b = "hello";
console.log(b);

//let可以重新赋值
let c = 10;
c = c + 1 ;
console.log(c);
//const不可以重新赋值。会报错
const d = "hello";
d = d + "world";
console.log(d);
```

#### var和let、const的区别：

- var成功重复声明变量，let和const不可以

```javascript
var productPrice = 5.99;
// line 1000
var productPrice = 9.99; //重复声明了变量
// line 5000

productPrice++;
console.log(productPrice);
输出：10.99
```

- var的作用域范围是函数作用域范围

```javascript
var price =1;
function setPrice() {
    price++;
} 
setPrice();
console.log(price)
输出：2
```

```javascript
function setPrice() {
    var price =1;  //而把var写在函数里面，外面的console.log就识别不到var
    price++;
} 
setPrice();
console.log(price)
输出：Uncaught ReferenceError: price is not defined 
```

```javascript
var price =1;
function setPrice() {
    var price = 10;
    console.log(price);  //var是函数作用域，所以这个console能访问到外面的也能访问到函数里的price
  	console.log(window.price); //访问全局的price
} 
setPrice();
console.log(price)
输出：10 1 1
```

- let和const的作用域范围是块作用域

```javascript
for(var i = 0; i < 5; i++) {}
console.log(i)
//var是函数作用域，而for是块不是函数，所以var的i出了for这个块作用域，依然占用这个变量名，局部变量造成了全局污染。
输出：5
```

```javascript
for(let i = 0; i < 5; i++) {}
console.log(i)
//let是块作用域，就解决了局部变量污染全局变量的问题。
输出：Uncaught ReferenceError: i is not defined
```

```javascript
const price = 10;
if(price < 59){
    const deliverFee = 5;
    price += deliverFee;
}
console.log(price);
输出：Uncaught TypeError: Assignment to constant variable.
解释：const不能重新赋值
```

```javascript
let price = 10;
if(price < 59){
    const deliverFee = 5;
    price += deliverFee;
}
console.log(price);
console.log(deliverFee);
输出：15
Uncaught TypeError: Assignment to constant variable.
解释：let可以重复赋值,const是块作用域，所以最后一个console无法访问deliverFee
```

**练习：** 

- 第一题：用let或const改写这段使用var的旧程序

```javascript
var subtotal = 19.9;
var tax = 0.13;
var total = subtotal * ( 1 + tax);
console.log(total)
输出：22.487
```

```javascript
const subtotal = 19.9;
const tax = 0.13;
const total = subtotal * ( 1 + tax);
console.log(total)
输出：22.487
```

```javascript
let subtotal = 19.9;
let tax = 0.13;
let total = subtotal * ( 1 + tax);
console.log(total)
输出：22.487
```
**练习：** 

- 第二题：用let或const改写这段使用var的旧程序（注意函数作用域和块作用域的区别，必要时需要改变部分代码）

- 如果成绩哎60分以上，则课程pass

```javascript
var point = 95;
if(point >= 60){
    var pass = true;
}
console.log(pass);
输出：true
```

```javascript
let point = 95;
let pass = false;
if(point >= 60){
    pass = true;
}
console.log(pass);
输出：true
```

```javascript
let point = 95;
if(point >= 60){
    pass = true;
    console.log(pass);
}
输出：true
```


