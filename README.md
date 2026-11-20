import java.util.Stack;

public class Solution {
    public static int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        Stack<Integer> stack = new Stack<>();
        // Push -1 as a base index to calculate lengths for valid substrings starting at index 0
        stack.push(-1); 
        int maxLength = 0;

        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);

            if (ch == '(') {
                // Push index of open parenthesis
                stack.push(i);
            } else {
                // Pop the last unmatched '(' or base index
                stack.pop();

                if (stack.isEmpty()) {
                    // If stack becomes empty, push current index as a new base marker
                    stack.push(i);
                } else {
                    // Current valid length is current index minus top index in stack
                    maxLength = Math.max(maxLength, i - stack.peek());
                }
            }
        }

        return maxLength;
    }

    public static void main(String[] args) {
        // Test cases from the assignment
        System.out.println(longestValidParentheses("(()"));     // Output: 2
        System.out.println(longestValidParentheses(")()())"));  // Output: 4
        System.out.println(longestValidParentheses(""));        // Output: 0
    }
}
