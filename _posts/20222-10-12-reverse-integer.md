---
layout: post
title: reverse integer
date: 2022-10-12
tags: [leetcode]
comments: false
---
整数反转：需要特别注意的情况是数据越界
参考答案之后：
1. 采取的方法是用try-catch捕获异常
2. 把整数反转问题转化为字符串反转，用stringbuffer库函数
```
package com.company.str;

public class reverseInteger {
    public int reverse(int x) {
        String s = Integer.toString(x);
        boolean flag = true;
        if (s.charAt(0) == '-') {
            s = s.substring(1, s.length()-1);
            flag = false;
        }
        StringBuffer sb = new StringBuffer(s);
        try {
            String result = sb.reverse().toString();
            if (!flag) {
                StringBuffer res = new StringBuffer();
                res.append("-").append(result);
                return Integer.parseInt(res.toString());
            }
            return Integer.parseInt(result);
        } catch (Exception e) {
            return 0;
        }
    }

    public static void main(String[] args) {
        reverseInteger reverseInteger = new reverseInteger();
        int x = -150;
        System.out.println(reverseInteger.reverse(x));
    }
}

```