## 208.Implement Trie (Prefix Tree)

Implement a trie with insert, search, and startsWith methods.

**Note:**
You may assume that all inputs are consist of lowercase letters a-z.

**Solution:**

    class TrieNode(object):
        def __init__(self):
            """
            Initialize your data structure here.
            """
            self.neighbors = {}
            self.isEnd = False

    class Trie(object):

        def __init__(self):
            self.root = TrieNode()

        def insert(self, word):
            """
            Inserts a word into the trie.
            :type word: str
            :rtype: void
            """
            node = self.root
            for char in word:
                if char not in node.neighbors:
                    node.neighbors[char] = TrieNode()
                node = node.neighbors[char]
            node.isEnd = True

        def search(self, word):
            """
            Returns if the word is in the trie.
            :type word: str
            :rtype: bool
            """
            node = self.root
            for char in word:
                if char not in node.neighbors:
                    return False
                else:
                    node = node.neighbors[char]
            return node.isEnd

        def startsWith(self, prefix):
            """
            Returns if there is any word in the trie
            that starts with the given prefix.
            :type prefix: str
            :rtype: bool
            """
            node = self.root
            for char in prefix:
                if char not in node.neighbors:
                    return False
                else:
                    node = node.neighbors[char]
            return True

    # Your Trie object will be instantiated and called as such:
    # trie = Trie()
    # trie.insert("somestring")
    # trie.search("key")