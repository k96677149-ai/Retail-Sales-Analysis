class Solution {
    public List<Integer> findAnagrams(String s, String p) {

        List<Integer> ans = new ArrayList<>();

        if (s.length() < p.length()) {
            return ans;
        }

        int[] pFreq = new int[26];
        int[] windowFreq = new int[26];

        // Frequency of characters in p
        for (char c : p.toCharArray()) {
            pFreq[c - 'a']++;
        }

        int windowSize = p.length();

        // First window
        for (int i = 0; i < windowSize; i++) {
            windowFreq[s.charAt(i) - 'a']++;
        }

        // Check first window
        if (Arrays.equals(pFreq, windowFreq)) {
            ans.add(0);
        }

        // Slide the window
        for (int i = windowSize; i < s.length(); i++) {

            // Add new character
            windowFreq[s.charAt(i) - 'a']++;

            // Remove old character
            windowFreq[s.charAt(i - windowSize) - 'a']--;

            // Check if current window is an anagram
            if (Arrays.equals(pFreq, windowFreq)) {
                ans.add(i - windowSize + 1);
            }
        }

        return ans;
    }
}