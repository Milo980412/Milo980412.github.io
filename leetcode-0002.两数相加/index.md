# 力扣 0002.两数相加


## 2.两数相加
{{< admonition question >}}
- 给你两个非空的链表,表示两个非负的整数。它们每位数字都是按照逆序的方式存储的,并且每个节点只能存储一位数字。
- 请你将两个数相加,并以相同形式返回一个表示和的链表。
{{< /admonition >}}
{{< admonition info >}}
- 你可以假设除了数字0之外,这两个数都不会以0开头。
{{< /admonition >}}

**示例1:**

```
输入: L1 = [2,4,3], L2 = [5,6,4]
输出: [7,0,8]
解释: 342 + 465 = 807.
```

**示例2:**

```
输入: L1= [0], L2 = [0]
输出: [0]
```

**示例3:**

```
输入: L1 = [9,9,9,9,9,9,9], L2 = [9,9,9,9]
输出: [8,9,9,9,0,0,0,1]
```

## 法一：利用官方构造函数设置结点


```javascript
var addTwoNumbers = function(l1, l2) {
    let head = new ListNode();  //创建一个新结点head
    let tail = head;  //head和tail都在新结点的位置
    let carry = 0;  //进位carry初始化为0
    //同时遍历l1和l2直至到达它们的尾端 
    while(l1 != null || l2 != null){  
        let sum = 0;
        if(l1 != null){  
            sum += l1.val;  //计算相同位置的和
            l1 = l1.next;  //将l1前进到下一个结点
        }
        if(l2 != null){  
            sum += l2.val;  //计算相同位置的和
            l2 = l2.next;  //将l2前进到下一个结点
        }
        sum += carry;  //与当前位置的进位值相加
        tail.next = new ListNode(sum % 10)  //创建一个数值为sum%10 取模的新结点，并将其设置为当前结点的下一个结点，答案链表处相应的数字为(n1+n2+carry)%10
        carry = Math.floor(sum / 10);  //新的进位符为(n1+n2+carry)/10 取整  
        tail = tail.next;  //将当前结点前进到下一个结点
    }
    if(carry > 0){
        tail.next = new ListNode(carry);  //检查carry是否存在进位，是则添加一个数值为carry的新结点
    }
    return head.next;
}
```
- **时间复杂度：** O(max(m,n))，其中m和n分别为两个链表的长度，我们要遍历两个链表的全部位置，而处理每个位置只需要O(1)时间。

- **空间复杂度：** O(1)，返回值不计入空间复杂度。

- 由于输入的两个链表都是逆序存储数字的位数的，因此两个链表中同一位置的数字可以直接相加。

- 我们同时遍历两个链表，逐位计算它们的和，并与当前位置的进位值相加。

- 创建一个数值为sum%10 取模的新结点tail，并将其设置为当前结点的下一个结点，答案链表处相应的数字为(n1+n2+carry)%10

- 新的进位符为(n1+n2+carry)/10 取整  

- 此外，链表遍历结束后，检查carry是否存在进位，是则添加一个数值为carry的新结点

### 官方构造函数

```javascript
function ListNode(val, next) {
  this.val = val === undefined ? 0 : val
  this.next = next === undefined ? null : next
}
```

利用构造函数，生成结点，把链表里的数存进去

```javascript
tail.next = new ListNode(sum % 10)
```

## 法二：官方答案

```javascript
var addTwoNumbers = function(l1, l2) {
    let head = null, tail = null;  //当前结点初始化为空结点
    let carry = 0;  //进位carry初始化为0
    while(l1 != null || l2 != null){  //同时遍历l1和l2直至到达它们的尾端
        const n1 = l1 ? l1.val : 0;
        const n2 = l2 ? l2.val : 0;
        const sum = n1 + n2 +carry;  //逐位计算相同位置的和，并与当前位置的进位值相加
        if(!head){
            head = tail = new ListNode(sum % 10);  //让head停在第一个结点的位置，tail同下
        }else{
            tail.next = new ListNode(sum % 10);  //创建一个数值为sum%10 取模的新结点，答案链表处相应的数字为(n1+n2+carry)%10
            tail = tail.next;  //将当前结点前进到下一个结点
        }
        carry = Math.floor(sum / 10);  //新的进位符为(n1+n2+carry)/10 取整
        if(l1){
            l1 = l1.next;  //将l1前进到下一个结点
        }
        if(l2){
            l2 = l2.next;  //将l1前进到下一个结点
        }
    }
    if(carry > 0){
        tail.next = new ListNode(carry);
    }
    return head;
};
```
