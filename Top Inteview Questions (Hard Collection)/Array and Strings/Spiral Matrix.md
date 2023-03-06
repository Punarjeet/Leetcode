# Approach

In order to traverse the matrix spirally we need to go through following steps :\
step 1. left to right\
step 2. top to bottom\
step 3. right to left\
step 4. bottom to top\
then repeat from step 1
And in each iteration we will either cover one column or row so we just assign each of the above step with direction and then add 1 to get to the next step.

# Code
```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        int t = 0, b = n-1, l = 0, r = m-1, d = 0;    // start with 0 direction corresponds to step 1
        vector<int> ans;
        while(t<=b && l<=r) {
            if(d==0) {
                for(int i=l;i<=r;i++) {
                    ans.push_back(matrix[t][i]);     //  step 1 and increase the top pointer(top row)
                }
                t++;
            } else if(d==1) {
                for(int i=t;i<=b;i++) {
                    ans.push_back(matrix[i][r]);    // step 2 and reduce the right pointer(last column)
                }
                r--;
            } else if(d==2) {
                for(int i=r;i>=l;i--) {
                    ans.push_back(matrix[b][i]);   // step 3 and reduce the bottom pointer(last row)
                }
                b--;
            } else {
                for(int i=b;i>=t;i--) {
                    ans.push_back(matrix[i][l]);  // step 4 and increase the left pointer(first column)
                }
                l++;
            }
            d = (d+1) % 4;                        // move to next step
        }
        return ans;
    }
};
```
Let me know in comments if you have any question or suggestions.
Hope it helps!🙂