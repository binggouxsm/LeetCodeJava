# [00046 Permutations](https://leetcode.com/problems/permutations/)

## 思路： 回溯法

### (1)具体解法：

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        ArrayList<Integer> leftnums = new ArrayList<Integer>();
        for(int num : nums){
            leftnums.add(num);
        }
        backtrack(new ArrayList<Integer>(),leftnums , ret);
        return ret;
    }
    
    public void backtrack(ArrayList<Integer> perm,ArrayList<Integer> leftnums, List<List<Integer>> ret){
        if(leftnums.size() == 0){
            ret.add(new ArrayList<Integer>(perm));
        }
        for(int i = 0 ; i < leftnums.size(); i++){
        	
        	ArrayList<Integer> leftnumsCopy = (ArrayList<Integer>)leftnums.clone();
            perm.add(leftnums.get(i));
            leftnumsCopy.remove(i);
            backtrack(perm,leftnumsCopy,ret);
            perm.remove(perm.size() -1);
        }
            
    }
}
```


