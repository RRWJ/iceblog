---
layout: post
title: generate parentheses
date: 2022-10-09
tags: [leetcode]
comments: false
---
昨晚做完491. 递增子序列后，趁热打铁，继续跟进回溯算法
按照模版写出了第一版代码：
```
package com.company.backtrace;

import java.util.ArrayList;
import java.util.List;

public class generateParenthesis {
    public List<String> generateParenthesis(int n) {
        String[] kuohao = {"(", ")"};
        List<String> result = new ArrayList<>();
        dfs(0, new StringBuffer(), 0, 0, n, result, kuohao);
        return result;
    }

    public void dfs(int index, StringBuffer sb, int leftNum, int rightNum, int n, List<String> result, String[] kuohao) {
        if (index > 2*n) return;
        if (sb.length() != 0 && leftNum == n && rightNum == n) result.add(sb.toString());
        for (int i = 0; i < kuohao.length; i++) {
            if (sb.length() == 0 || leftNum < n) {
                sb.append(kuohao[0]);
                leftNum++;
                dfs(index + 1, sb, leftNum, rightNum, n, result, kuohao);
                sb.deleteCharAt(sb.length() - 1);
                leftNum--;
            }
            if (rightNum < leftNum) {
                sb.append(kuohao[1]);
                rightNum++;
                dfs(index + 1, sb, leftNum, rightNum, n, result, kuohao);
                sb.deleteCharAt(sb.length() - 1);
                rightNum--;
            }
        }
    }

    public static void main(String[] args) {
        generateParenthesis generateParenthesis = new generateParenthesis();
        int n = 3;
        System.out.println(generateParenthesis.generateParenthesis(n));
    }
}
```
```
input: 3
output: [((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ((())), ((())), ((())), ((())), ((())), ((())), ((())), ((())), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), (()()), (()()), (()()), (()()), (())(), (())(), (())(), (())(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()(), ()(()), ()(()), ()(()), ()(()), ()()(), ()()(), ()()(), ()()()]
```
问题总结：
重复输出的问题-> 可能出现在 for循环/index > 2*n 这部分
修改for循环后：
```
public List<String> generateParenthesis(int n) {
        String[] kuohao = {"(", ")"};
        List<String> result = new ArrayList<>();
        dfs(0, new StringBuffer(), 0, 0, n, result, kuohao);
        return result;
    }

    public void dfs(int index, StringBuffer sb, int leftNum, int rightNum, int n, List<String> result, String[] kuohao) {
        if (index > 2*n) return;
        if (sb.length() != 0 && leftNum == n && rightNum == n) result.add(sb.toString());
        if (sb.length() == 0 || leftNum < n) {
            sb.append(kuohao[0]);
            leftNum++;
            dfs(index + 1, sb, leftNum, rightNum, n, result, kuohao);
            sb.deleteCharAt(sb.length() - 1);
            leftNum--;
        }
        if (rightNum < leftNum) {
            sb.append(kuohao[1]);
            rightNum++;
            dfs(index + 1, sb, leftNum, rightNum, n, result, kuohao);
            sb.deleteCharAt(sb.length() - 1);
            rightNum--;
        }
    }
```