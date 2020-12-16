# Strings

### Count Vowels

Find the number of vowels in a string. Vowels in English are A, E, O, U and I.

Input: “hello”

Output: 2

        public static int countVowels(String str) {
            if(str == null)
                return 0;
            
            Set<Character> vowels = new HashSet<>();
            vowels.add('a'); vowels.add('e'); vowels.add('o'); vowels.add('u'); vowels.add('i');

            int count = 0;
            for(var ch : str.toLowerCase().toCharArray())
                if(vowels.contains(ch))
                    count++;

            return count;
        }

### Reverse String

Input: “hello”

Output: “olleh”

        public static String reverse(String str) {
            if(str == null)
                return "";

            StringBuilder reversed = new StringBuilder();
            for(int i=str.length()-1;i>=0;i--)
                reversed.append(str.charAt(i));

            return reversed.toString();
        }

### Reverse Words

Reverse the order of words in a sentence.

Input: “Trees are beautiful”

Output: “beautiful are Trees”

        public static String reverseWords(String str) {
            if(str == null)
                return "";

            String[] words = str.trim().split(" ");
            StringBuilder reversed = new StringBuilder();
            for(int i=words.length-1;i>=0;i--) {
                reversed.append(words[i]);
                if(i != 0)
                    reversed.append(" ");
            }
            return reversed.toString();
        }

        or

        public static String reverseWords2(String str) {
            if (str == null)
                return "";

            String[] words = str.trim().split(" ");
            Collections.reverse(Arrays.asList(words));
            return String.join(" ", words);
        }

        or using stack

### Rotation

Check if a string is a rotation of another string.

Input: “ABCD”, “DABC” (rotate one char to the right)

Output: true

        public static boolean areRotations(String str1, String str2) {
            if(str1 == null || str2 == null || (str1.length() != str2.length()))
                return false;
            return (str1 + str1).contains(str2);
        }

### Remove Duplicates

Remove duplicate characters in a string.

Input: “Hellooo World!!!”

Output: “Helo Wrd!”

        public static String removeDuplicates(String str) {
            if(str == null)
                return "";
            
            StringBuilder noDuplicates = new StringBuilder();
            Set<Character> found = new HashSet<>();

            for(var ch : str.toCharArray()) {
                if (!found.contains(ch)) {
                    noDuplicates.append(ch);
                    found.add(ch);
                }
            }
            return noDuplicates.toString();
        }

### Most Repeated Char

Find the most repeated character in a string.

Input: “Hellooo!!”

Output: ‘o’

        public static char mostRepeatedChar(String str) {
            if(str == null || str.isEmpty())
                throw new IllegalStateException();

            Map<Character, Integer> counts = new HashMap<>();
            for(var ch : str.toCharArray()) {
                if (!counts.containsKey(ch))
                    counts.put(ch, 1);
                else
                    counts.put(ch, counts.get(ch) + 1);
            }

            int max = 0;
            char maxChar = '\0';
            for(var entry : counts.entrySet()) {
                if(entry.getValue() > max) {
                    max = entry.getValue();
                    maxChar = entry.getKey();
                }
            }
            return maxChar;
        }

### Sentence Capitalization

Capitalize the first letter of each word in a sentence. Also, remove any extra spaces between words.

Input: “   hello    woRld   to   my     strIngs   ”

Output: “Hello World To My Strings”

        public static String capitalize(String sentence) {
            if(sentence == null || sentence.trim().isEmpty())
                return "";

            String[] words = sentence.trim().replaceAll("\\s+", " ").split(" ");
            for(int i=0;i<words.length;i++)
                words[i] = words[i].substring(0,1).toUpperCase()
                            + words[i].substring(1).toLowerCase();

            return String.join(" ", words);
        }

### Anagrams

Detect if two strings are anagram of each other. A string is an anagram of another string if it has the exact same characters in any order.

Input: “abcd”, “adbc”

Output: true


Input: “abcd”, “cadb”

Output: true


Input: “abcd”, “abcd”

Output: true


Input: “abcd”, “abce”

Output: false

* **using Sorting**

        // O(n log n)
        public static boolean areAnagrams(String str1, String str2) {
            if(str1 == null || str2 == null || str1.length() != str2.length())
                return false;

            // O(n)
            char[] array1 = str1.toCharArray();
            // O(n log n)
            Arrays.sort(array1);
            // O(n)
            char[] array2 = str2.toCharArray();
            // O(n log n)
            Arrays.sort(array2);

            return Arrays.equals(array1, array2);
        }

* **using Histogramming**

        // O(n)
        public static boolean areAnagrams2(String str1, String str2) {
            if(str1 == null || str2 == null || str1.length() != str2.length())
                return false;

            Map<Character, Integer> counts = new HashMap<>();
            // O(n)
            for(char ch : str1.toCharArray()) {
                if (!counts.containsKey(ch))
                    counts.put(ch, 1);
                else
                    counts.put(ch, counts.get(ch) + 1);
            }

            // O(n)
            for(char ch : str2.toCharArray()) {
                if (!counts.containsKey(ch))
                    counts.put(ch, -1);
                else
                    counts.put(ch, counts.get(ch) - 1);
            }

            for(var value : counts.values())
                if(value != 0)
                    return false;

            return true;
        }

### Palindrome

Check if a string is palindrome. If we read a palindrome string from left or right, we get the exact same characters.

Input: “abba”

Output: true


Input: “abcba”

Output: true


Input: “abca”

Output: false

        public static boolean isPalindrome(String str) {
            if(str == null || str.isEmpty())
                return false;

            String reversed = new StringBuilder(str).reverse().toString();
            return str.equals(reversed);
        }

        or

        public static boolean isPalindrome2(String str) {
            if(str == null || str.isEmpty())
                return false;

            for(int i=0; i<str.length()/2; i++)
                if(str.charAt(i) != str.charAt(str.length() - i - 1))
                    return false;
            return true;
        }
