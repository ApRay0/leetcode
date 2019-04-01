
# Solution Of Leetcode In C++

## 1. Two Sum
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

## 2. Add Two Numbers
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
## 3. Longest Substring Without Repeating Characters
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

## 4. Median of Two Sorted Arrays
```cpp

```

## 5. Longest Palindromic Substring
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

## 6. ZigZag Conversion
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

## 7. Reverse Integer
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

## 8. String to Integer (atoi)
```cpp
class Solution {
public:
    int myAtoi(string str) {
        long long res = 0;
        int n = str.size();
        int i = 0, sign = 1;
        while(str[i] = ' '){
            i++;
        }
        if(str[i] == '-'){
            sign = -1;
            i++;
        } 
        if(str[i] == '+'){
            i++;
        }
        while(str[i] <= '9' && str[i] >= '0' && i < n){
            res = res * 10 + (str[i] - '0');
            i++;
            if( sign * res > INT_MAX) return INT_MAX;
            if( sign * res < INT_MIN) return INT_MIN;
        }
        return sign * res;
    }
};
```

## 9. Palindrome Number
```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || x != 0 && x % 10 == 0) return false;
        int sum = 0;
        while(x > sum){
            sum = 10 * sum + x % 10;
            x /= 10;
        }
        return (x == sum) || (x == sum / 10);
    }
};
```

## 10. Regular Expression Matching
```cpp
class Solution {
private:
    bool match(const string &s, const string &p, int index1, int index2)
    {
        int len1 = s.size(), len2 = p.size();
        if(index2 == len2) return index1 == len1; 
        
        if(p[index2+1] != '*')
        {
           if( index1 < len1 && (p[index2] == s[index1] || p[index2] == '.')) return match(s, p, index1 + 1, index2 + 1);
        }
        else
        {
            if(match(s, p, index1, index2 + 2)) return true;
            while(index1 < len1 && (p[index2] == s[index1] || p[index2] == '.')){
                index1++;
                if(match(s, p, index1, index2 + 2)) return true;
            }
        }
        return false;
    }

public:
    bool isMatch(string s, string p) {
       return match(s, p, 0, 0); 
    }
};
```

## 11. Container With Most Water
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int res = 0, i = 0, j = n - 1;
        while(i < j){
            res = max(res, min(height[i], height[j]) * (j - i));
            if(height[i] < height[j])  i++;
            else j--;
        }
        return res;
    }
};
```

## 12. Integer to Roman
```cpp
class Solution {
public:
    string intToRoman(int num) {
    string M[] = {"", "M", "MM", "MMM"};
    string C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
    string X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
    string I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
    return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];        
    }
};
```

## 13. Roman to Integer
```cpp
class Solution {
public:
    int romanToInt(string s) {
        map<char, int> tran = {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
        int res = tran[s.back()];
        int n = s.size();
        for(int i = 0; i < n - 1; i++){
            if(tran[s[i]] < tran[s[i+1]]){
                res -= tran[s[i]];
            }
            else{
                res += tran[s[i]];
            }
        }
        return res;
    }
};
```

## 14. Longest Common Prefix
```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string prefix = "";
        for(int idx = 0; strs.size() > 0; prefix += strs[0][idx], idx++)
            for(int i = 0; i < strs.size(); i++)
                if(idx >= strs[i].size() ||(i > 0 && strs[i][idx] != strs[i-1][idx]))
                    return prefix;
        return prefix;
    }
};
```

## 15. 3Sum
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        int n = nums.size();
        std::sort(nums.begin(), nums.end());
        for (int i = 0; i < n - 2; i++){
            if(i == 0 || (nums[i]) != nums[i-1]){
                int aim = -nums[i], low = i + 1, high = n - 1;
                while(low < high){
                    if(nums[low] + nums[high] == aim){
                        vector<int> tmp(3);
                        tmp[0] = nums[i];
                        tmp[1] = nums[low];
                        tmp[2] = nums[high];
                        res.push_back(tmp);
                        while(nums[low] == tmp[1] && low < high) low++;
                        while(nums[high] == tmp[2] && low < high) high--;
                    }
                    else if(nums[low] + nums[high] < aim) low++;
                    else high--;
                }
            }
            while(nums[i] == nums[i+1] && i < n - 2) i++;
        }
        return res;
    }
};
```

## 16. 3Sum Closest
```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int res = nums[0] + nums[1] + nums[2];
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        for (int i = 0; i < n -2; i++){
            int low = i + 1, high = n - 1, sum;
            while(low < high){
                sum = nums[i] + nums[low] + nums[high];
                if(sum > target){
                    res = abs(res - target) > abs(sum - target)? sum : res;
                    high--;
                }
                else if(sum < target){
                    res = abs(res - target) > abs(sum - target)? sum : res;
                    low++;
                }
                else return target;
            }
        }
        return res;
    }
};
```

## 17. Letter Combinations of a Phone Number
```cpp
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if(digits.empty()) return vector<string> ();
        vector<string> res;
        vector<string> tab = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        int n = digits.size();
        res.push_back("");
        for(int i = 0; i < n; i++){
            vector<string> tmp;
            int num = digits[i] -'0';
            for(int j = 0; j < res.size(); j++){
                for(int k = 0; k < tab[num].size(); k++){
                    tmp.push_back(res[j] + tab[num][k]);
                }
            }
            res = tmp;
        }
        return res;
    }
};
```

## 18. 4Sum
```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        for (int i = 0; i < n - 3 ; i++){
            for (int j = i + 1; j < n - 2; j++){
                int low = j + 1, high = n - 1;
                while(low < high){
                    int sum = nums[i] + nums[j] + nums[low] + nums[high];
                    if (sum < target) low++;
                    else if (sum > target) high--;
                    else{
                        vector<int> tmp(4);
                        tmp[0] = nums[i];
                        tmp[1] = nums[j];
                        tmp[2] = nums[low];
                        tmp[3] = nums[high];
                        res.push_back(tmp);
                        while(nums[low] == tmp[2] && low < high) low++;
                        while(nums[high] == tmp[3] && low < high) high--;
                    }
                }
                while(nums[j] == nums[j+1] && j < n - 2) j++;
            }
            while(nums[i] == nums[i+1] && i < n - 3) i++;
        }
        return res;
    }
};
```

## 19. Remove Nth Node From End of List
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* res = new ListNode(0);
        res->next = head;
        ListNode* p = res;
        int len = -1;
        while(p){
            p = p->next;
            len++;
        }
        len = len - n;
        p = res;
        while(len){
            p = p->next;
            len--;
        }
        p->next = p->next->next;
        return res->next;
    }
};
`