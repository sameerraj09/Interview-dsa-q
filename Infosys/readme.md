**921. Minimum Add to Make Parentheses Valid**

Approach:-
If we will get the open bracket then we will try to push the value in stack
and if we will closw bracket we will try to pop if stack is not empty
else just do count++ means we have nothing to balance the close bracket
and at last just remove the sum of count and stack size
```
class Solution {
    public int minAddToMakeValid(String s) {
        Stack<Character> a = new Stack<>();
        int count = 0;
        
        for (int i = 0; i < s.length(); i++) {
            char curr = s.charAt(i);
            
            if (curr == '(') {
                a.push(curr);
            } else if (curr == ')') {
                if (!a.isEmpty()) {
                    a.pop(); // Matching ')' for an existing '('
                } else {
                    count++; // Unmatched ')', increase the count
                }
            }
        }
        
        // Add unmatched '(' from the stack to the unmatched count
        return count + a.size();
    }
}
```
**Longest Palindrome:-**

Approach:-

Identifying Potential Centers:

Every character in the string can be considered a potential center of a palindrome.
For odd-length palindromes, the center is the character itself (e.g., aba has a as the center).
For even-length palindromes, the center is between two characters (e.g., abba has bb as the center).
Iterating Through the String:

We iterate through each character in the string using a loop.
For each character, we call the helper function expandAroundCenter twice:
Once for odd-length palindromes (using the same character as both the left and right center).
Once for even-length palindromes (using the current character and the next character as the centers).
Expanding Around the Center:

The expandAroundCenter function expands outward from the center indices (left and right) as long as the characters are the same and within the bounds of the string.
It returns the longest palindromic substring found during the expansion.
Updating the Longest Palindrome:

After finding palindromes for both odd and even cases, we compare their lengths with the current longest palindrome and update it accordingly.
Returning the Result:

After iterating through the entire string, we return the longest palindromic substring found.


```
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return ""; // Handle edge cases
        
        String longestPalin = ""; // To store the longest palindrome found
        
        for (int i = 0; i < s.length(); i++) {
            // Check for odd-length palindromes centered at s[i]
            String oddPalin = expandAroundCenter(s, i, i);
            // Check for even-length palindromes centered between s[i] and s[i + 1]
            String evenPalin = expandAroundCenter(s, i, i + 1);
            
            // Update the longest palindrome found
            if (oddPalin.length() > longestPalin.length()) {
                longestPalin = oddPalin;
            }
            if (evenPalin.length() > longestPalin.length()) {
                longestPalin = evenPalin;
            }
        }
        
        return longestPalin; // Return the longest palindromic substring found
    }

    private String expandAroundCenter(String s, int left, int right) {
        // Expand as long as the characters match
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;  // Move left pointer outwards
            right++; // Move right pointer outwards
        }
        // Return the palindromic substring
        return s.substring(left + 1, right); // Adjust indices to get the substring
    }
}

```
