# Two Sum
## [题目](https://leetcode-cn.com/problems/two-sum/)
Given an array of integers `nums` and an integer `target`, return *indices* of the two numbers such that they add up to *`target`*. You may assume that each input would have **exactly one solution** and you may not use the same element twice. **You can return the answer in any order**.

## 解题思路
加法具有对称性。用一个map保存数字与下标的对应关系。顺序扫描数组，如果另一半数字在map中，直接取出下标；如果不在map中，将当前数字保存到map中。

## Python 
### Solution
```Python
from typing import List

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        mapping = {}
        for index, num in enumerate(nums):
            another_num = target - num
            if another_num in mapping:
                return [index, mapping[another_num]]
            mapping[num] = index
```

### typing类型提示支持
Python是动态类型语言，运行时不需要指定变量类型。Python3.5引入了一个类型系统，允许开发者指定变量类型，共IDE和各种开发工具使用，**对代码运行不产生影响**。
```python
def test(num: str):
    print(type(num))

if __name__ == '__main__':
    test('hi')
    test(1)
    test({})
```
运行结果：
```
<class 'str'>
<class 'int'>
<class 'dict'>
```
- 静态类型语言与动态类型语言的区别在于，变量的类型是否需要在编译之前就要确定，变量的类型在运行中是否可以改变。
- 静态类型语言的优点是可以进行编译期间检查，IDE的提示也会更到位；动态类型语言更灵活，写起来快，但是不便于检查错误

### 字典
- 既可以用花括号来创建字典，也可以用`dict()`函数来创建字典
- key必须是不可变类型
- 添加一个key-value时，直接以`dict[key] = value`形式指定即可。如果key不存在，则会新建；如果key已存在，则会覆盖原value
- 删除一个key-value的方式：`del dict[key]`; `del dict`会删除整个字典对象
- 判断字典是否包含指定的key，可以使用 `in` 和 `not in`运算符（是的，它们是运算符）。

### enumerate()函数
`enemurate()`函数用于将一个可遍历的数据对象（如列表，字典，元组，字符串,集合）组合为一个索引序列，格式为（索引，数据）。一般用在for循环中

### 列表
python列表中的元素不需要具有相同的类型；创建一个列表只需要把逗号分隔的不同数值的数据项使用方括号括起来即可。

## Go 
### Solution
```golang
package leetcode

func twoSum(nums []int, target int) []int{
	mapping := make(map[int]int)
	for i := 0; i < len(nums); i++{
		anotherNum := target - nums[i]
		if _, anotherNumIndex := mapping[anotherNum]; anotherNumIndex {
			return []int{i, mapping[anotherNum]}
		}
		mapping[nums[i]] = i
	}
	return nil
}
```

### go变量声明方式
1. `var idetifier type`， 可以一次声明多个变量：`var identifier1, identifier2 type`， 例如：`var a string = "hello"` 如果没有初始化变量值，默认初始化为0值
2. `var v_name = value`， 声明的同时初始化，此时可以省略类型，编译器会根据值自行判断变量类型
3. `v_name := value`，也是自动推断类型。但是这种形式只能在函数体中出现。注意`:=`左边如果没有声明新的变量，就会产生编译错误
4. `var(
	v_name1 type
	v_name2 type
	)`
	这种因式分解关键字的写法一般用于声明全局变量

### make函数
- new 和 make 是两个内置函数，主要用来创建并分配类型的内存。new 分配内存并返回指针，而 make 用于 slice、map 和 channel 的初始化并返回引用。

### Map
- Map的声明形式为map[key_type]value_type, 使用make创建
```golang
var countryCapitalMap map[String][string]
countryCapitalMap = make(map[string]string)
```
或者
```golang
countryCapitalMap := make(map[string]string)
```
也可以：
```golang
countryCapitalMap := map[string]string{"France": "Paris", "Italy": "Rome", "Japan": "Tokyo", "India": "New delhi"}
```
- map中添加元素与python类似

- map查找元素:
```golang
  value, isExist = map[key]
```
如果不存在该元素，则`isExist`为false

- map删除元素：
```golang
delete(map, key)
```
