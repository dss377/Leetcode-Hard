题目：
==
Follow up for "Find Minimum in Rotated Sorted Array": What if duplicates are allowed?

Would this affect the run-time complexity? How and why? Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates.

分析：
==
在一个排序被反转过的数组中找到最小的数。按照常理，是应该找到中间在哪里反转的，但我一时实现不了这样的操作，好吧，我先简单粗暴的来一波。

代码：
==
```C++
class Solution {
public:
    int findMin(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        return nums[0];
    }
};
```

好吧，我目瞪狗呆。还是看一下比较好的的做法吧。

利用二分法来找最小值。
```C++
class Solution {
public:
    int findMin(vector<int>& nums) {
         if(nums.empty())
            return 0;
        if(nums.size()==1)
            return nums[0];
        int l=nums.size();
        int low=0;
        int high=l-1;//分成两部分来找中间点
        while(low<high&&nums[low]>=nums[high])
        {
            int mid=low+(high-low)/2;
            if(nums[mid]<nums[low])   
                high=mid;//说明mid在右边那一部分
            else if(nums[mid]==nums[low])
                low++;//如果重复就直接low++继续进行下一步比较
            else
                low=mid+1;
        }
        return nums[low];
    }
};
```
