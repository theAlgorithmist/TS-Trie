# Typescript Math Toolkit Trie Data Structure

This is a rudimentary or textbook implementation of a Aho Corasick double-array Trie data structure.  The code provided in this repo is the minimal implementation exposed in the Tyepscript Math Toolkit, a private library I maintain for clients.  Over time, I have open-sourced many elements of this library.

This implementation exposes a minimal API, allowing insertion, removal, and containment tests.  The _TSMT$Trie_ class also allows the Trie to be initialized from a prior state instead of a new dictionary.  Internal state may be queried, making this an ideal implementation for those wishing to learn the data structure from first principles.  It also facilitates TDD.

References:

1 - Aho, Alfred V.; Corasick, Margaret J. (June 1975). "Efficient string matching: An aid to bibliographic search". Communications of the ACM. 18 (6): 333–340. doi:10.1145/360825.360855. MR 0371172.

2 - Aoe, Jun-ichi, Morimoto, Katsushi, "An Efficient Implementation of Trie Structures", SOFTWARE—PRACTICE AND EXPERIENCE, Vol. 22(9), 695–721 (September 1992)

3 - Knuth, D.E., "The Art of Computer Programming", Vol. I, Fundamental Algorithms, pp. 295–304; Vol. III, Sorting and Searching, pp. 481–505, Addison-Wesley, Reading, Mass., 1973.

Note:  Reference #2 is the source of the infamous, 'bachelor', 'badge', 'baby', 'jar' dictionary.

NOTE:  This data structure has been [updated and is now part of the AMYR library](https://github.com/theAlgorithmist/AMYR).


Author:  Jim Armstrong - [The Algorithmist]

@algorithmist

theAlgorithmist [at] gmail [dot] com

Typescript: 3.8.3

Jest: 25.2.1

Version: 1.0


## Installation

Installation involves all the usual suspects

  - npm installed globally
  - Clone the repository
  - npm install
  - get coffee (this is the most important step)


### Building and running the tests

1. npm t (it really should not be this easy, but it is)

2. Standalone compilation only (npm build)

Specs (_trie.spec.ts_) reside in the ___tests___ folder.


### Usage

Initialize the Trie with an alphabet, consisting of a set of characters and a unique code for each character.  There is some efficiency to be gained by using the set of integers as codes since they double as array indices.  A default alphabet is provided if none is specified on construction.

```
import {
  TSMT$Trie,
  WORD_TERMINATOR
} from "../src/Trie";
.
.
.
const trie: TSMT$Trie = new Trie();  // default alphabet, 'a', 'b', 'c' ... 'z'.

or

const alphabet: Record<string, number> = {
{
  '#': 1,
  'a': 2,
  'b': 3,
  'c': 4,
  'd': 5,
  'e': 6,
  'f': 7,
  'g': 8,
}

const trie: TSMT$Trie = new Trie(alphabet)
```

Insert words into the trie one at a time,

```
  trie.insert('bachelor');
  trie.insert('jar');
  trie.insert('badge');
  trie.insert('baby');
```

Access a copy of the Trie internal state,

```
  console.log('BASE    :', trie.base);
  console.log('CHECK   :', trie.check);
  console.log('TAIL    :', trie.tail);
  console.log('POSITION:', trie.position);  
```

Initialize the Trie directly from a prior state and test if the Trie contains a given word,

```
  const base: Array<number>  = [4, 0, 1, -15, -1, -12, 1, 0, 0, 0, 0, 0, 0, 0, -9];
  const check: Array<number> = [0, 0, 7,   3,  3,   3, 1, 0, 0, 0, 0, 0, 0, 0, 1 ];
  const tail: Array<string>  = [
    'h', 'e', 'l', 'o', 'r', WORD_TERMINATOR,
    PLACEHOLDER,
    PLACEHOLDER,
    'a', 'r', WORD_TERMINATOR,
    'g', 'e', WORD_TERMINATOR,
    'y', WORD_TERMINATOR
  ];

  trie.setState(base, check, tail, 17);

  expect(trie.contains('bachelor')).toBe(true);
  expect(trie.contains('badge')).toBe(true);
  expect(trie.contains('baby')).toBe(true);
  expect(trie.contains('jar')).toBe(true);
  expect(trie.contains('boba')).toBe(false);
  expect(trie.contains('fett')).toBe(false);
```

Working with state in this manner requires some knowledge of the inner workings of the algorithm and the _base_, _check_, and _tail_ arrays.  This implementation is closest to that described in reference #2, above.

Refer to the remainder of the specs for more usage examples.


License
----

Apache 2.0

**Free Software? Yeah, Homey plays that**

[//]: # (kudos http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

[The Algorithmist]: <https://www.linkedin.com/in/jimarmstrong/>

