# Max Points on a Line

Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

 
```
Example 1:

Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```
```
Example 2:

Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
``` 
```
Constraints:

1 <= points.length <= 300
points[i].length == 2
-104 <= xi, yi <= 104
All the points are unique.
```


>Code

```cpp
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int n = points.size();
        if(n <= 2) return n;
        int maxi = 0;
        for(int i=0;i<n;i++){

            for(int j=i+1;j<n;j++){

                int x1 = points[i][0];
                int x2 = points[j][0];
                int y1 = points[i][1];
                int y2 = points[j][1];    

                // double slope = double(y2 - y1)/double(x2 - x1);
                int total=2;
                for(int k=0;k<n && k!=i && k!=j;k++){
                    
                    int x = points[k][0];
                    int y = points[k][1];
                    // third point
                    // double(y - y1)/double(x1 - x1)
                    if((y2 - y1)*(x - x1) == (x2 - x1)*(y - y1))
                        total++;
                }
                maxi = max(maxi, total);
            }
        }
        return maxi;
    }
};

```
