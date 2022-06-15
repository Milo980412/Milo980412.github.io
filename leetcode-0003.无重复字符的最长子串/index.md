# 力扣 0003.无重复字符的最长子串


## 3.无重复字符的最长子串
{{< admonition question >}}
给定一个字符串`s`,请你找出其中不含有重复字符的最长子串的长度。
{{< /admonition >}}

**示例1:**

```
输入: s = "abcabcbb"
输出: 3
解释:因为无重复字符的最长子串是"abo",所以其长度为3。
```

**示例2:**

```
输入: s="bbbbb"
输出: 1
解释:因为无重复字符的最长子串是"b",所以其长度为1。
```

**示例3:**

```
输入: s="pwwkew"
输出: 3
解释:因为无重复字符的最长子串是"wke",所以其长度为3。
请注意,你的答案必须是子串的长度,"pwke"是一个子序列,不是子
串。
```

### 法一：滑动窗口+哈希集合判断重复

```javascript
var lengthOfLongestSubstring = function(s) {
    let set = new Set();  //创建一个set集合
    let i = 0 ,j = 0;  //创建两个指针,i指针随着for循环遍历字符串，j指针指向字符串的开头,即滑动窗口
    let maxLength = 0;  //记录最大长度
    if(s.length === 0){
        return 0;
    }
    for(let i = 0; i< s.length; i++){  
        if(!set.has(s[i])){  //如果set理没有s[i]，说明目前为止没有重复的字符
            set.add(s[i]);  //把它添加到set里
            maxLength = Math.max(maxLength,set.size);  //更新最大不重复字符的数量，如果比之前大就更新
        }else{
            while(set.has(s[i])){  //如果set里有s[i]，开始以下操作，直到set里没有s[i]为止
                set.delete(s[j]);  //从set里开始删除s[j]
                j++;  //并且开始递增j，即把j指针右移
            }
            set.add(s[i]);  //set里没有之前重复的s[i]后，添加新的s[i],开始新的一轮
        }
    }
    return maxLength;  //输出不含有重复字符的最长子串的长度
};
```
- **时间复杂度：** O(N)，N是字符串的长度，两个指针分别会遍历整个字符串一次。

- **空间复杂度：** O(∣Σ∣)，字符集这里默认为ASCII码，即[0,128),所以字符集大小为128。

- 创建一个set集合。

- 创建两个指针,i指针随着for循环遍历字符串，j指针指向字符串的开头,即滑动窗口。

- 如果set理没有s[i]，说明目前为止没有重复的字符，把它添加到set里，然后更新最大不重复字符的数量，如果比之前大就更新。

- 如果set里有s[i]，则从set里开始删除s[j]，并且开始递增j，即把j指针右移，直到set里没有s[i]为止，添加新的s[i],开始新的一轮。

- 直到遍历完整个字符串，最后输出最大不重复字符的数量。

### 法二：官方答案

```javascript
var lengthOfLongestSubstring = function(s) {
    // 哈希集合，记录每个字符是否出现过
    const occ = new Set();
    const n = s.length;
    // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
    let rk = -1, ans = 0;
    for (let i = 0; i < n; ++i) {
        if (i != 0) {
            // 左指针向右移动一格，移除一个字符
            occ.delete(s.charAt(i - 1));
        }
        while (rk + 1 < n && !occ.has(s.charAt(rk + 1))) {
            // 不断地移动右指针
            occ.add(s.charAt(rk + 1));
            ++rk;
        }
        // 第 i 到 rk 个字符是一个极长的无重复字符子串
        ans = Math.max(ans, rk - i + 1);
    }
    return ans;
};
```
