# 208. 实现 Trie (前缀树)

[https://leetcode.cn/problems/implement-trie-prefix-tree/?envType=study-plan-v2&envId=top-100-liked](https://leetcode.cn/problems/implement-trie-prefix-tree/?envType=study-plan-v2&envId=top-100-liked)

```java
class Trie {
    // 内部类：定义前缀树节点
    class TrieNode {
        // 子节点数组，大小为 26（对应 'a'-'z'）
        TrieNode[] children;
        // 标记当前节点是否为一个单词的结尾
        boolean isEnd;

        TrieNode(){
            children = new TrieNode[26];
            isEnd = false;
        }
    }

    TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    /** 插入单词 */
    public void insert(String word) {
        TrieNode node = root;
        for(char c : word.toCharArray()){
            int index = c - 'a';
            // 如果对应字符的子节点不存在，则创建一个
            if(node.children[index] == null){
                node.children[index] = new TrieNode();
            }
            // 移动到子节点
            node = node.children[index];
        }
        // 单词遍历完，将最后一个节点标记为结尾
        node.isEnd = true;
    }
    
    /** 查找单词是否存在 */
    public boolean search(String word) {
        TrieNode node = root;
        // 看看这条路是否走得通
        for(char c : word.toCharArray()){
            int index = c - 'a';
            if(node.children[index] == null){
                return false;
            }
            node = node.children[index];
        }
        // 如果走得通，且能走到结尾，说明单词存在
        return node.isEnd == true;
    }
    
    /** 查找是否存在以 prefix 为前缀的单词 */
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        // 看看这条路是否存在，但不需要走到结尾
        for(char c : prefix.toCharArray()){
            int index = c - 'a';
            if(node.children[index] == null){
                return false;
            }
            node = node.children[index];
        }
        // 如果存在这条路（不用管后面还能不能走了），说明前缀存在
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