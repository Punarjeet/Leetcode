# 0(n) Space
<!-- Describe your first thoughts on how to solve this problem. -->
We can use an extra array to store the right side multiplication and then calculate the output array by multiplying the running product from left side with the ```right[i+1]``` which is the product of elements ```[i+1 to n-1]```.

# Code

```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> right(n+1,1);
        vector<int> ans(n);
        for(int i=n-1;i>=0;i--) {
            right[i] = nums[i] * right[i+1]; // right[i] = product from i to n-1
        }
        int l = 1;
        for(int i=0;i<n;i++) {
            ans[i] = right[i+1] * l;  // ans is the running multiple l = product of [0,i-1] with right[i+1] which is product of [i+1,n-1]
            l *= nums[i];
        }
        return ans;
    }
};
```
# Follow Up to use 0(1) Space

We can use a single pointer in which we keep the running product from right side and then multiply it with ```ans[n-1-i]```. In code below we are multiplying left side for index ```i``` when we do ```ans[i] *= l``` and right side when we are visiting it from right side ```ans[n-1-i] *= r```

For example : [1,2,3,4,5]. Calculating value at ```ans[0]```

When ```i = 0``` we will multiply  ```ans[0]``` with ```l = 1``` and when we reach the end of the array ```i = n-1``` then we will multiply ```ans[n-1-i] = ans[0]``` with ```r``` at that time which will be the running product from right side which is ```nums[1] * nums[2] * nums[3] * nums[4] = 120```. Thus ```ans[0] = 120```. 
Similarly we can get the whole ans array.
# Code
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n,1);
        int l = 1, r = 1;
        for(int i=0;i<n;i++) {
            ans[i] *= l;       // multiplying left side
            ans[n-1-i] *= r;   // multiplying right side from the end to element at n-1-i
            l *= nums[i];      // updating l
            r *= nums[n-1-i];  // updating r from the right side
        }
        return ans;
    }
};
```
Space complexity of solution is still ```O(n)``` but as per question it is ```O(1)``` as we are not considering the output array. 

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂