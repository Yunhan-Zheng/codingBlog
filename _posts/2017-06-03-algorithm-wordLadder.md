---
layout: post
title: Word Ladder
tags: algorithm jiuzhang linkedIn bfs revisit
date: 2017-06-03 10:00:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/word-ladder/" target="_blank">Word Ladder</a>

Example:

Given start = "hit", end = "cog" and dict = ["hot","dot","dog","lot","log"], return word number on the shortest transformation route.

As one shortest transformation is "hit" -> "hot" -> "lot" -> "log" -> "cog",
return 5.

### Sample solution

```java
public class Solution {
    public int ladderLength(String start, String end, Set<String> dict) {
        if (dict == null){
            return 0;
        }
        if (start.equals(end)){
            return 1;
        }
        dict.add(start);
        dict.add(end);

        HashSet<String> hash = new HashSet<>();
        Queue<String> queue = new LinkedList<>();
        queue.offer(start);
        hash.add(start);

        int length = 1;
        while (!queue.isEmpty()){
            length++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String word = queue.poll();
                for (String nextWord: getNextWords(word, dict)) {
                    if (hash.contains(nextWord)) {
                        continue;
                    }
                    if (nextWord.equals(end)) {
                        return length;
                    }
                    
                    hash.add(nextWord);
                    queue.offer(nextWord);
                }
            }
        }
        return 0;
    }

    // replace character of a string at given index to a given character
    // return a new string
    private String replace(String s, int index, char c) {
        char[] chars = s.toCharArray();
        chars[index] = c;
        return new String(chars);
    }
    
    // get connections with given word.
    // for example, given word = 'hot', dict = {'hot', 'hit', 'hog'}
    // it will return ['hit', 'hog']
    // O(25*L^2) is better than O(NL) when N can be big and L can be small
    // O(NL) 的算法是for dictWord : dict /O(N)
    //               if (distance(word, dictWord) == 1) /O(L)
    private ArrayList<String> getNextWords(String word, Set<String> dict) {
        ArrayList<String> nextWords = new ArrayList<String>();
        for (char c = 'a'; c <= 'z'; c++) {  //O(25)
            for (int i = 0; i < word.length(); i++) { //O(L)
                if (c == word.charAt(i)) {
                    continue;
                }
                String nextWord = replace(word, i, c); //O(L)
                if (dict.contains(nextWord)) {  //O(L)
                    nextWords.add(nextWord);
                }
            }
        }
        return nextWords;
    }
}
```