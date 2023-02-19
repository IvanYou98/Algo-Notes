# Dynamic Programming

### Laicode 87 Max Product of Cutting Rope

Given a rope with positive integer-length *n*, how to cut the rope into *m* integer-length parts with length *p*[0], *p*[1], ...,*p*[*m*-1], in order to get the maximal product of *p*[0]**p*[1]* ... **p*[*m*-1]? *****m* **is determined by you** and must be greater than 0 **(at least one cut must be made**). Return the max product you can have.

**Assumptions**

- n >= 2

**Examples**

- n = 12, the max product is 3 * 3 * 3 * 3 = 81(cut the rope into 4 pieces with length of each is 3).

```java
public class Solution {
  public int maxProduct(int length) {
    // M[i] means the the max product of cutting a rope of length i (at least one cut must be made)
    int[] M = new int[length + 1];
    M[1] = 1;
    // l means the total length of the rope
    for (int l = 2; l <= length; l++) {
      int maxProduct = 0;
      for (int left = l - 1; left >= 1; left--) {
				// left means there's no cut on the left rope,
				//  M[left] means there's at least one cut on the left rope
        // (l - left) means the right rope 
			  int largertProduct = Math.max(M[left], left) * (l - left);
        maxProduct = Math.max(maxProduct, largertProduct);
      }
      M[l] = maxProduct;
    }
    return M[length];
  }
}
```

### 99. Dictionary Word I

Given a word and a dictionary, determine if it can be composed by concatenating words from the given dictionary.

**Assumptions**

- The given word is not null and is not empty
- The given dictionary is not null and is not empty and all the words in the dictionary are not null or empty

**Examples**

Dictionary: {“bob”, “cat”, “rob”}

- Word: “robob” return false
- Word: “robcatbob” return true since it can be composed by "rob", "cat", "bob"