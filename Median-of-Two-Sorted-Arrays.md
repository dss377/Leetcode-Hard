题目：
==
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

```
Example 1:

nums1 = [1, 3]
nums2 = [2]
The median is 2.0
```
```
Example 2:
nums1 = [1, 2]
nums2 = [3, 4]
The median is (2 + 3)/2 = 2.5
```
分析：
==
题目找到两个有序数组的中位数，我就相把两个数组合并为一个数组，然后排序找中位数就好了啊。于是，我的代码是酱紫的：
```C++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        vector<int> nums(nums1.size()+nums2.size(),0);
        for(int i=0;i<nums1.size();i++){
            nums[i]=nums1[i];
        }
        for(int j=0;j<nums2.size();j++){
            nums[nums1.size()+j]=nums2[j];
        }
        for(int i=0;i<nums1.size()+nums2.size();i++){
            sort(nums.begin(),nums.end());
        }
      int l=nums1.size()+nums2.size();
     if(l%2!=0)
            return nums[(l-1)/2];
        else{
            return (nums[l/2-1]+nums[l/2])/2.0;
        }
      
    }
};
```
Time Limit Exceeded   哇地一声哭出来，好不容易没有error了又超时，简直难受死了。呜呜，我只好上网看看大神们的代码了。

对于一个长度为n的已排序数列a，如果n为奇数，中位数为a[n/2],如果n为偶数，则中位数(a[n/2]+a[n/2+1])/2，可以通过在两个数列中求出第K小的元素解决此问题。不妨设数列A元素个数为n，数列B元素个数为m，分别求第k小元素
取A[k/2] B[k/2]比较，如果 A[k/2]>B[k/2]那么，所求的元素必然不在B的前k/2个元素中，反之，必然不在A的前k/2个元素中，于是我们可以将A或B数列的前k/2元素删去，求剩下两个数列的
k-k/2小元素，于是得到了数据规模变小的同类问题，递归解决，如果k/2大于某数列个数，所求元素必然不在另一数列的前k/2个元素中，同上操作即可。

代码：
==
```C++
class Solution {
public:
   double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
       int l1=nums1.size();  
        int l2=nums2.size();  
        int l=l1+l2;  
        if(l&1){  
            return findKth(nums1,0,nums2,0,l/2+1);  
        }  
        return (findKth(nums1,0,nums2,0,l/2)+findKth(nums1,0,nums2,0,l/2+1))/2;  
    }  
   double findKth(vector<int>& nums1,int i1,vector<int>& nums2,int i2,int k){  
        if(i1>=nums1.size()){  
            return nums2[i2+k-1];  
        }  
        if(i2>=nums2.size()){  
            return nums1[i1+k-1];  
        }  
        if(k==1){  
            return min(nums1[i1],nums2[i2]);  
        }  
        int ret1=i1+k/2-1>=nums1.size()?INT_MAX:nums1[i1+k/2-1];  
        int ret2=i2+k/2-1>=nums2.size()?INT_MAX:nums2[i2+k/2-1];  
        if(ret1<ret2){  
            return findKth(nums1,i1+k/2,nums2,i2,k-k/2);  
        }
        else{  
            return findKth(nums1,i1,nums2,i2+k/2,k-k/2);  
        }  

    }
};
```
