# Minimum Consecutive Cards to Pick Up

You are given an integer array cards where cards[i] represents the value of the ith card. A pair of cards are matching if the cards have the same value.

Return the minimum number of consecutive cards you have to pick up to have a pair of matching cards among the picked cards. If it is impossible to have matching cards, return -1.

 
```
Example 1:

Input: cards = [3,4,2,3,4,7]
Output: 4
Explanation: We can pick up the cards [3,4,2,3] which contain a matching pair of cards with value 3. Note that picking up the cards [4,2,3,4] is also optimal.
```

```
Example 2:

Input: cards = [1,0,5,3]
Output: -1
Explanation: There is no way to pick up a set of consecutive cards that contain a pair of matching cards.
```
```
Constraints:

1 <= cards.length <= 105
0 <= cards[i] <= 106
```
# Code
```cpp
class Solution {
public:
    int minimumCardPickup(vector<int>& cards) {
        // Declare the variables.
        int n = cards.size();
        unordered_map<int, vector<int>> mp;
        // Take the indices where the elements comes.
        for(int i=0;i<n;i++){
            mp[cards[i]].push_back(i);
        }
        // Traverse the map to get the minimum difference of indices between the two same elements.
        int ans = INT_MAX;
        for(auto i : mp){
            int m = i.second.size();
            if(m >= 2){
                for(int j=0;j<m-1;j++){
                    int diff = i.second[j+1] - i.second[j] + 1;
                    ans = min(ans, diff);
                }
            }
        }
        if(ans == INT_MAX) return -1;
        return ans;
    }
};
```
