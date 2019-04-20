
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
```

## 20. Valid Parentheses
```cpp
class Solution {
public:
    bool isValid(string s) {
        if (s.size() == 1) return false;
        stack<char> st;
        for (int i = 0; i < s.size(); i++){
            if(s[i] == '{' || s[i] == '(' || s[i] == '['){
                st.push(s[i]);
            }
            else{
                if (st.empty()) return false;
                else if (s[i] == '}' && st.top() != '{') return false;
                else if (s[i] == ')' && st.top() != '(') return false;
                else if (s[i] == ']' && st.top() != '[') return false;
                else st.pop();
            }
        }
        if (st.empty()) return true;
        else return false;
    }
};
```

## 21. Merge Two Sorted Lists
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if(l1 == nullptr){
        return l2;
    }
    if(l2 == nullptr){
        return l1;
    }
    if(l1->val <= l2->val){
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    }
    else{
        l2->next = mergeTwoLists(l1, l2->next);
        return l2;
    }
    }
};
```

## 22. Generate Parentheses
```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        recur(res, "", n, 0);
        return res;
    }
private:
    void recur(vector<string> &res, string s, int n, int m){
        if(n == 0 && m == 0){
            res.push_back(s);
            return;
        }
        if(n != 0) recur(res, s + '(', n - 1, m + 1);
        if(m != 0) recur(res, s + ')', n, m - 1);
    }
};
```

## 23. Merge k Sorted Lists
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0) return nullptr;
        else{
            while (lists.size()>1){
                lists.push_back(merge2(lists[0],lists[1]));
                lists.erase(lists.begin());
                lists.erase(lists.begin());
            }
            return lists.front();
        }
    }
private:
    ListNode* merge2(ListNode* l1, ListNode* l2){
        if(l1 == nullptr) return l2;
        if(l2 == nullptr) return l1;
        if(l1->val > l2->val){
            l2->next = merge2(l1, l2->next);
            return l2;
        }
        else{
            l1->next = merge2(l1->next, l2);
            return l1;
        }
    }
};
```

## 24. Swap Nodes in Pairs
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
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr) return head;
        ListNode* h = new ListNode (0);
        ListNode* p1 = h;
        ListNode* p2 = head;
        ListNode* p3 = head->next;
        while(1){
            p2->next = p3->next;
            p3->next = p2;
            p1->next = p3;
            if(p2->next && p2->next->next){
                p1 = p2;
                p2 = p1->next;
                p3 = p2->next;
            }
            else{
                break;
            }
        }
        return h->next;
    }
};
```

## 25. Reverse Nodes in k-Group
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
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* res = new ListNode (0);
        res->next = head;
        ListNode* ex = res;
        while(1){
            int count = k;
            ListNode* last = ex;
            while(last != nullptr && count != 0){
                last = last->next;
                count--;
            }
            if(count != 0 || last == nullptr) break;
            else{
                ListNode* first = ex->next;
                for(int i = 0; i < k - 1; i++){
                    ListNode* p = ex->next;
                    ListNode* tmp = p->next;
                    p->next = last->next;
                    last->next = p;
                    ex->next = tmp;
                }
                ex = first;
            }
        }
        return res->next;
    }
};
```

## 26. Remove Duplicates from Sorted Array
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n = nums.size();
        if(n < 2) return n;
        int res;
        int i = 1;
        int index = 1;
        while(i < n){
            if(nums[i] != nums[i-1]){
                nums[index++] = nums[i];
            }
            i++;
        }
        return index;
    }
};
```
## 27. Remove Element
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
        int index = 0;
        for(int i = 0; i < n; i++){
            if(nums[i] != val){
                nums[index++] = nums[i];
            }
        }
        return index;
    }
};
```

## 28. Implement strStr()
```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.size();
        int m = needle.size();
        if (m == 0) return 0;
        for(int i = 0; i < n - m + 1; i++){
            int j = 0;
            int k = i;
            while(haystack[k] == needle[j] && j < m){
                k++;
                j++;
            }
            if(j == m) return i;
        }
        return -1;
    }
};
```

## 29. Divide Two Integers
```cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        if(dividend == INT_MIN){
            if(divisor == 1) return dividend;
            else if(divisor == -1) return INT_MAX;
        }
        int res = dividend / divisor;
        return res;
    }
};
```

## 30. Substring with Concatenation of All Words
```cpp

```

## 31. Next Permutation
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int index = n - 1;
        while(index > 0 && nums[index] <= nums[index - 1]){
            index--;
        }
        if(index == 0){
            int i = 0, j = n - 1;
            while(i < j){
                swap(nums[i], nums[j]);
                i++;
                j--;
            }
        }
        else{
            int i = index, j = n - 1;
            while (j >= 0 && nums[j] <= nums[i-1]) j--;
            swap(nums[i-1], nums[j]);
            j = n - 1;
            while(i < j){
                swap(nums[i], nums[j]);
                i++;
                j--;
            }
        }
        return;
    }
};
```

## 32. Longest Valid Parentheses
```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> sk;
        int res = 0, i = 0, n = s.size();
        sk.push(-1);
        while(i < n){
            if(s[i] == '('){
                sk.push(i);
            }
            else{
                sk.pop();
                if(sk.empty()) sk.push(i);
                else res = max(res,i - sk.top());
            }
            i++;
        }
        return res;
    }
};
```

## 33. Search in Rotated Sorted Array
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int i = 0, j = nums.size();
        int res = -1;
        while(i < j){
            int mid = (i + j) / 2;
            if(nums[mid] == target) return mid;
            if(nums[mid] > nums[i]){
                if(nums[mid] > target && nums[i] <= target) j = mid;
                else i = mid + 1;
            }
            else{
                if(nums[mid] < target && nums[j - 1] >= target) i = mid + 1;
                else j = mid;
            }
        }
        return res;
    }
};
```

## 34. Find First and Last Position of Element in Sorted Array
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res = {-1, -1};
        int i = 0, j = nums.size() - 1;
        if(j == -1) return res;
        while(i < j){
            int mid = (i + j) / 2;
            if (nums[mid] < target) i = mid + 1;
            else j = mid;
        }
        if(nums[i] != target) return res;
        j = nums.size() - 1;
        res[0] = i;
        while(i < j){
            int mid = (i + j) / 2 + 1;
            if (nums[mid] > target) j = mid - 1;
            else i = mid;
        }
        res[1] = j;
        return res;
    }
};
```

## 35. Search Insert Position
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int i = 0, j = nums.size();
        while(i < j){
            int mid = (i + j) / 2;
            if(nums[mid] < target) i = mid + 1;
            else j = mid;
        }
        return i;
    }
};
```

## 36. Valid Sudoku
```cpp
class Solution
{
public:
    bool isValidSudoku(vector<vector<char> > &board)
    {
        int used1[9][9] = {0}, used2[9][9] = {0}, used3[9][9] = {0};
        
        for(int i = 0; i < board.size(); ++ i)
            for(int j = 0; j < board[i].size(); ++ j)
                if(board[i][j] != '.')
                {
                    int num = board[i][j] - '0' - 1, k = i / 3 * 3 + j / 3;
                    if(used1[i][num] || used2[j][num] || used3[k][num])
                        return false;
                    used1[i][num] = used2[j][num] = used3[k][num] = 1;
                }
        
        return true;
    }
};
```
## 37. Sudoku Solver
```cpp

```

## 38. Count and Say
```cpp
class Solution {
public:
    string countAndSay(int n) {
        string res = "11";
        if(n == 1) return res="1";
        int count, i;
        while(n > 2){
            string tmp = "";
            count = 1;
            for(i = 0; i < res.size() - 1; i++){
                if(res[i] == res[i+1]){
                    count++;
                }
                else{
                    tmp = tmp + to_string(count) + res[i];
                    count = 1;
                }
            }
            tmp = tmp + to_string(count) + res[i];
            res = tmp;
            n--;
        }
        return res;
    }
};
```

## 39. Combination Sum
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
       std::sort(candidates.begin(), candidates.end());
        std::vector<std::vector<int> > res;
        std::vector<int> combination;
        combinationSum(candidates, target, res, combination, 0);
        return res;
    }
private:
    void combinationSum(std::vector<int> &candidates, int target, std::vector<std::vector<int> > &res, std::vector<int> &combination, int begin) {
        if (!target) {
            res.push_back(combination);
            return;
        }
        for (int i = begin; i != candidates.size() && target >= candidates[i]; i++) {
            combination.push_back(candidates[i]);
            combinationSum(candidates, target - candidates[i], res, combination, i);
            combination.pop_back();
        }

        
    }
};
```

## 40. Combination Sum II
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        vector<vector<int>> res;
        vector<int> vec;
        sol (candidates, target, res, vec, 0);
        return res;
    }
private:
    void sol (vector<int>& candidates, int target, vector<vector<int>>& res, vector<int>& vec, int index){
        if (!target){
            res.push_back(vec);
            return;
        }
        for (int i = index; i != candidates.size() && target >= candidates[i]; i++){
            if (i == index || candidates[i] != candidates[i - 1]){
                vec.push_back(candidates[i]);
                sol (candidates, target - candidates[i], res, vec, i + 1);
                vec.pop_back();
            }
        }
    }
};
```

## 41. First Missing Positive
```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n; i++){
            while( nums[i] > 0 && nums[i] < n && nums[i] != nums[nums[i] - 1]){
                swap(nums[i], nums[nums[i] - 1]);
            }
        }
        for (int i = 0; i < n; i++){
            if(nums[i] != i + 1){
                return i + 1;
            }
        }
        return n + 1;
    }
};
```

## 42. Trapping Rain Water
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        if (height.empty()) return 0;
        int n = height.size();
        vector<int> ltor (n), rtol (n);
        int res = 0;
        ltor[0] = height[0];
        rtol[0] = height[n - 1];
        for (int i = 1; i < n; i++){
            ltor[i] = max(ltor[i - 1], height[i]);
            rtol[i] = max(rtol[i - 1], height[n - i - 1]);
        }
        for (int i = 0; i < n; i++){
            res += min(ltor[i], rtol[n - i - 1]) - height[i];
        }
        return res;
    }
};
```

## 43. Multiply Strings
```cpp

```

## 44. Wildcard Matching
```cpp

```

## 45. Jump Game II
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int maxrange = 0, res = 0, low = 0, high = 0, n = nums.size();
        if(n == 1) return 0;
        while(maxrange < n - 1){
            for(int i = low; i <= high && i < n; i++){
                maxrange = max(i + nums[i], maxrange);
            }
            low = high + 1;
            high = maxrange;
            res++;
        }
        return res;
    }
};
```

## 46. Permutations
```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> ini (1, nums[0]);
        res.push_back(ini);
        vector<int> vec;
        for(int i = 1; i < nums.size(); i++){
            vector<vector<int>> tmp;
            for(int j = 0; j < res.size(); j++){
                for(int k = 0; k <= res[j].size(); k++){
                    vec = res[j];
                    vec.insert(vec.begin() + k, nums[i]);
                    tmp.push_back(vec);
                }
            }
            res = tmp;
        }
        return res;
    }
};
```

## 47. Permutations II
```cpp
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        rec(nums, 0, nums.size(), res);
        return res;
    }
private:
    void rec(vector<int> num, int begin, int end, vector<vector<int>> &res){
        if(begin + 1 == end){
            res.push_back(num);
            return;
        }
        for(int i = begin; i < end; i++){
            if (i != begin && num[begin] == num[i]) continue;
            swap(num[i], num[begin]);
            rec(num, begin + 1, end, res);
        }
    }
};
```

## 48. Rotate Image
```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for(int i = 0; i < n / 2; i++){
            for(int j = 0; j < n - 2 * i - 1; j++){
                swap(matrix[i][i + j], matrix[i + j][n - 1 - i]);
                swap(matrix[n - 1 - i][n - 1 - i - j], matrix[n - 1 - i - j][i]);
                swap(matrix[i][i + j], matrix[n - 1 - i][n - 1 - i - j]);
            }
        }
        return;
    }
};
```

## 49. Group Anagrams
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        int n = strs.size();
        vector<string> str = strs;
        vector<vector<string>> res;
        int j = 0;
        map<string, int> ref;
        for (int i = 0; i < n; i++){
            sort(str[i].begin(), str[i].end());
            if (ref.find(str[i]) == ref.end()){
                ref[str[i]] = j;
                j++;
                vector<string> tmp (1, strs[i]); 
                res.push_back(tmp);
            }
            else{
                res[ref[str[i]]].push_back(strs[i]);
            }
        }
        return res;
    }
};
```

## 50. Pow(x, n)
```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if(n == 0) return 1;
        if(n < 0){
            if (n == INT_MIN) n += 2;
            n = -n;
            x = 1/x;
        }
        return (n % 2 == 0)? myPow(x * x, n / 2) : x * myPow(x * x, n / 2);
    }
};
```

## 51. N-Queens
```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> res;
        vector<string> piece(n, string(n, '.'));
        rec(res, piece, 0, n);
        return res;
    }
private:
    void rec(vector<vector<string>> &res,vector<string> &piece, int row, int &n){
        if (row == n){
            res.push_back(piece);
            return;
        }
        for(int col = 0; col < n; col++){
            if (valid(piece, row, col, n)){
                piece[row][col] = 'Q';
                rec(res, piece, row + 1, n);
                piece[row][col] = '.';
            }
        }
    }
    bool valid(vector<string> &piece, int row, int col, int &n){
        for(int i = 0; i < row; i++){
            if(piece[i][col] == 'Q') return false;
        }
        for(int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--){
            if(piece[i][j] == 'Q') return false;
        }
        for(int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++){
            if(piece[i][j] == 'Q') return false;
        }
        return true;
    }
};
```

## 52. N-Queens II
```cpp
class Solution {
public:
    int totalNQueens(int n) {
        int res = 0;
        vector<string> piece (n, string(n, '0'));
        rec(res, piece, 0, n);
        return res;
    }
private:
    void rec(int &count, vector<string> &piece, int row, int &n){
        if (row == n){
            count++;
            return;
        }
        for (int col = 0; col < n; col++){
            if (valid(piece, row, col, n)){
                piece[row][col] = '1';
                rec(count, piece, row + 1, n);
                piece[row][col] = '0';
            }
        }
    }
    bool valid(vector<string> &piece, int row, int col, int & n){
        for (int i = 0; i < row; i++){
            if (piece[i][col] == '1') return false;
        }
        for (int i = row - 1, j = col - 1; i >= 0 && j >=0; i--, j--){
            if (piece[i][j] == '1') return false;
        }
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++){
            if (piece[i][j] == '1') return false;
        }
        return true;
    }
};
```

## 53. Maximum Subarray
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = nums[0];
        int sum = 0;
        for (int i = 0; i < nums.size(); i++){
            sum += nums[i];
            res = max(sum, res);
            sum = max(sum, 0);
        }
        return res;
    }
};
```

## 54. Spiral Matrix
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        if (matrix.empty()) return res;
        int n = matrix.size() - 1, m = matrix[0].size() - 1;
        rec(res, matrix, 0, 0, n, m);
        return res;
    }
private:
    void rec(vector<int> &res, vector<vector<int>> &matrix, int row, int col, int n, int m){
        if ( row == n) {
            for (int j = col; j <= m; j++){
                res.push_back(matrix[row][j]);
            }
            return;
        }
        if ( col == m) {
            for (int i = row; i <= n; i++){
                res.push_back(matrix[i][col]);
            }
            return;
        }
        if (row > n || col > m) return;
        for (int j = col; j < m; j++){
            res.push_back(matrix[row][j]);
        }
        for (int i = row; i < n; i++){
            res.push_back(matrix[i][m]);
        }
        for (int j = m; j > col; j--){
            res.push_back(matrix[n][j]);
        }
        for (int i = n; i > row; i--){
            res.push_back(matrix[i][col]);
        }
        rec(res, matrix, row + 1, col + 1, n - 1, m - 1);
    }
};
```

## 55. Jump Game
```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        if (nums.size() == 1) return true;
        int index = 0, maxrange = 0, n = nums.size() - 1;
        while(index <= maxrange){
            maxrange = max(maxrange, index + nums[index]);
            if (maxrange >= n) return true;
            index++;
        }
        return false;
    }
};
```

## 56. Merge Intervals
```cpp

```

## 57. Insert Interval
```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> res;
        int n = intervals.size();
        if (n == 0){
            res.push_back(newInterval);
            return res;
        }
        int left = n - 1, right = 0, i = 0;
        while(left > 0 && intervals[left][0] > newInterval[0]) left--;
        while(right < n - 1 && intervals[right][1] < newInterval[1]) right++;
        vector<int> ins (2,0);
        for(i = 0; i < left; i++){
            res.push_back(intervals[i]);
        }
        if(intervals[left][1] < newInterval[0]){
            ins[0] = newInterval[0];
            res.push_back(intervals[i]);
        }
        else{
            ins[0] = intervals[left][0];
            if(intervals[left][0] > newInterval[0]) ins[0] = newInterval[0];
        }
        if(intervals[right][0] > newInterval[1]){
            ins[1] = newInterval[1];
            res.push_back(ins);
            res.push_back(intervals[right]);
        }
        else{
            ins[1] = intervals[right][1];
            if(intervals[right][1] < newInterval[1]) ins[1] = newInterval[1];
            res.push_back(ins);
        }
        for(i = right + 1; i < n; i++){
            res.push_back(intervals[i]);
        }
        return res;
    }
};
```

## 58. Length of Last Word
```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        int res = 0;
        int n = s.size();
        while(s[n-1] == ' ' ) n--;
        for(int i = 0; i < n; i++){
            if(s[i] == ' ') res=0;
            else res++;
        }
        return res;
    }
};
```

## 59. Spiral Matrix II
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res (n, vector<int> (n));
        int p = 0;
        int q = n-1;
        int num = 1;
        while (p < q)
        {
        for (int i = p; i <= q; i++)
        {
            res[p][i] = num;
            num++;
        }
        for (int i = p + 1; i <= q; i++)
        {
            res[i][q] = num;
            num++;
        }
        for (int i = q-1; i >= p; i--)
        {
            res[q][i] = num;
            num++;
        }
        for (int i = q-1;i >= p + 1;i--)
        {
            res[i][p] = num;
            num++;
        }
            p++;
            q--;
        }
        if (p == q) res[p][p] = n*n;
        return res;
    }
};
```

##  60. Permutation Sequence
```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        string ans = "";
        int i, j, t, sum, jie;
        jie = 1;
        for (i = 1; i <= n; i++){
            jie = i * jie;
            ans += to_string(i);
        }
        for (i = 0; i < n; i++){
            jie /= n - i;
            for (sum = 0, j = 1; j <= n; j++){
                if (sum + jie >= k) break;
                sum += jie;
                swap(ans[i], ans[i + j]);
            }
            k -= sum;
        }
        return ans;
    }
};
```

## 61. Rotate List
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
    ListNode* rotateRight(ListNode* head, int k) {
        if (head == nullptr) return head;
        ListNode* p = head;
        ListNode* res;
        int n = 1;
        while(p->next){
            p = p->next;
            n++;
        }
        p->next = head;
        k %= n;
        n -= k;
        while(n){
            n--;
            p = p->next;
        }
        res = p->next;
        p->next = nullptr;
        return res;
    }
};
```

## 62. Unique Paths
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> res (m, vector<int> (n,1));
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                res[i][j] = res[i-1][j] + res[i][j-1];
            }
        }
        return res[m-1][n-1];
    }
};
```

## 63. Unique Paths II
```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size(), n = obstacleGrid[0].size();
        int i = 0, j = 0;
        vector<vector<long int>> res (m, vector<long int> (n, 0));
        while(i < m && obstacleGrid[i][0] == 0){
            res[i][0] = 1;
            i++;
        }
        i = 0;
        while(i < n && obstacleGrid[0][i] == 0){
            res[0][i] = 1;
            i++;
        }
        for (i = 1; i < m; i++){
            for (j = 1; j < n; j++){
                if (obstacleGrid[i][j] == 1){
                    res[i][j] = 0;
                }
                else{
                    res[i][j] = res[i-1][j] + res[i][j-1];
                }
            }
        }
        return res[m-1][n-1];
    }
};
```

## 64. Minimum Path Sum
```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size(), res = 0;
        for (int i = 1; i < m; i++){
            grid[i][0] += grid[i-1][0];
        }
        for (int i = 1; i < n; i++){
            grid[0][i] += grid[0][i-1];
        }
        for (int i = 1; i < m; i++){
            for (int j = 1; j < n; j++){
                grid[i][j] += min(grid[i-1][j], grid[i][j-1]);
            }
        }
        return grid[m-1][n-1];
    }
};
```

## 65. Valid Number
```cpp

```

## 66. Plus One
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        for (int i = n - 1; i >= 0; i--){
            if (digits[i] == 9){
                digits[i] = 0;
            }
            else{
                digits[i] += 1;
                return digits;
            }
        }
        digits[0] = 1;
        digits.push_back(0);
        return digits;
    }
};
```

## 67. Add Binary
```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        string res = "";
        int i = a.size() - 1, j = b.size() - 1, c = 0;
        while (i >= 0 || j >= 0 || c == 1){
            c += i >= 0? a[i] - '0': 0;
            c += j >= 0? b[j] - '0': 0;
            res = char(c % 2 + '0') + res;
            c /= 2;
            i--;
            j--;
        }
        return res;
    }
};
```

## 68. Text Justification
```cpp

```

## 69. Sqrt(x)
```cpp
class Solution {
public:
    int mySqrt(int x) {
        long i = 1;
        while(i * i <= x){
            i++;
        }
        return i - 1;
    }
};
```

## 70. Climbing Stairs
```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) return 1;
        vector<int> res (n, 0);
        res[0] = 1;
        res[1] = 2;
        for (int i = 2; i < n; i++){
            res[i] = res[i-1] + res[i-2];
        }
        return res[n-1];
    }
};
```

## 