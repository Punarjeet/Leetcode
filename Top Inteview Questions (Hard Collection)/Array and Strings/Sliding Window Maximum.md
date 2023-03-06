# Approach
We can use a deque which is a doubly linked list where we can remove/add from start and end in ```O(1)```. At ```i``` we can remove all the elements less than ```nums[i]``` from the back in deque as they can never be the part of the answer. And we can check from start if at any time we have a element less than the index to be considered for this window which is ``` <i-k```. The first element of the deque is the max for the window ```(i-k,i]```.

# Code
```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> q;
        int n = nums.size();
        vector<int> ans;
        for(int i=0;i<n;i++) {
            while(!q.empty() && nums[q.back()]<nums[i]) {
                q.pop_back();
            }
            q.push_back(i);
            while(q.front()<=i-k) {
                q.pop_front();
            }
            if(i>=k-1) {
                ans.push_back(nums[q.front()]);
            }
        }
        return ans;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂