# Lab 3 Write-Up

## Code

```java
class Solution {
    public List<String> removeSubfolders(String[] folder) {
        ArrayList<String> newFolders = new ArrayList<>();
        Arrays.sort(folder, Comparator.comparingInt(String::length));
        for(int i = 0; i < folder.length; i++)
        {
            String prePath = parentFolders(folder[i]);
            if(!saved(newFolders, prePath))
                newFolders.add(folder[i]);
        }

        return newFolders;
        
    }

    private String parentFolders(String str)
    {
        int lastFolder = 0;
        for(int i = 0; i < str.length(); i++)
        {
            if(str.charAt(i) == '/')
                lastFolder = i;
        }

        return(str.substring(0,lastFolder));
            
    }


    public boolean saved(ArrayList<String> pFolders, String str)
    {
        for(int i = 0; i < pFolders.size(); i++)
        {
            if(str.equals(pFolders.get(i)))
                return true;
        }
        String small = parentFolders(str);
        if(small.length() > 0)
            return saved(pFolders, small);
        return false;
    }
}
```
## Description
For this problem, you needed to take a list of folder paths and remove every folder that sits inside another folder in the list.
Then return only the top-level folders that remain.
First, I sorted the folders by length, allowing me to only traverse the array of folders once, as this ensured that every possible sub folder would only appear in the list *after* the parent folder.
Then for each folder, my solution finds  its parent path using `parentFolders`.
Then uses `saved` to determine whether that parent or any higher parent has already been kept.
If it has, the current folder is a subfolder and is not added to the list of folders to return.
If not, then the current folder is added to `newFolders` to be returned.

The helper function `parentFolders` scans a path for its last `/` and returns everything before it.
For example: `/a/b/c` returns `/a/b` and `/a` would return an empty string.

The helper function `saved` goes through the parent folder chain recursively.
First it checks whether the given path exactly matches any folder already kept.
If it does, it returns `true`.
Otherwise it moves up one level by calling `parentFolders` and recurses on the result, stopping and returning `false` once it reaches the empty string.

## Complexity Analysis
Sorting takes O(n log n), where n is each folder in the original array, since comparing two strings by length is instant and Arrays.sort uses timsort. 
After that, each folder checks some number of ancestors, and each check scans the kept list, and builds a shorter string. 
So per folder, it's the number of ancestors to check, the amount of strings in the kept list and the amount of characters in the folder path.
In the worst case, it checks the entire list of ancestors in the pre-path for the string, the entire number of strings in the kept list and goes through all characters to build the shorter string per each folder.
The pre-path and the number of characters copied into new strings are constant, and the number of strings in the kept list in the worst case is n. 
So per folder that is n amount of work which is O($n^2$). Sorting is less than this so run time can be simplified to O($n^2$).

For space complexity, the result list holds at most `n` folders, and sorting may need up to `n` extra space. 
Overall, the extra space is O(n).
