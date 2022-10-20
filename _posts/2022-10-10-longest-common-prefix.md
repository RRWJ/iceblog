---
layout: post
title: longest common prefix
date: 2022-10-10
tags: [leetcode]
comments: false
---
两个两个比较，返回公共字符串
```
package com.company.str;

import java.util.HashSet;
import java.util.Set;

public class longestCommonPrefix {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 1) return strs[0];
        Set<String> set = new HashSet<>();
        for (int i = 1; i< strs.length; i++){
            String s = findCommonPrefix(strs[0], strs[i]);
            set.add(s);
        }
        return set.iterator().next();
    }

    public String findCommonPrefix(String s1, String s2) {
        int i = 0;
        int j = 0;
        
        StringBuffer sb = new StringBuffer();
        while (i < s1.length() && j < s2.length()) {
            if(s1.charAt(i) == s2.charAt(j)){
                sb.append(s1.charAt(i));
            }
            i++;
            j++;
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        String[] strings = {"dog","racecar","car"};
        longestCommonPrefix longestCommonPrefix = new longestCommonPrefix();
        System.out.println(longestCommonPrefix.longestCommonPrefix(strings));
    }
}
```
```
input: ["cir","car"]
output: "cr"
```
存在问题：不连续 
解决方法：设置index标记位，标记相等字符串的前一个
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 1) return strs[0];
        Set<String> set = new HashSet<>();
        for (int i = 1; i< strs.length; i++){
            String s = findCommonPrefix(strs[0], strs[i]);
            set.add(s);
        }
        return set.iterator().next();
    }

    public String findCommonPrefix(String s1, String s2) {
        int i = 0;
        int j = 0;
        int index = -1;
        StringBuffer sb = new StringBuffer();
        while (i < s1.length() && j < s2.length()) {
            if(s1.charAt(i) == s2.charAt(j) && index+1 == i){
                sb.append(s1.charAt(i));
                index = i;
            }
            i++;
            j++;
        }
        return sb.toString();
    }
}
```
```
input:["abab","aba","abc"]
output:"aba"
```
存在问题：两两比较，只返回💰两个
解决方法：递归继续比较，set长度为1截止
```
public class longestCommonPrefix {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 1) return strs[0];
        Set<String> set = new HashSet<>();
        for (int i = 1; i< strs.length; i++){
            String s1 = findCommonPrefix(strs[0], strs[i]);
            set.add(s1);
        }
        if (set.size() == 1){
            return set.iterator().next();
        } else {
            return longestCommonPrefix(set.toArray(new String[set.size()]));
        }
    }

    public String findCommonPrefix(String s1, String s2) {
        int i = 0;
        int j = 0;
        int index = -1;
        StringBuffer sb = new StringBuffer();
        while (i < s1.length() && j < s2.length()) {
            if(s1.charAt(i) == s2.charAt(j) && index+1 == i){
                sb.append(s1.charAt(i));
                index = i;
            }
            i++;
            j++;
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        String[] strings = {"abab","aba","abc"};
        longestCommonPrefix longestCommonPrefix = new longestCommonPrefix();
        System.out.println(longestCommonPrefix.longestCommonPrefix(strings));
    }
}

```
😁看答案后，纵向/垂直比较😄
```
public String longestCommonPrefix(String[] strs) {
        if (strs.length == 1) return strs[0];
        Set<String> set = new HashSet<>();
        for (int i = 1; i< strs.length; i++){
            String s1 = findCommonPrefix(strs[0], strs[i]);
            set.add(s1);
        }
        if (set.size() == 1){
            return set.iterator().next();
        } else {
            return longestCommonPrefix(set.toArray(new String[set.size()]));
        }
    }
```