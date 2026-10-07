Longest Substring Without Repeating CharactersProblem in Simple TermsFind the length of the longest part of a word where no letters repeat.Key Examples"abcabcbb" $\rightarrow$ 3 (The longest part without repeating letters is "abc")."bbbbb" $\rightarrow$ 1 (Only "b" works because every letter is the same)."pwwkew" $\rightarrow$ 3 (The longest part is "wke").How the Solution Works (The Sliding Window Idea)Think of it like looking at the word through a flexible glass window with a left edge and a right edge:Expand the window to the right one letter at a time (right pointer).Remember where each letter was last seen using a map/dictionary.If you run into a letter you've already seen inside your current window, jump the left edge right past the previous spot of that repeated letter.Keep track of the largest window size you were able to make.Java CodeJavaimport java.util.HashMap;
import java.util.Map;

public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        int left = 0;
        
        // Maps each character to its last seen position
        Map<Character, Integer> charMap = new HashMap<>();
        
        for (int right = 0; right < s.length(); right++) {
            char currentChar = s.charAt(right);
            
            // If duplicate character is in the current window, move left boundary
            if (charMap.containsKey(currentChar)) {
                left = Math.max(left, charMap.get(currentChar) + 1);
            }
            
            // Save the character's position
            charMap.put(currentChar, right);
            
            // Update the largest window size
            maxLength = Math.max(maxLength, right - left + 1);
        }
        
        return maxLength;
    }
}
Speed & MemoryTime: $O(n)$ — We look at each character only once.Space: $O(n)$ — Memory used to remember character locations.
