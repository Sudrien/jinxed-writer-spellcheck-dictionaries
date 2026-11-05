Downloadable assets for https://github.com/Sudrien/jinxed-writer-for-m5tab5

## english.sym

The spelling dictionary Jinxed Writer downloads when its card has none.
The firmware fetches it by this repository's commit hash, so do not
rewrite history here: a commit that disappears is a download that fails.
A new dictionary is a new commit, and a new hash in the firmware's
`spell.h`.

- 86,060 words, lower-case a-z, each with a frequency for ranking.
- 15,347,221 bytes, SHA-256
  `f6fb3ea3b070934df3561589f3a5abaffc1021bcfc9f6b80a8f93fd700cccf10`.
- The format is described in `m5tab5/main/spell.c` of Jinxed Writer.

To rebuild it, from Jinxed Writer's `m5tab5/` (the build is
reproducible: the same input gives the same bytes):

    cc -O2 -DSPELL_HOST -Imain -o spelldict tools/spelldict.c main/spell.c
    ./spelldict dictionary.txt english.sym

where `dictionary.txt` is `dictionaries/dictionary.txt` of
[symspell-c99](https://github.com/sumanpokhrel-11/symspell-c99) at
commit `a764b99562e62aed3b510c03518657b39addd63a`.

## Where the words come from

english.sym is a compiled form of word lists made by others, and is
distributed under their terms. Their notices are in `licenses/`, as
each requires.

- **symspell-c99**, by Suman Pokhrel, MIT licence
  (`licenses/symspell-c99.LICENSE`). Its `dictionary.txt` is the input
  above: a base list of 82,765 words, with words added from its
  misspelling test sets, filtered and ranked by English Wikipedia word
  frequencies. The SymSpell approach in Jinxed Writer's checker also
  follows this library, though none of its code is used.
- **SymSpell**, by Wolf Garbe, MIT licence (`licenses/SymSpell.LICENSE`):
  the symmetric-delete algorithm, and `frequency_dictionary_en_82_765.txt`
  (first published July 2017), which symspell-c99's base list is, with
  the same frequencies and 46 words changed. Garbe made it by
  intersecting Google Books Ngram data with SCOWL.
- **SCOWL** (Spell Checker Oriented Word Lists), by Kevin Atkinson and
  the authors it credits (`licenses/SCOWL.Copyright`). The notice is
  SCOWL's as released from January 2017 to April 2018
  (wordlist repository, tag `rel-2018.04.16`), the releases Garbe's list
  could have been made from; it includes the UK Advanced Cryptics
  Dictionary's notice, which asks to be included verbatim.
- **Google Books Ngram** data, by Google, under the Creative Commons
  Attribution 3.0 licence, as Garbe's README credits it: the source of
  the original frequencies.
- **English Wikipedia**, whose word frequencies symspell-c99 used to
  filter and rank its list.
