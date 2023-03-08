# Approach 1 O(N) time and O(N) space
In order to make a deep copy we need to create a new node for each original node in our linked list and assign next and random pointers to these new nodes. We can use a hashmap that stores the mapping of the node in the original list and the newly created node with the same value and assign the next pointer of the new nodes. In order to assign the random pointer we can iterate over the original list and assign the ```new node random pointer to the new node corresponding to the random pointer of the original node.```


# Code
```
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*,Node*> mp;
        Node *cur = head;
        Node *dummy= new Node(-1), *prev = dummy;
        while(cur) {                 // store the mapping of curroriginalent and new nodes
            Node *t = new Node(cur->val);
            mp[cur] = t;
            prev->next = t;
            prev = prev->next;     // assign next pointer of new nodes
            cur = cur->next;
        }
        cur = head;
        while(cur) {            
            mp[cur]->random = mp[cur->random];  // assign new list random pointer to new node corresponding to the random pointer of original list
            cur = cur->next;
        }
        return dummy->next;
    }
};
```

# Aproach 2 O(N) time and O(1) space
Can we get rid of the map in the above solution? In order to do so, we should be able to get the new node corresponding to the original node in O(1) time as we had in the hashmap. We can achieve this by keeping the new node just next to the corresponding original node. Then the ```random pointer of the new node is the next pointer of the random pointer of the original node.```<br>
After the random pointer assignment, we need to disconnect both lists. It is not difficult as we know for sure that the next pointer of the original node is part of the new list.<br>
Note : Here the space used is O(n) if we consider the output list space, however we are just try to rid of the extra space(hashmap) in this solution.

# Code
```
class Solution {
public:
    Node* copyRandomList(Node* head) {
        Node *cur = head, *next;
        while(cur) {            // merge original and new list by keeping new node just next to original node
            next = cur->next;
            Node *copy = new Node(cur->val);
            cur->next = copy;
            copy->next = next;
            cur = next;
        }
        cur = head;
        while(cur) {
            next = cur->next->next;
            if(cur->random) {
                cur->next->random = cur->random->next; // assign random pointer
            }
            cur = next;
        }
        Node *dummy = new Node(-1);
        Node *prev = dummy;
        cur = head;
        while(cur) {                       // disintegrate to 2 linked lists
            next = cur->next->next;
            prev->next = cur->next;
            prev = prev->next;
            cur->next = next;
            cur = next;
        }
        return dummy->next;
    }
};
```

Let me know in comments if you have any question or suggestions.<br>
Hope it helps!🙂