# Approach 1 : O(n) space and O(n) time without modifying array
We can use a hashmap to store the number and if we see a already existing element we can return that element as it is the duplicate number.

# Code
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        unordered_map<int,int> mp;
        for(auto x: nums) {
            if(mp.count(x)) return x;
            mp[x]++;
        }
        return -1;
    }
};
```

# Approach 2 : O(1) space and O(n) time with modifying array
Here we will use the information that elements will be from ```[1,n]``` and length of array is ```n+1```. It means that we can sort the array and correct position at index ```i is i+1```. To do this if a element is not at the right postion we can correct it by swapping ```nums[i] with nums[nums[i]-1]``` as it will put the element at index ```i to be i+1```. And if we find a element where the element at ```nums[nums[i]-1] == nums[i```] then it means there is correct element already at the position and this is the duplicate one.

# Code
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        for(int i=0;i<n;) {
            if(nums[i] == i + 1) {
                i++;
            } else if(nums[nums[i]-1] == nums[i]) {
                return nums[i];
            } else {
                swap(nums[i], nums[nums[i]-1]);
            }
        }
        return -1;
    }
};
```

# Approach 3 : O(1) space and O(n) time without modifying array
We can use the cycle detection algorithm where we use slow and fast pointer and move them with 1 and 2 steps repectively. We can use this as when we move from nums[i] to nums[nums[i]] then if we have a duplicate then it will form a loop. It happens because more than 1 value points to the same index for the next iteration. For ex : \
```[1,3,4,2,2] here i = 3,4 will go next to i = 2```\
After we detect the cycle we want to move to the start of the cycle from the meeting point. You can see for the proof that the distance from the meeting point to the start of the cycle is equal to the distance from the head to the start of the cycle.

# Code
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        int slow = nums[0];
        int fast = nums[nums[0]];
        while(slow!=fast) {
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        slow = 0;
        while(slow!=fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂