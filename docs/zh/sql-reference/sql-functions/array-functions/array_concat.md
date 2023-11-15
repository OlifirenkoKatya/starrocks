# array_concat

## 功能

将多个数组拼接成一个数组。拼接后的数组包含多个数组里的所有元素。待拼接的数组元素类型可以相同，也可以不同，但是建议对相同元素类型的数组进行拼接。

NULL 值会作为正常值处理。

## 语法

```Haskell
array_concat(input0, input1, ...)
```

## 参数说明

`input`：表示不限数量、具有相同元素类型的数组。数组元素可以是以下数据类型：BOOLEAN、TINYINT、SMALLINT、INT、BIGINT、LARGEINT、FLOAT、DOUBLE、DECIMALV2、VARCHAR、DATETIME、DATE、JSON。**从 2.5 版本开始，该函数支持 JSON 类型的数组元素。**

## 返回值说明

返回 (input0, input1, ...) 中所有元素有序拼接后的数组。

返回的数组元素类型与 `input` 中数组的元素类型一致。

## 示例

**示例一：对数值元素的数组进行拼接。**

```plain text
mysql> select array_concat([57.73,97.32,128.55,null,324.2], [3], [5]) as res;
+-------------------------------------+
| res                                 |
+-------------------------------------+
| [57.73,97.32,128.55,null,324.2,3,5] |
+-------------------------------------+
```

**示例二：对字符串元素的数组进行拼接。**

```plain text
mysql> select array_concat(["sql","storage","execute"], ["Query"], ["Vectorized", "cbo"]);
+----------------------------------------------------------------------------+
| array_concat(['sql','storage','execute'], ['Query'], ['Vectorized','cbo']) |
+----------------------------------------------------------------------------+
| ["sql","storage","execute","Query","Vectorized","cbo"]                     |
+----------------------------------------------------------------------------+
```

**示例三：对不同元素类型的数组进行拼接。**

```Plain_Text
select array_concat([57,65], ["pear","apple"]);
+-------------------------------------------+
| array_concat([57, 65], ['pear', 'apple']) |
+-------------------------------------------+
| ["57","65","pear","apple"]                |
+-------------------------------------------+
```

**示例四：null作为正常值处理。**

```plain text
mysql> select array_concat(["sql",null], [null], ["Vectorized", null]);
+---------------------------------------------------------+
| array_concat(['sql',NULL], [NULL], ['Vectorized',NULL]) |
+---------------------------------------------------------+
| ["sql",null,null,"Vectorized",null]                     |
+---------------------------------------------------------+
```