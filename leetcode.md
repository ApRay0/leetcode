# Solution of leetcode in C++
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

```