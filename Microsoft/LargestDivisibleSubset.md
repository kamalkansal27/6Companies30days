# Largest Divisible Subset

Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:

> answer[i] % answer[j] == 0, or
> answer[j] % answer[i] == 0

If there are multiple solutions, return any of them.

 
```
Example 1:

Input: nums = [1,2,3]
Output: [1,2]
Explanation: [1,3] is also accepted.
```
```
Example 2:

Input: nums = [1,2,4,8]
Output: [1,2,4,8]
``` 
```
Constraints:

> 1 <= nums.length <= 1000
> 1 <= nums[i] <= 2 * 109
> All the integers in nums are unique.
```

>Code:

```cpp
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<int> dp(n, 1), hash(n);
        int lastIndex = 0;
        int maxi = 1;
        for(int idx=0;idx<n;idx++){
            hash[idx] = idx;
            for(int prev=0;prev<idx;prev++){
                if(nums[idx] % nums[prev] == 0 && dp[idx] < 1 + dp[prev]){
                    dp[idx] = 1 + dp[prev];
                    hash[idx] = prev;      
                }
            }
            if(dp[idx] > maxi){
                maxi = dp[idx];
                lastIndex = idx;
            }
        }
        vector<int> ans;
        ans.push_back(nums[lastIndex]);
        while(lastIndex != hash[lastIndex]){
            lastIndex = hash[lastIndex];
            ans.push_back(nums[lastIndex]);
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};

```
