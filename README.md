3. Longest Substring Without Repeating Characters📝 Problem StatementGiven a string s, find the length of the longest substring without duplicate characters.💡 ExamplesExample 1:Input: s = "abcabcbb"Output: 3Explanation: The answer is "abc", with a length of 3.Example 2:Input: s = "bbbbb"Output: 1Explanation: The answer is "b", with a length of 1.Example 3:Input: s = "pwwkew"Output: 3Explanation: The answer is "wke", with a length of 3.Note that the answer must be a substring, "pwke" is a subsequence and not a substring.🔒 Constraints$0 \le \text{s.length} \le 5 \times 10^4$s consists of English letters, digits, symbols, and spaces.🧠 Approach & LogicThe problem requires finding a contiguous sequence of non-repeating characters. An optimal solution uses the Sliding Window Pattern paired with a Hash Table:Sliding Window (left to right):The right pointer iterates through each character to expand the window.The left pointer maintains the starting position of the current non-repeating substring window.Index Map Memory:A HashMap stores each character alongside its most recent 0-based index.Updating Window Bounds:When encountering a character already present in the map, left shifts to Math.max(left, map.get(currentChar) + 1).Using Math.max guarantees left never moves backward when skipping old characters from earlier windows.Tracking Length:At each iteration, length is recalculated as right - left + 1, and maxLength is updated accordingly.💻 Java Solutionimport java.util.HashMap;
import java.util.Map;

public class Solution {

    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        int left = 0;
        
        // Maps character to its last seen index
        Map<Character, Integer> charMap = new HashMap<>();
        
        for (int right = 0; right < s.length(); right++) {
            char currentChar = s.charAt(right);
            
            // If character was seen inside current window, move 'left' past its previous position
            if (charMap.containsKey(currentChar)) {
                left = Math.max(left, charMap.get(currentChar) + 1);
            }
            
            // Update last seen position of current character
            charMap.put(currentChar, right);
            
            // Update max length
            maxLength = Math.max(maxLength, right - left + 1);
        }
        
        return maxLength;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();

        // Test Cases
        String s1 = "abcabcbb";
        String s2 = "bbbbb";
        String s3 = "pwwkew";
        String s4 = "";

        System.out.println("Input: s = \"" + s1 + "\" -> Output: " + solution.lengthOfLongestSubstring(s1)); // Output: 3
        System.out.println("Input: s = \"" + s2 + "\" -> Output: " + solution.lengthOfLongestSubstring(s2)); // Output: 1
        System.out.println("Input: s = \"" + s3 + "\" -> Output: " + solution.lengthOfLongestSubstring(s3)); // Output: 3
        System.out.println("Input: s = \"" + s4 + "\" -> Output: " + solution.lengthOfLongestSubstring(s4)); // Output: 0
    }
}
⏱️ Complexity AnalysisTypeComplexityDescriptionTime Complexity$O(n)$String of length $n$ is traversed in a single pass using the right pointer.Space Complexity$O(\min(n, m))$Map holds at most $m$ distinct characters (bounded by $O(1)$ for fixed ASCII set size).
