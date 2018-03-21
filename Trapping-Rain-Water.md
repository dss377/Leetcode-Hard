题目：
==
 Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example,
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6. 

https://leetcode.com/static/images/problemset/rainwatertrap.png

分析：
==
题目大意：给出一个数组，每个元素表示长方体的高，这些长方体宽度为1，求这个数组的长方体组成的图形能蓄多少水。首先要明确，当前位置能蓄水的条件是两边的高度都高于当前位置。而被水填满后的形状是先升后降的塔形，所以，遍历一遍找到塔顶，然后分别从左右两边开始，往塔顶所在位置遍历，水位只增高不减，而且会一直和最近遇到的最大高度持平，这样我们可以知道实时水位，就可以边遍历边计算蓄水面积。

代码：
==
```C++
class Solution {
public:
    int trap(vector<int>& height) {
         if(height.size()<=2) return 0;
        int max=-1,maxInd=0;
        int i=0;
        for(int i=0;i<height.size();i++){
            if(height[i]>max){
                max=height[i];
                maxInd=i;
            }
        }
        int area=0,base=height[0];
        for(i=0;i<maxInd;i++){
            if(base<height[i]) base=height[i];
            else area+=(base-height[i]);
        }
        for(i=height.size()-1,base=height[height.size()-1];i>maxInd;i--){
            if(base<height[i]) base=height[i];
            else area+=(base-height[i]);
        }
        return area;
    }
};
```
```C++
class Solution {
public:
    int trap(vector<int>& height) {
        int l=height.size();
         if(l<=2) return 0;
        vector<int> maxLeft(l, 0);  
        vector<int> maxRight(l, 0);  
        int val=height[0];  
        for(int i=1;i<l; i++) {  
            if(val>height[i]) {  
                maxLeft[i]=val;  
            } 
            else {  
                maxRight[i]=height[i];  
                val=height[i];  
            }  
        }  
        val=height[l-1];  
        for(int i=l-2;i>=0;i--) {  
            if(val>height[i]) {  
                maxRight[i]=val;  
            } 
            else {  
                maxRight[i]=height[i];  
                val=height[i];  
            }  
        }  
  
        int area=0;  
        for(int i=1;i<l-1;i++) {  
            int h=min(maxLeft[i], maxRight[i])-height[i];  
            if(h>0)  
              area+=h;  
        }  
        return area;  
    }
};
```

这是我在网上看到的另外的解法，两种方法都是从两边往中间找，思路也差不多。这个代码是：当前位置，左边高度的最大值和右边高度的最大值，取其中最小的，然后和当前高度相减，如果大于0，则就可以蓄水。
