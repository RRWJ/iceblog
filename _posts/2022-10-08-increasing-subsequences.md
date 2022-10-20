---
layout: post
title: increasing subsequences
date: 2022-10-07
tags: [leetcode]
comments: false
---
491. 递增子序列
第一版代吗如下：
循环位置不同，遍历根节点的顺序不同
出现重复元素，如何回退
```
public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < nums.length; i++) {
            List<Integer> res = new ArrayList<>();
            res.add(nums[i]);
            res = dfs(i, i , nums, res);
            // 问题：如何回退
            result.add(res);
        }
        return result;
    }

    public List<Integer> dfs(int i, int j, int[] nums, List<Integer> res) {
        if (j > nums.length) return res;
        List<Integer> result = new ArrayList<>();
        if (j < nums.length && i < nums.length && j > i && nums[j] >= nums[i]) {
            res.add(nums[j]);
            res = dfs(i, j + 1, nums, res);
        }
        return res;
    }
```
```
input: [4, 6, 7, 7]
output: [[4, 6, 7, 7], [6, 7, 7], [7, 7], [7]]
```
参考正确答案
```
public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> res = new ArrayList<>();
        dfs(0, nums, result, res);
        return result;
    }

    public void dfs(int i, int[] nums, List<List<Integer>> result, List<Integer> res) {
        if (i > nums.length ) return;
        if (res.size() > 1) result.add(new ArrayList<>(res));
        Set<Integer> set = new HashSet<>();
        for (int j = i; j < nums.length; j++) {
            if (set.contains(nums[j])) break;
            if (res.size() == 0 || nums[j] >= res.get(res.size() - 1)) {
                set.add(nums[j]);
                res.add(nums[j]);
                dfs(j + 1, nums, result, res);
                res.remove(res.size() - 1);
            }
        }
    }
```