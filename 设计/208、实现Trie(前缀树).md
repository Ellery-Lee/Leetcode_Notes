# 208、实现Trie(前缀树)

- Trie树讲解：https://leetcode-cn.com/problems/implement-trie-prefix-tree/solution/trie-tree-de-shi-xian-gua-he-chu-xue-zhe-by-huwt/

- 题目要求：实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。

- **说明**：你可以假设所有的输入都是由小写字母 `a-z` 构成的。保证所有输入均为非空字符串。

- ```
  Trie trie = new Trie();
  
  trie.insert("apple");
  trie.search("apple");   // 返回 true
  trie.search("app");     // 返回 false
  trie.startsWith("app"); // 返回 true
  trie.insert("app");   
  trie.search("app");     // 返回 true
  ```

## 方法一：Trie树结构（版本一）   82.98%

```java
class Trie {
    private Trie[] next;
    private boolean isEnd;
    /** Initialize your data structure here. */
    public Trie() {
        //一次建树，多次查询
        next = new Trie[26];
        isEnd = false;
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        Trie temp = this;
        for(int i = 0; i < word.length(); i++){
            char currentChar = word.charAt(i);
            if(temp.next[currentChar - 'a'] == null){
                temp.next[currentChar - 'a'] = new Trie();
            }
            temp = temp.next[currentChar - 'a'];
        }
        //字符串结束
        temp.isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie temp = this;
        for(int i = 0; i < word.length(); i++){
            char currentChar = word.charAt(i);
            if(temp.next[currentChar - 'a'] == null){
                return false;
            }
            temp = temp.next[currentChar - 'a'];
        }
        return temp.isEnd;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Trie temp = this;
        for(int i = 0; i < prefix.length(); i++){
            char currentChar = prefix.charAt(i);
            if(temp.next[currentChar - 'a'] == null){
                return false;
            }
            temp = temp.next[currentChar - 'a'];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```



## 方法二：Trie树结构（版本二）49.66%

```java
class TrieNode{
    private TrieNode[] root;
    private boolean isEnd = false;

    public TrieNode(){
        root = new TrieNode[26];  //26个字母
    }

    public void setEnd(){
        isEnd = true;
    }

    public boolean isEnd(){
        return isEnd;
    }

    public boolean contains(char ch){
        return root[ch - 'a'] != null;
    }

    public TrieNode get(char ch){
        return root[ch - 'a'];
    }

    public void put(char ch){
        root[ch - 'a'] = new TrieNode();
    }
}


class Trie {
    TrieNode root;
    /** Initialize your data structure here. */
    public Trie(){
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode temp = root;
        for(int i = 0; i < word.length(); i++){
            if(!temp.contains(word.charAt(i))){
                temp.put(word.charAt(i));
            }
            temp = temp.get(word.charAt(i));
        }
        temp.setEnd();
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode temp = root;
        for(int i = 0; i < word.length(); i++){
            if(!temp.contains(word.charAt(i))){
                return false;
            }
            temp = temp.get(word.charAt(i));
        }
        return temp.isEnd();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode temp = root;
        for(int i = 0; i < prefix.length(); i++){
            if(!temp.contains(prefix.charAt(i))){
                return false;
            }
            temp = temp.get(prefix.charAt(i));
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```



- timeline

1. ~~2020.6.30-~~
2. 2020.7.1
3. 2020.7.2
4. 2020.7.7
5. 2020.7.14
6. 2020.7.29