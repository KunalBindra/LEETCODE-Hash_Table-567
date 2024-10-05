# LEETCODE-Hash_Table-567
Let's do a dry run of the `checkInclusion` function with an example to see how it works step by step.

### Problem Statement:
The function checks if the permutation of the string `s1` is a substring of `s2`. It uses the sliding window technique to maintain a window of characters from `s2` and compares it to `s1`.

### Example:  
**Input:**
- `s1 = "ab"`
- `s2 = "eidbaooo"`

### Initial Setup:
1. `count`: an array of size 26 to store the frequency of characters in `s1`.  
   `count = [0, 0, 0, ..., 0]` (26 zeros, one for each letter of the alphabet)
   
2. `required`: the length of `s1`, which is 2 (i.e., `required = 2`).

3. `count` array is updated for characters in `s1`. After processing `s1`:
   - `s1 = "ab"` -> `count['a' - 'a']++` and `count['b' - 'a']++`
   - `count` becomes:
     ```
     count = [1, 1, 0, 0, ..., 0]  
              ^  ^  
             'a' 'b'
     ```
     So, the frequencies of 'a' and 'b' are 1.

### Sliding Window over `s2`:
We will slide a window over `s2` to check if any substring of `s2` is a permutation of `s1`.

**Step 1** (`r = 0, l = 0`):
- Current character in `s2` is `'e'`.  
  `s2[0] = 'e'`  
  `count['e' - 'a']--` -> `count['e' - 'a'] = -1`  
  `required` remains 2 (since `'e'` is not in `s1`, `required` is not changed).
  
- `count` becomes:
  ```
  count = [1, 1, 0, 0, -1, ..., 0]  
                   ^  
                  'e'
  ```
  
**Step 2** (`r = 1, l = 0`):
- Current character in `s2` is `'i'`.  
  `s2[1] = 'i'`  
  `count['i' - 'a']--` -> `count['i' - 'a'] = -1`  
  `required` remains 2 (since `'i'` is not in `s1`).
  
- `count` becomes:
  ```
  count = [1, 1, 0, 0, -1, 0, 0, -1, ..., 0]  
                   ^             ^  
                  'e'           'i'
  ```

**Step 3** (`r = 2, l = 0`):
- Current character in `s2` is `'d'`.  
  `s2[2] = 'd'`  
  `count['d' - 'a']--` -> `count['d' - 'a'] = -1`  
  `required` remains 2 (since `'d'` is not in `s1`).
  
- `count` becomes:
  ```
  count = [1, 1, 0, -1, -1, 0, 0, -1, ..., 0]  
                      ^  ^             ^  
                     'd''e'           'i'
  ```

**Step 4** (`r = 3, l = 0`):
- Current character in `s2` is `'b'`.  
  `s2[3] = 'b'`  
  `count['b' - 'a']--` -> `count['b' - 'a'] = 0`  
  `required--` -> `required = 1` (since `'b'` is in `s1`).

- `count` becomes:
  ```
  count = [1, 0, 0, -1, -1, 0, 0, -1, ..., 0]  
              ^              ^ ^ ^  
             'a'           'd' 'e' 'i'
  ```

**Step 5** (`r = 4, l = 0`):
- Current character in `s2` is `'a'`.  
  `s2[4] = 'a'`  
  `count['a' - 'a']--` -> `count['a' - 'a'] = 0`  
  `required--` -> `required = 0` (since `'a'` is in `s1`).

- `count` becomes:
  ```
  count = [0, 0, 0, -1, -1, 0, 0, -1, ..., 0]  
                      ^   ^   ^ ^  
                     'd' 'e' 'i'
  ```

- Now, since `required == 0`, the window length is checked.  
  The current window is `r - l + 1 = 4 - 0 + 1 = 5`. This is greater than `s1.length()`, so we slide the window from the left (`l++`).

**Step 6** (`r = 5, l = 1`):
- After sliding, we increment the count for `'e'` as `l` is moved past it:  
  `count['e' - 'a']++` -> `count['e' - 'a'] = 0`  
  `required++` -> `required = 1`.

  We keep sliding further as `required > 0`.

**Step 7** (`r = 5, l = 2`):
- The current window becomes "ba", which is a permutation of "ab". Hence, the function returns `true`.

### Final Output:
The function returns `true` because a permutation of `s1` (`"ab"`) exists as a substring of `s2` (`"ba"`).
