题目：
==
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Example:

Given nums = [5, 2, 6, 1]

To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
Return the array [2, 1, 1, 0].

分析：
==
给定一个数组，让我们找到每个数组元素后面的元素中有几个比其本身小的数，并以数组记录返回。定义一个数组count初始化为0，遍历给定的数组，如果后面有比其自身小的数，count数组该位置元素就加一，最后返回count数组即可。

代码;
==
```C++
class Solution {
public:
    vector<int> countSmaller(vector<int>& nums) {
        int l=nums.size();
        vector<int> count(l,0);
        for(int i=0;i<l;i++)
        {
            for(int j=i+1;j<l;j++){
                if(nums[j]<nums[i])
                    count[i]++;
            }
            
        }
        return count;
    }
};
```

总结感受：
==
一开始看成了找比自己大的了，运行一下发现与结果不同，改了一下就ac了。

