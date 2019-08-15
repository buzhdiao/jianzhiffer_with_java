#### leetocode-300 最长上升子序列（动态规划解法）

题目：

给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例:
```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```
说明:

可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
你算法的时间复杂度应该为 $O(n^2)$ 。

#### 思路：

使用动态规划的解法，比如以101为例，以101为最后一个元素的最长子序列的长度，等于之前元素组成的子序列的长度加1，那么之前元素组成的子序列的长度可能是多少呢？

* 以10为结尾，那么长度是1，

* 以9结尾，长度是1，

* 以2结尾，长度是1

* 以5结尾，长度是2，序列是[2,5]

* 以3结尾，长度是2，序列是[2,3]

* 以7结尾，长度是3，序列是[2,5,7]或者[2,3,7]

  那么，如果以上几种情况再加上101作为结尾，最长上升序列长度是4，序列是[2,3,7,101],或者是[2,5,7,101]

通过以上分析，得到思路如下;

* 专门开辟一个数组，大小与原数组相同，用于存放以第i个元素结尾时，最长上升子序列的长度
* 定义最终的结果maxans,定义每次遍历的结果maxval
* 定义2层循环，外循环寻找以第i个元素结尾时，最长上升子序列的长度，内循环，遍历第i个元素之前（不包括i)的子序列长度,在它们之间寻找一个最大值，加上1作为以当前元素结尾的最长上升子序列的长度；
* 在内循环时，只比较比当前元素小的位置；

#### 解决代码：

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int maxans = 1;
        for (int i = 1; i < dp.length; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    maxval = Math.max(maxval, dp[j]);
                }
            }
            dp[i] = maxval + 1;
            maxans = Math.max(maxans, dp[i]);
        }
        return maxans;
    }
}

```

-----

```java
import java.lang.Math;
class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] times = new int[nums.length];
        times[0] =1;
        int maxans =1;
        for(int i=1;i<nums.length;i++){
            int maxval =0;
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j]){
                    maxval = Math.max(times[j],maxval);
                }
            }
            times[i]=maxval+1;
            maxans = Math.max(maxans,times[i]);
        }
        return maxans;
        
    } 
}
```

#### 总结：

* math类的导入:import java.lang.Math

  