# Approach
Major deduction from the question we can infer is the answer can be from ```[1,n+1]``` as there can be n consecutive number from ```[1,n]``` in the array making maximum value to be n+1. So `nums[i]<0 && nums[i]>n+1` can be neglected.

To neglect the negative number we can move it to the end of the array. Then iterating on all the positive elements less than k(length of postive elements) we make the element at index nums[i]-1 negative. So the first postive element in the array will be the first missing number as that index was not negated.

# Code
```
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        int k = n-1, pos=0;
        for(int i=0;i<n;i++) {
            if(nums[i]<=0 && i<=k) {
                swap(nums[i--], nums[k--]);
            } else if(nums[i]>0) pos++;
        }
        k = pos;
        for(int i=0;i<k;i++) {
            if(abs(nums[i])<=k) {
                nums[abs(nums[i])-1] = -abs(nums[abs(nums[i])-1]);
            }
        }
        for(int i=0;i<k;i++) {
            if(nums[i]>0) return i+1;
        }
        return k+1;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂