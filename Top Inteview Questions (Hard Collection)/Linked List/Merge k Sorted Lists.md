# Approach 1 O(KN) time and O(1) space

We can iterate over all the starting elements of the lists, find the minimum and add to the list. In order to move the selected pointer to its next, we can use pointer to pointer approach.

# Code
```
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode* dummy = new ListNode();
        ListNode *temp = NULL, *cur = dummy;
        while(1) {
            ListNode** least = &temp;
            for(int i=0;i<lists.size();i++) {
                if(*least==NULL || (lists[i]!=NULL && (*least)->val>lists[i]->val)) {
                    least = &lists[i];
                }
            }
            if(*least==NULL) break;
            cur->next = *least;
            cur = cur->next;
            *least = (*least)->next;
        }
        return dummy->next;
    }
};
```

# Aproach 2 O(Nlog(k)) time and O(k) space
To find the minimum element at each point in time, we can use a min-heap. In C++, the priority_queue data structure is implemented using heaps. By default, the implementation places the maximum element at the top of the queue, but we can create a priority queue with the minimum element at the top by using a custom comparator. To implement this, we can push all the first elements of each list into the queue, retrieve the minimum element, and then add the next element from the selected list to the queue.

# Code
```
class Solution {
public:
    struct compare {
        bool operator()(ListNode* a, ListNode *b) {
            return a->val>b->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode* dummy = new ListNode();
        ListNode *prev = dummy;
        priority_queue<ListNode*, vector<ListNode*>, compare> pq;
        for(auto x: lists) {
            if(x) pq.push(x);
        }
        while(!pq.empty()) {
            ListNode* cur = pq.top();
            pq.pop();
            prev->next = cur;
            prev = prev->next;
            if(cur->next) pq.push(cur->next);
        }
        return dummy->next;
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂