---
title: Falsehoods Programmers Believe About Words
date: 2026-10-11
cover_image: _DSC2033.jpg
slug: words
tags: ['words', 'linguistics', 'programming', 'engineering']
---

In the spirit of the [many falsehoods programmers believe about](https://github.com/kdeldycke/awesome-falsehood), I present falsehoods programmers believe about words. 

My experiences with linguistics and engineering have led me to the realization that there are numerous falsehoods programmers believe about words and shockingly no one has seemingly written one of these yet.[^language] This is a blend of literal words and writing systems – mostly because text is what we interact with most frequently when we interact with language.[^not-language]

## Words are separated by spaces

This might be the biggest one: when trying to parse language, we assume that words have spaces between them. This is _generally_ true for many writing systems like Latin and Cyrillic. Though even languages using those writing systems have complications: punctuation is non-whitespace and even compound nouns are sometimes spelled with a dash and sometimes a space, but in both cases still denote one concept. But this breaks down entirely with numerous writing systems like Chinese.

## Words are more than one character

Ok, we need to validate some text, so we start with reasonable lower bounds for length. Words are > 1 or 2 characters, surely? No! You don't need to even break out of the top 10 most frequent English words to get a single character: the indefinite article "a". 

## Words are no more than N characters long

But surely we can cap how long a word is? Because all language is productive, even in English compounding or derivation can take an already long word and make it slightly longer. But for [agglutinating languages](https://en.wikipedia.org/wiki/Agglutinative_language) where morphemes are piled together, words can stretch on for what we would use full sentences for. 

## You can count the number of parts of a word by counting bytes

Again, starting from (a very limited) Latin writing system, when we are counting how many characters there are in a string, we often just start counting bytes — since 1 byte == 1 character, right? Until you hit an accent. And then there are extended systems like UTF-8 and JIS which use between 1 and 4 bytes. Ok, so surely 4 bytes is a maximum, then! That's all of UTF-32 for everything. But even that's not enough because there are numerous zero-width joiners. For example the Bengali character র‍্য is a combination of র `U+09B0`, ZWJ `U+200D`, ্ `U+09CD`, and য `U+09AF` for a minimum of 12 bytes in UTF-8 and more in UTF-32.

## Words are enumerable

We can list all the possible words in a language. Again, all languages are productive and constantly creating new words, but even if we ignore that, languages with complex morphology mean these lists become intractable quickly.

## At least the set of words I need to ban is enumerable

But surely then we can enumerate all of the words that we want to ban because they are curse words: That's fanfuckingtastic! Or you might run into Homer Simpson calling someone an "assamahole".[^Yu2004] It turns out, even in English this list isn't enumerable. 

## Ok, ok, ok but I can get some coverage by just regexing for bad words

And then you get the "****ake Mushrooms". 


## There is a fixed set of classes of words across all languages

English is often described as having the following word classes (or parts of speech): nouns, verbs, adjectives, adverbs, pronouns, prepositions, conjunctions, interjections, numerals, articles. Surely all languages have that same set of classes? Nope! At most, we believe that all languages have nouns and verbs that behave differently, but many languages show no distinctions between other categories (adjectives and adverbs having no distinction at all, for example) or they simply have no words that are in a particular class (Japanese, Finnish, and Turkish don't have prepositions; English doesn't have counting classifiers like Japanese and Korean do).[^adjectives] 

## Words that are the same spelling mean the same thing

Every string of characters has a unique meaning, right? Nope! Homonyms exist: "lead" (to go in front of) and "lead" (the metal). Which meaning is intended is very clear given the context it shows up in.

## Ok, but words in specific circumstances that have the same spelling mean the same thing within one language 

Sure, homonyms exist, but surely a word in the same sentence has the same meaning to all speakers of that language? Nope, foiled by dialectal variation. One example is the word "quite" in US English versus British English. In US English it means very; in British English it means not-very. The phrase "I had a quite fun weekend" means very different things on either side of the pond: in the US a genuinely more-fun-than-average weekend; in the UK a less-fun-than-average weekend.

## Words are language

This isn't restricted to programmers: I've heard this from psychology researchers, teachers, and loads more people who haven't seriously learned a second language as an adult! Many people reduce language down to a bag of words — each word in each language is interchangeable one to one and then as soon as you know all the words you know the language. 

[^language]: There are, however, [two very good](https://garbled.benhamill.com/2017/04/18/falsehoods-programmers-believe-about-language) [ones about language](https://www.lexiconista.com/falsehoods-about-languages/) which cover some aspects of language and words, but they are not specifically  focused words.

[^not-language]: Though text _itself_ is not language, it is an encoding of a spoken (or signed) language. One of the first things we learn in an intro to linguistics course is that although we perceive text "as the language" it is not — it is an encoding of a language. Defining what/where the actual language gets surprisingly complicated, but from the [Ethnologue](https://www.ethnologue.com/faq/how-many-languages-unwritten/) "The exact number of unwritten languages is difficult to determine precisely. Ethnologue (28th edition) has data to indicate that of the currently listed 7,170 living languages, 4,153 have a developed writing system." 

[^adjectives]: After nouns and verbs, adjectives are the cord class that people usually assume "surely all languages have this one!" And these are especially funny because though most (maybe even all?) languages can describe/modify nouns and verbs — the way those systems work is all over the place! To the point that the idea this is one category cross-linguistically looks like it comes more from a western (and colonialist!) perspective rather than something inherent to all languages. In an alternate reality where most of the description was not done with an Indo-European lens, we might not be trying to fit the (single) category "adjective" onto words with a bunch of different properties in a bunch of different languages. For a fantastic discussion, see the Lumper v Splitter section of [Episode 47 of Lingthusiasm: The happy fun big adjective episode](https://lingthusiasm.com/post/628144566474833920/transcript-episode-47-the-happy-fun-big-adjective).

[^Yu2004]: Yu, Alan. “Reduplication In English Homeric Infixation.” Proceedings of the North East Linguistic Society, University of Massachusetts, 2004.