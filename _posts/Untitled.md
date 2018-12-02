---
layout:     post
title:      顺时针打印矩阵
subtitle:   剑指offer-牛客网
date:       2018-12-02
author:     Y.
catalog: true
tags:
    - 剑指offer  
    - 矩阵



---

# 顺时针打印矩阵

## 题目描述  

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

时间限制：1秒 空间限制：32768K  

## 代码  

```javascript  
function printMatrix(matrix)
{
    // write code here
    var result = [];
    var row = matrix.length;
    var col = matrix[0].length;
    
    var cycle = Math.min(col, row);
    cycle = Math.ceil(cycle / 2);
    
    function printOneCycle(matrix, init, colNumber, rowNumber, result) {
        for(var j = 0; j < colNumber; j++) {
            result.push(matrix[init][init + j]);
        }
        if(rowNumber > 1) {
            for(var i = 0; i < rowNumber - 1; i++ ) {
                result.push(matrix[init + i + 1][init + colNumber - 1]);
            }   
        }
        if(rowNumber > 1 && colNumber > 1) {
            for(var j = 0; j < colNumber - 1; j++ ) {
                result.push(matrix[init + rowNumber - 1][init + colNumber - 1 - j - 1]);
            }
        }
        if(rowNumber > 2 && colNumber > 1) {
            for(var i = 0; i < rowNumber - 2; i++ ) {
                result.push(matrix[init + rowNumber - 1 - i - 1][init]);
            }
        }
    }
    
    for(let i = 0; i < cycle; i++) {
        printOneCycle(matrix, i, col - i * 2, row - i * 2, result);
    }
    return result;
}
```

解题思路：

1. 确定共需几步，及起始点的位置
2. 正常情况为4步，必有第一步，那么剩余步骤出现的条件是什么要想清楚
3. 以及除第一步外，输出节点的数目也要确定