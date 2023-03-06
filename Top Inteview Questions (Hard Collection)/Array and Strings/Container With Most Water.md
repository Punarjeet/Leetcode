# Approach
We can use 2 pointers from start and end keeping the width the maximum, then if ```nums[i] < nums[j]``` we are sure that we cannot create container with more value if we choose i because for calculating the height we are taking the mininum of the both heights and moving either of them will reduce the width by 1

# Code
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int l = 0, r = n-1;
        int ans = 0;
        while(l<r) {
            if(height[l]<=height[r]) {
                ans = max(ans, height[l]*(r-l));
                l++;
            } else {
                ans = max(ans, height[r]*(r-l));
                r--;
            }
        }
        return ans;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂