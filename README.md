quacknn-bopomofo
================

This project trys to emit Chinese text that looks like the input through the following procedure:

* [preprocess](#Preprocessing) input material and replace Chinese text with [bopomofo](https://en.wikipedia.org/wiki/Bopomofo)
* pass it into an RNN as one-hot vectors
* get the output and let an input method handle it

Using phonetic representations of Chinese help work around impractical vector sizes associated with the size of the charset. The model may learn to use phonetic puns.

Bopomofo is preferred to pinyin due to:

* script separation: keeps the script difference (Latin vs. CJK)
* well-formedness: valid bopomofo sequences can be constructed more easily
* tone support: bopomofo IMs value tones more than pinyin IMs.

Dependncies
-----------

* Preprocessing: 
* NN:
* Input Method:

Preprocessing
-------------

The formatting of input files follow the good old one-unit-per-line rule. Each unit is passed into a monkey-patched version of pypinyin which yields bopomofo instead of pinyin.

Script or code point normalization is not mandatory as pypinyin accepts Unihan and GBK-PUA characters.

NN Dimensions
-------------

Our basic idea is one-hot vectors covering printable ASCII, bopomofo, and NUL/NL (as end of sequence marker) — `127 - 31 + 41 = 137` dimensions. Extra 8-bit range may be considered for UTF-8 support as everyone loves to use emojis. With UTF-8 added, we have `137 + 128 - 13 = 252` dimensions. An extra 6+1 dimensions can be removed assuming all CJK Unified Ideographs are consumed, plus PUA ditched. 🌚

Input Method
------------

RIME should be the way to go.
