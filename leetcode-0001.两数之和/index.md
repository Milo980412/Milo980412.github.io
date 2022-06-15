# 力扣 0001.两数之和


## 1.两数之和
{{< admonition question >}}
- 给定一个整数数组 `nums` 和一个整数目标值 ` target`，请你在该数组中找出和为目标值 ` target`  的那两个整数，并返回它们的数组下标。
{{< /admonition >}}
{{< admonition info >}}
- 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

- 你可以按任意顺序返回答案。
{{< /admonition >}}

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

## 法一：暴力解法


```javascript
var twoSum = function(nums, target) {
    for(let i = 0,len = nums.length; i < len; i++){
        for(let j = i+1; j < len; j++){
            if((target - nums[i]) == nums[j]){
                return [i,j];
                }
        }
    }
    return [];
};
```

- **时间复杂度：** 
O(N2)，其中 N是数组中的元素数量。对于每一个元素 `x`，我们可以 O(1) 地寻找 `target - x`。两个循环，所以是O(N2)。

- **空间复杂度：** 
O(1)

- 简单粗暴,2遍for循环逐个遍历判断。

## 法二：哈希表（官方答案）


```javascript
var twoSum = function(nums, target) {
    let map = new Map();
    for(let i = 0; i < nums.length; i++){
        if(map.has(target - nums[i])){
            return [map.get(target - nums[i]),i];
        }else{
            map.set(nums[i],i);
        }
    }
    return [];
}
```
- **时间复杂度：** O(N)，其中 N是数组中的元素数量。对于每一个元素 `x`，我们可以 O(1) 地寻找 `target - x`。

- **空间复杂度：** O(N)，其中 N是数组中的元素数量。主要为哈希表的开销。
- 一遍for循环搞定,将数字存在哈希表的键值对中,并判断`target-nums[i]`的结果在哈希表键值对中是否存在,是则说明找到匹配数字。

- 我们遍历到数字a时,用target减去a,就会得到b,若b存在于哈希表中,我们就可以直接返回结果了。若b不存在,那么我们需要将a存入哈希表,好让后续遍历的数字使用。


