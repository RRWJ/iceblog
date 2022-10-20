---
layout: post
title: median of two sorted arrays
date: 2022-10-18
tags: [leetcode]
comments: false
---
解题思路：
先排序再取中位数
```
package com.company.sort;

public class medianOfTwoSortedArrays {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int[] num3 = new int[nums1.length + nums2.length];
        int k = 0;
        int i = 0;
        int j = 0;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] <= nums2[j]) {
                num3[k] = nums1[i];
                i++;
                k++;
            } else {
                num3[k] = nums2[j];
                j++;
                k++;
            }
        }
        while (i < nums1.length) {
            num3[k++] = nums1[i++];
        }
        while (j < nums2.length) {
            num3[k++] = nums2[j++];
        }
        if (num3.length % 2 == 0) {
            return ((double) (num3[num3.length / 2] + num3[num3.length / 2 - 1]) / 2);
        } else {
            return (double) num3[num3.length / 2];
        }
    }

    public static void main(String[] args) {
        medianOfTwoSortedArrays medianOfTwoSortedArrays = new medianOfTwoSortedArrays();
        int[] nums1 = {1, 2};
        int[] nums2 = {3, 4};
        System.out.println(medianOfTwoSortedArrays.findMedianSortedArrays(nums1, nums2));
    }
}

```