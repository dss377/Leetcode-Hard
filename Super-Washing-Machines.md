题目：
==
You have n super washing machines on a line. Initially, each washing machine has some dresses or is empty.

For each move, you could choose any m (1 ≤ m ≤ n) washing machines, and pass one dress of each washing machine to one of its adjacent washing machines at the same time .

Given an integer array representing the number of dresses in each washing machine from left to right on the line, you should find the minimum number of moves to make all the washing machines have the same number of dresses. If it is not possible to do it, return -1.

```
Example1

Input: [1,0,5]

Output: 3

Explanation: 
1st move:    1     0 <-- 5    =>    1     1     4
2nd move:    1 <-- 1 <-- 4    =>    2     1     3    
3rd move:    2     1 <-- 3    =>    2     2     2   

Example2

Input: [0,3,0]

Output: 2

Explanation: 
1st move:    0 <-- 3     0    =>    1     2     0    
2nd move:    1     2 --> 0    =>    1     1     1     

Example3

Input: [0,2,0]

Output: -1

Explanation: 
It's impossible to make all the three washing machines have the same number of dresses. 
```
Note:

    The range of n is [1, 10000].
    The range of dresses number in a super washing machine is [0, 1e5].

分析：
==
给定一个长度为n的整数数组，每次选择m个数(1 ≤ m ≤ n)进行移动：将这m个数减1，同时，其相邻的元素就加1，而且这m个数也可以是被加元素，求最少要移动多少次，才能使数组中的所有数都相等。如果不能做到，则返回-1。首先肯定是遍历找出衣服总数了，然后看是否能够平均分配，若不能则返回-1，如果能，我们就要算出这个平均数是多少，然后再遍历，找到所有数与这个平均数的差距之和，因为有的多，有的少，所以任一位置时max(machines[i]-aveClothes,abs(move)
就是最小的操作步数。

代码：
==
```C
int findMinMoves(int* machines, int machinesSize) {
    int cloSum=0; 
    for(int i=0;i<machinesSize;i++){
        cloSum+=machines[i];
    }
    int move=0,ret=0;
    if(cloSum%machinesSize!=0)  return -1;
    int aveClothes=cloSum/machinesSize;
    for(int i=0;i<machinesSize;i++){
        move=move+machines[i]-aveClothes;
        ret=max(ret,max(machines[i]-aveClothes,abs(move)));
    }
    return ret;
}
int max(int x,int y){
    return x>y?x:y;
}
```

总结感受：
==
最初的想法是和前两天做的求最小操作数的那两道题一样，以为求于平均值的差的绝对值之和就可以，运行之后发现不对，这个题中的元素的增减相对自由，但拿进与拿出衣服是要区别对待，我们算出的差的和是拿进与拿出抵消后的，不是总的操作步数，所以才会有找真正操作步数的操作。
