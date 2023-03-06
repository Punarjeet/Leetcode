# Approach
Using extra space we can easily get the new states by as for each element we can look at the 8 positions to get the sum of zeroes and ones and based on checks given in the question we can get the next state

But to do this in-place we need to store 2 information in a single cell in ```board[i][j]``` one is the current state and second is the next state. As the values can only be 0,1 we can use binary representation. Current information can be stored on 1st bit which will have a value of ```0,1```. And new state can be stored in 2nd bit which is ```00,10```. And we can add to store both states. So the ```board[i][j]``` after one iteration can have values : \
value   CS   NS \
00&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;1\
01&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;0\
10&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;1\
11&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;1

To get the current state we can just take modulo of the number by 2. For the new state we can right shift the number to get the next state stored at second bit.

# Code
```
class Solution {
public:
    int dx[8] = {0,0,1,-1,1,1,-1,-1};
    int dy[8] = {1,-1,0,0,1,-1,1,-1};
    bool isValid(int x, int y, int n, int m) {
        return x>=0 && y>=0 && x<n && y<m;
    }
    
    int toValue(int o, int z, int cur) {
        if(cur) {
            if(o<2 || o>3) return 0;
            return 2;
        } else {
            if(o==3) return 2;
            return 0;
        }
        return 0;
    }
    void gameOfLife(vector<vector<int>>& board) {
        int n = board.size();
        int m = board[0].size();
        for(int i=0;i<n;i++) {
            for(int j=0;j<m;j++) {
                int o = 0, z=0;
                for(int k=0;k<8;k++) {
                    int x = i + dx[k], y = j + dy[k];
                    if(isValid(x, y, n, m)) {
                        if(board[x][y]%2==0) {
                            z++;
                        } else {
                            o++;
                        }
                    }   
                }
                board[i][j]+=toValue(o,z,board[i][j]);
            }
        }
        for(int i=0;i<n;i++) {
            for(int j=0;j<m;j++) {
                board[i][j] = board[i][j]>>1;
            }
        }
    }
};
```

Let me know in comments if you have any question or suggestions.
Hope it helps!🙂