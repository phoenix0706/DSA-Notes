# Find Common Characters

Given a string array `words`, return an array of all characters that show up in all strings within the words (including duplicates). You may return the answer in any order.

[Problem Link-Leetcode](https://leetcode.com/problems/find-common-characters/description/)

```
Example 1:
Input: words = ["bella","label","roller"]
Output: ["e","l","l"]

Example 2:
Input: words = ["cool","lock","cook"]
Output: ["c","o"]

```

---

## **Intution**:

To solve this problem, the idea is to count the frequency of each character in every string and find the minimum frequency of each character across all strings. Characters with a minimum frequency greater than zero in all strings are common characters.

## **Approach**:

## **Solution**:

### **Brute Force**:

1. For each string in the array, count the frequency of each character.
2. Compare these frequencies to find common characters.
3. Collect the characters that are common across all strings.

### Java

```Java

class Solution {
    public List<String> commonChars(String[] words) {
        List<String> newStr = new ArrayList<>();
        String res = words[0];
        for(int i=0;i<words.length;i++){
            if(i!= words.length-1){
                res = checkStrings(res,words[i+1]);
            }

        }
        //System.out.println(res);
        String s = "";
        for(int i = 0;i<res.length();i++){
            s += res.charAt(i);
            newStr.add(s);
            s= "";
        }
        return newStr;

    }

    public String checkStrings(String s1, String s2){
        String res = "";
        for(int i=0;i<s1.length();i++){
            for(int j=0;j<s2.length();j++){
                if(s1.charAt(i) == s2.charAt(j)){
                    s2 = s2.substring(0,j)+' '+s2.substring(j+1);
                    res += s1.charAt(i);
                    break;
                }
            }
        }
        return res;
    }
}

```

Time Complexity: Time Complexity: O(n*m*(26^2) ), where n is the number of strings and m is the average length of the strings.

Space Complexity: O(26), for storing the frequency of each character.

---

### **Best Approach**

1. Frequency Array Initialization:
   Create a frequency array freq_arr to store the minimum frequency of each character from 'a' to 'z' across all words.

2. First Word Frequency:
   Calculate the frequency of each character in the first word and store it in freq_arr.

3. Processing Subsequent Words:
   For each subsequent word, create a temporary frequency array temp.
   Calculate the frequency of each character in the current word and store it in temp.
   Update freq_arr to contain the minimum frequency of each character by comparing freq_arr and temp.

4. Collecting Results:
   Iterate over freq_arr, and for each character, add it to the result list based on its frequency.

#### Java

```Java
class Solution {
    static void countfill(int []freq_arr,String arr ){
        for(int i=0;i<arr.length();i++){
            freq_arr[arr.charAt(i)-'a']+=1;
        }

    }
    public List<String> commonChars(String[] words) {
     int freq_arr[]=new int[26];
     Arrays.fill(freq_arr,0);
    countfill(freq_arr,words[0]);
        for(int i=1;i<words.length;i++){
            int temp[]=new int[26];
            Arrays.fill(temp,0);
            countfill(temp, words[i]);
            for(int j=0;j<26;j++){
                freq_arr[j]=Math.min(freq_arr[j],temp[j]);
            }
        }

ArrayList<String> ans=new ArrayList<String>();
for(int k=0;k<26;k++){
    int count=freq_arr[k];
    while(count-->0){
        ans.add(Character.toString((char)('a'+k)));
    }
}
return ans;
    }
}
```

#### Python

```python

class Solution:
    def freqarray(self,freq,word):
        for char in word:
            freq[ord(char)-ord('a')]+=1
        return freq
    def commonChars(self, words: List[str]) -> List[str]:
        freq=[0]*26
        self.freqarray(freq,words[0])

        for word in words:
            temp=[0]*26
            temp=self.freqarray(temp,word)
            for i in range(0,26):
                freq[i]=min(temp[i],freq[i])
        ans=[]
        for i in range(0,len(freq)):
            for j in range(0, freq[i]):
                ans.append((chr(ord('a')+i)))
        return ans

```

Time Complexity: The time complexity is 𝑂(𝑁×𝑀), where 𝑁 is the number of words and M is the average length of the words. This is because we need to process each character of each word to count frequencies and then update the minimum frequencies.

Space Complexity: The space complexity is O(26) which can be said as O(1), as we use fixed-size arrays (freq_arr and temp of size 26) to store character frequencies, irrespective of the input size.

---

**Materials To Read/Watch**
