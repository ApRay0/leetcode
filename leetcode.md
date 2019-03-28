# Solution Of Leetcode In C++
## 1.Two Sum
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> mapple;
        vector<int> res;
        for(int i = 0; i < nums.size(); i++){
            mapple[nums[i]] = i;
        }
        for(int i = 0; i < nums.size(); i++){
            int tmp = target - nums[i];
            if(mapple.find(tmp) != mapple.end() && mapple[tmp] != i){
                res.push_back(i);
                res.push_back(mapple[tmp]);
                break;
            }
        }
        return res;
    }
};
```

## 2.Add Two Numbers
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* res = new ListNode(0);
        ListNode* p = res;
        int sum = 0;
        while(l1 || l2 || sum){
            if(l1){
                sum += l1->val;
                l1 = l1->next;
            }
            if(l2){
                sum += l2->val;
                l2 = l2->next;
            }
            p->next = new ListNode(sum % 10);
            p = p->next;
            sum = sum / 10;
        }
        return res->next;
    }
};
```
## 3.Longest Substring Without Repeating Characters
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.length(), res = 0;
        int index[128] = {0};
        for (int j = 0, i = 0;j < n;j++){
            i = max(index[s[j]], i);
            res = max(res, j - i + 1);
            index[s[j]] = j + 1;
        }
        return res;
    }
};
```

## 4.Median of Two Sorted Arrays
```cpp

```

## 5.Longest Palindromic Substring
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int left = 0, len = 0;
        int n = s.size();
        for(int i = 0;i < n;i++){
            int k = 0;
            while(i - k >= 0 && i + k <= n && s[i-k] == s[i+k]){
                if (len < 2 * k + 1){
                    len = 2 * k + 1;
                    left = i - k;
                }
                k++;
            }
            k = 0;
            while(i - k >= 0 && i + k + 1<= n && s[i-k] == s[i+k+1]){
                if (len < 2 * k + 2){
                    len = 2 * k + 2;
                    left = i - k;
                }
                k++;
            }
        }
        return s.substr(left, len);
    }
};
```

## 6.ZigZag Conversion
```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if(numRows==1) return s;
        int n=0;
        int l=2*numRows-2;
        int len=s.size();
        string res;
        for(int i=0;i<numRows;i++){
            int gap=l-2*i;
            int k=gap;
            if(i<len) res.push_back(s[i]);
            while((i+k)<len){
                if (gap!=0) res.push_back(s[i+k]);
                gap=l-gap;
                k=k+gap;
            }
        }
        return res;
    }
};
```

## 7.Reverse Integer
```cpp
class Solution {
public:
    int reverse(int x) {
        long long res = 0;
        while(x){
            res *= 10;
            res += x % 10;
            x /= 10;
        }
        return (res<INT_MIN || res>INT_MAX) ? 0 : res;
    }
};
```

## 8.