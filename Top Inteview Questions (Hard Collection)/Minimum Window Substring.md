# Approach
We can solve this problem using two pointers and a map. First we will fill the map with the count of string t. Then iterate on s keep a right and left pointer. Every calculation will be in range ```[l,r)``` for string s.
For right pointer ```if(count[s[r]]>0)``` it means that ```count[s[r]] in t > count[s[r]] in s``` so we can consider this element in s and reduce ```m(size of t)``` and decrease ```mp[s[r]]```. Then when ```m==0``` it means we have all the elements of t in the range ```[l,r)```. So now we move ```l``` to just more than the first element where ```count[s[r]] in t == count[s[r]] in s``` which means ```count[s[r]]==0``` where the range will not fully contain string t and keep the minimum window.

# Code
```
class Solution {
public:
    string minWindow(string s, string t) {
        int n = s.size(), m = t.size();
        int l = 0, r = 0, mi = INT_MAX, la=0;
        vector<int> count(128,0);
        if(m>n) return "";
        for(auto x : t) {
            count[x]++;
        }
        while(r<n) {
            if(count[s[r++]]-->0) {               // in t string
                m--;
            }
            while(m==0) {                        // valid [l,r) sub string
                if(r-l<mi) {                     // check for minimum window
                    mi = r-l;
                    la = l;
                }
                if(count[s[l]]==0) {            // check if the left is part of t string
                    m++;
                }
                count[s[l++]]++;
            }
        }
        return mi==INT_MAX?"":s.substr(la, mi);
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂