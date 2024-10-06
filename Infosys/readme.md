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
