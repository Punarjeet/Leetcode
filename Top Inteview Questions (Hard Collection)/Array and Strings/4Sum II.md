# Approach
We can create a map of sum for the first 2 arrays in ```O(n^2)``` and then loop over both the other arrays and then find the sum at ```i``` and ```j``` and then find ```-(nums3[i] + nums4[j])``` in the map so that sum of all 4 will be 0.

# Code
```
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int,int> mp;
        for(int i=0;i<nums1.size();i++) {
            for(int j=0;j<nums2.size();j++) {
                mp[nums1[i] + nums2[j]]++;
            }
        }
        int sum, ans = 0;
        for(int i=0;i<nums3.size();i++) {
            for(int j=0;j<nums4.size();j++) {
                sum = nums3[i] + nums4[j];
                if(mp.count(-sum)) {
                    ans+=mp[-sum];
                }
            }
        }
        return ans;
    }
};
```
Let me know in comments if you have any question or suggestions.
Hope it helps!🙂