题目：
==
Given an unsorted integer array, find the first missing positive integer.

For example,
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.

Your algorithm should run in O(n) time and uses constant space. 

分析：
==
给定一个未排序的数组，找到没有出现的那个正数。一开始我没有看到不能额外申请空间，定义了一个新的数组与原数组中所有的正数做比较，但是超时。好吧，不能有新数组那我覆盖总行吧。思路就是把1放在数组第一个位置nums[0]，2放在第二个位置nums[1]，即需要把nums[i]放在nums[nums[i]-1]上，那么我们遍历整个数组，如果nums[i]!=i+1,而nums[i]为整数且不大于数组长，另外nums[i]不等于nums[nums[i]-1]的话，我们将两者位置调换，如果不满足上述条件直接跳过，最后我们再遍历一遍数组，如果对应位置上的数不正确则返回正确的数。

代码：
==
```C++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
    int i=0;
    while (i<nums.size()) {
          if (nums[i]!=i+1&&nums[i]>0&&nums[i]<=nums.size()&&nums[i]!=nums[nums[i]-1]) {
                swap(nums[i], nums[nums[i]-1]);
            }
          else {
                i++;
            }
        }
        for (i=0;i<nums.size();i++) {
            if (nums[i]!=i+1)  return i+1;
        }
        return nums.size()+1;
    }
};
```

总结体会：
==
好吧，我n多次的wrong answer，总终还是参考大神的代码。我的难点就在于关于负数的处理不合适，所以老是不ac，我没有想到这样子处理，喔单纯的以为我要只考虑正数，但我却处理不好负数，就很难受了。
