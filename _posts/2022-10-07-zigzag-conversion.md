---
layout: post
title: zigzag conversion
date: 2022-10-07
tags: [leetcode]
comments: false
---
6. Z 字形变换
```
public class zShapeTransform {
    public String convert(String s, int numRows) {
        if (s.length() == 1 || numRows == 1) {
            return s;
        }
        int gapLength = 2 * numRows - 2;
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < numRows; i++) {
            StringBuffer sb1 = new StringBuffer();
            for (int j = 0; j < s.length(); j++) {
                if (j % gapLength == i && j == gapLength - i) {
                    sb1.append(s.charAt(j));
                }
            }
            sb.append(sb1);
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        zShapeTransform zShapeTransform = new zShapeTransform();
        String s = "PAYPALISHIRING";
        int numRows = 3;
        System.out.println(zShapeTransform.convert(s, numRows));
    }
}
```
解题思路：
## 找规律

例如对一个4行的

0     6      12        18
1   5 7   11 13    17
2 4   8 10   14 16
3     9      15
对于n行的, s中的第i个字符：

对余数进行判断

i%(2n-2) == 0 ----> row0

i%(2n-2) == 1 & 2n-2-1 ----> row1

i%(2n-2) == 2 & 2n-2-2 ----> row2

...

i%(2n-2) == n-1 ----> row(n-1)