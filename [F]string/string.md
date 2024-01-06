# string

## intro

- terms
    - palindrome
        - use two pointers
    - anagram
        - use hashmap
        - need to have same length
    - substring
        - is contiguous like subarray, not like subsequence
    - subsequence
        - by deleting some chars
    - prefix and suffix
    - trie
        - can insert and search in `O(L)`
    - isomorphic
        - use hashmap
        - build bijection mapping relation

## pattern

- **traverse from end**
    - traverse from last idx
    - or reverse whole string first
- **handle value’s bound**
    - be aware of the negative number
- **use chunk**
    - every chunk starts with 4 char (byte) to represent the the length of string in chunk
- **use rabin karp**
    - find pattern match / substring in string can use Rabin Karp (rolling hash)
        - time `O(n)` or `O(n+m)`
        - space `O(n)`, due to hashset or `O(1)`, due to finding fixed hash val
        - should consider the collision problem
            - solution 1: use 2-choice hashing
            - solution 2: when find match, check the substring really match or not. worst time could degenerate to `O(nm)`
    ```python
    def is_length_k_substring_repeat(s, k):
        base = 27
        mod = 10**9 + 7
        hashval_set = set()
        hashval = 0
        remove_base = (base ** (k - 1)) % mod
        for i in range(len(s)):
            if i < k:
                hashval = (hashval * base + ord(s[i])) % mod
                if i == k - 1:
                    hashval_set.add(hashval)
            else:
                hashval -= (remove_base * ord(s[i - k])) % mod
                hashval = (hashval * base + ord(s[i])) % mod
                if hashval in hashval_set:
                    return True
                hashval_set.add(hashval)
        return False
    ``` 
- **trivial case**
    - make sure be familiar with syntax of string