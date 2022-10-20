---
layout: post
title: search a 2d matrix
date: 2022-10-19
tags: [leetcode]
comments: false
---
@description: 二维数组的二分查找！
做题时间 30min 已AC
```
public class searchaA2dMatrix {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = matrix.length;
        int col = matrix[0].length - 1;
        int i = 0;
        int j = col;
        while (i < row && j >= 0) {
            if (matrix[i][j] == target) {
                return true;
            } else if (target < matrix[i][j]) {
                j--;
            } else {
                i++;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        searchaA2dMatrix searchaA2dMatrix = new searchaA2dMatrix();
        int[][] matrix = {{1, 3, 5, 7}, {10, 11, 16, 20}, {23, 30, 34, 60}};
        int target = 23;
        System.out.println(searchaA2dMatrix.searchMatrix(matrix, target));
    }
}
```