# Trie

Trie is a Tree like data structure designed to efficiently store Strings. It is efficient for doing prefix queries, search autocomplete, dictionary etc.

## The basics

Trie uses recursive strucutre. In our example we will use a String Trie. All lowercase characters. Trie has the following functions:

- `add(String s)`
- `find(String s)`

The basic structure of **Trie** looks like this:

```Java
Class Trie {
    private boolean isEnd;
    private[] Trie tries;

    public Trie () {
        tries = new Trie[26];
    }

    public void add(String s,  int idx) {
        if (idx == s.length()) {
            isEnd = true;
            return;
        }

        int index = s.charAt(idx) - 'a';
        Trie newTrie = new Trie();
        tries[index] = newTrie;
        
        newTrie.add(s, idx + 1);
    }

    public boolean find(String s, int idx) {
        if (idx == s.length()) {
            return isEnd;
        }

        int index = s.charAt(idx) - 'a';
        Trie trie = tries[index];

        if (trie == null) {
            return false;
        }

        return trie.find(s, idx + 1);
    }
}
```

## Advantages

Trie is a advanced data structure and has many use cases with very little or no modification to the original Trie.

- **Compact Representation**
- **Fast String**
- **Search autocomplete**
- **Efficient insertion and deletion of strings**
