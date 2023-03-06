# Approach
We can use ```union find``` to solve this problem. As at first all elements are like disjoint sets and there is a connection(edge) for ```nums[i]``` if we have ```nums[i] - 1 or nums[i] + 1``` already travesed in the array which are stored in the map for easy lookup. As we see a valid edge We can call union function to merge both the sets. So after creating all the edges we just need the largest size connected set(consecutive numbers).

# Code
```
class Solution {
public:
    int find(vector<int> &parent, int i) {
        if(i==parent[i]) return i;
        return parent[i] = find(parent, parent[i]);
    }
    
    void unionFun(vector<int> &size, int i, int j, vector<int> &parent) {
        int a = find(parent, i);
        int b = find(parent, j);
        if(a!=b) {
            if(size[a]>=size[b]) {
                size[a]+=size[b];
                parent[b] = a;
            } else {
                size[b] += size[a];
                parent[a] = b;
            }
        }
    }
    
    int longestConsecutive(vector<int>& nums) {
        unordered_map<int,int> mp;
        int n = nums.size();
        vector<int> parent(n), size(n);
        for(int i=0;i<n;i++) {
            parent[i] = i;
            size[i] = 1;
        }
        for(int i=0;i<n;i++) {
            if(mp.count(nums[i])) continue;
            if(mp.count(nums[i]-1)) {
                unionFun(size, mp[nums[i]-1], i, parent);
            }
            if(mp.count(nums[i]+1)) {
                unionFun(size, mp[nums[i]+1], i, parent);
            }
            mp[nums[i]] = i;
        }
        int ans = 0;
        for(auto x : size) {
            ans = max(ans, x);
        }
        return ans;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂