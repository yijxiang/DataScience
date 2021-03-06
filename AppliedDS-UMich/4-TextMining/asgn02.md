# Assignment 2

## [Jaccard distance](https://en.wikipedia.org/wiki/Jaccard_index)

+ Jaccard Index a.k.a. _Intersection over Union_ and the _Jaccard similarity coefficient_
+ a statistic used for comparing the similarity and diversity of sample sets
+ Jaccard coefficient Def: $J(A, B) = \frac{|A \cap B|}{| A \cup B|} = \frac{|A \cap B|}{|A| + |B| - |A \cap B|}$

+ __Jaccard distance__:
    + measures dissimilarity between sample sets
    + complementary to the Jaccard coefficient
    + $d_J(A, B) = 1 - J(A, B) = \frac{|A \cup B| - |A \cap B|}{|A \cup}$
    + The ratio of the size of the symmetric difference $A \Delta B = (A \cup B) - (A \cap B)$
    + a metric of the collection of all finite sets

+ Jaccard distance for measures:
    + $\mu$ = a measure on a measurable space $X$
    + Jaccard coefficient: $J_{\mu} (A, B) = \frac{\mu (A \cup B)}{\mu (A \cap B)}$
    + Jaccard distance: $d_{\mu} (A, B) =  1 - J_{\mu} (A, B) =  \frac{\mu(A \Delta B)}{\mu (A\cup B)}$

+ Generalized Jaccard similarity and distance
    + Vectors: ${\bf x} = (x_1, x_2, \cdots, x_n)$ and ${\bf y} = (y_1, y_2, \cdots, y_n), \forall x_i, y_i \in \Re^+_0$
    + Jaccard similarity coefficient (Ruzicka similarity): $J({\bf x}, {\bf y}) = \frac{\sum_i \min (x_i, y_i)}{\sum_i \max(x_i, y_i)}$
    + Jaccard distance (Soergel distance): $d_J ({\bf x}, {\bf y}) = 1 - J({\bf x}, {\bf y})$
    + Non-negative measurable functions on measurable space ${\bf X}$ with measure $\mu$: $f$ and $g$
    + Jaccard similarity coefficient (Ruzicka similarity): $J(f, g) = \frac{\int_i \min (f, g) d\mu}{\int_i \max(f, g)d\mu}$ where $\min$ and $\max$ are pointwise operators
    + Jaccard distance: $d_J (f, g) = 1 - J(f, g)$

+ Object Detection
    <a href="https://www.pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/"> <br/>
        <img src="https://www.pyimagesearch.com/wp-content/uploads/2016/09/iou_stop_sign.jpg" alt="In the figure above we can see that our object detector has detected the presence of a stop sign in an image. The predicted bounding box is drawn in red while the ground-truth (i.e., hand labeled) bounding box is drawn in green." title= "An example of detecting a stop sign in an image. The predicted bounding box is drawn in red while the ground-truth bounding box is drawn in green. Our goal is to compute the Intersection of Union between these bounding box." height="200">
    </a>
    <a href="https://www.pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/"> 
        <img src="https://www.pyimagesearch.com/wp-content/uploads/2016/09/iou_equation.png" alt="Examining this equation you can see that Intersection over Union is simply a ratio. In the numerator we compute the area of overlap between the predicted bounding box and the ground-truth bounding box. The denominator is the area of union, or more simply, the area encompassed by both the predicted bounding box and the ground-truth bounding box. Dividing the area of overlap by the area of union yields our final score — the Intersection over Union." title= "Computing the Intersection of Union is as simple as dividing the area of overlap between the bounding boxes by the area of union (thank you to the excellent Pittsburg HW4 assignment for the inspiration for this figure)." height="200">
    </a>

## [How Spell Checkers Work](https://engineerbyday.wordpress.com/2012/01/30/how-spell-checkers-work-part-1/#Jaccard)
+ Spelling checker
    + A spellchecker works by searching for a given string in its __dictionary__ of known strings.
    + The measurement of string similarity is relevant to several disciplines, including Genetics.
    + The DNA strands you sometimes blame for your expanding gut are also strings, constructed from the famous 4 element alphabet {A, C, G, T}.
    + Edit-distance: classic string similarity measure
    + Set Similarity
        + sets

            | Set | String | Elements | Element Count |
            |-----|--------|----------|---------------|
            | A | potatoes | {p, o, t, a, t, o, e, s} | 8 |
            | B | potato | {p, o, t, a, t, o} | 6 |
            | C | tomatos | {t, o, m, a, t, o, s} | 7 |
        + __Problem__: measure the similarity of set A (potatoes) to Set B (potato) & Set C (tomatos).
        + Measurement: Count(A intersection B)
        + Examples
            + A (potatoes) & B (potato) have 6 elements in common.
            + A (potatoes) & C (tomatos) also have 6 elements in common.

+ The Jaccard Coefficient
    + Given a set of elements in sets A and B, calculate the fraction of elements found in both sets. The higher the fraction, the more similar the sets.
    + The set of __all__ unique elements in (A,  B) => __(A union B)__.
    + The set of __common__ elements in (A, B) => __(A intersection B)__
    + Jaccard Coefficient: the similarity between two sets A & B is given by: __Count(A intersect B) / Count(A union B)__
        + Example

            | A (Potatoes) | Count(Union) | Count(Intersection) | Score |
            |--------------|--------------|---------------------|-------|
            | B (Potato) | 8 | 6 | 6/8 = 0.75 |
            | C (Tomatos) | 9 | 6 | 6/9 = 0.66 |

+ A Basic Spellcheck Algorithm <br/>
    To find suggestions for a given misspelling:
    + Calculate the Jaccard Coefficient of the misspelling with each string in the dictionary.
    + Collect those strings with a Jaccard score higher than some threshold.
    + Sort the matches by score, and pick the top N (1) matches as suggestions.
    
    + Comparing a misspelling against every string in the spellchecker’s dictionary (imagine Bing’s) could be prohibitively expensive. The algorithm also fails to consistently produce good corrections for spelling mistakes such as:
        + Single character errors, such as accidentally hitting the wrong key
        + Leaving out letters: sucess instead of success
        + Additional characters: happinness instead of happiness.
        + Phonetic interpretations of spellings
        + And so on…

+ N-grams
    + bi-grams: the set of all overlapping character pairs in the string: `{$p, po, ot, ta, at, to, o$}`.
    + The character `o` co-occurs with other characters – i.e. it is associated with them.
    + The association is ordered – `o` follows `p` and `o` precedes `t`. And `op` is not the same as `po`.
    + The last `o` in potato precedes an implicit terminating null character. An implicit null precedes the first `p`.
    + Two strings are similar if they have characters in common. They are a lot more similar if they have co-occurring characters in common.
    + N-grams capture co-occurrence. 
        + Given a set, bi-grams capture the co-occurrence of pairs of the set’s elements. <br/> potato => `{$p, po, ot, ta, at, to, o$}`
    + An Improved Spell Checking Algorithm w/ bi-gram
        + Transform each string in your dictionary into its constituent bi-grams.
        + Do the same for the misspelling
        + Calculate the Jaccard Similarity Coefficient of the bi-gram set of the misspelling to the bi-gram sets of your dictionary
        + You’ll find that the top N matches returned by this algorithm are actually pretty good.
    + Problems w/ N-gram:
        + The ranking order of your corrections isn’t always ideal. Some intuitively superior matches get lower scores.
        + You still have to compare the misspelling against every string in you dictionary.

+ Edit Distance
    + Transform any string A into any string B by __adding__, __removing__, __replacing__ or __transposing__ characters in A until you arrive at string B.
    + The edit distance between string A and B is the __minimum__ number of steps it takes to transform A into B.
        + The edit distance between equal strings is `0`.
        + The edit distance between potato and potatoe is `1`.
        + The distance between potato and potatoes is `2`.
    + The smaller the edit distance, the more similar the strings. 
    + Edit distance is a great way to rank corrections because most spelling mistakes are mutations of the correct spelling.
    + Calculating edit distances can be tricky. There may be more than one way to turn string A into B, and you must use the minimal number of steps required.
    + Levenshtein algorithm using dynamic programming
        + Formulate a systematic way to list and count the number of steps needed to transform string A into B
    + Delete And Transform: abcd ==> pqrs
        + Transform abcd ==> abc, by deleting d from abcd.
        + Transform abc ==> pqrs [which you’ve already calculated in an earlier iteration]
        + Total Cost = 1 Delete + Count Steps( abc ==> pqrs)
    + Transform and Add: abcd ==> pqrs
        + Transform abcd ==> pqr [which you’ve already calculated in an earlier iteration]
        + Transform pqr ==> pqrs, by adding s to pqr.
        + Total Cost = 1 Add + Count Steps (abcd ==> pqr)
    + Transform and Replace: abcd ==> pqrs
        + Transform the abc portion of abcd  ==> pqr [which you’ve already calculated earlier]
        + Replace the last character from abcd – d with s.
        + Total Cost = 1 Replace + Count Steps (abc ==> pqr)
    + Putting it Together <br/>
        calculating the edit distance of each prefix of A to each prefix of B.
        + For each string in {a, ab, abc, abcd}
            + Calculate the edit distance to each string in {p, pq, pqr, pqrs} using the steps outlined above
            + Save the minimum cost found.
        + By the time you actually calculate the edit distance from abcd ==> pqrs, you’ve already computed all the prior information you need.


## [Edit Distance and Jaccard Distance Calculation with NLTK](https://python.gotrained.com/nltk-edit-distance-jaccard-distance)

+ Edit Distance Python NLTK
    + Demo 1
        ```python
        import nltk

        w1 = 'mapping'
        w2 = 'mappings'

        nltk.edit_distance(w1, w2)
        ```
    + Demo 2:
        ```python
        import nltk

        mistake = "ligting"
        words = ['apple', 'bag', 'drawing', 'listing', 'linking', 'living', 'lighting', 'orange', 'walking', 'zoo']

        for word in words:
            ed = nltk.edit_distance(mistake, word)
            print(word, ed)
        # apple 7
        # bag 6
        # drawing 4
        # listing 1
        # linking 2
        # living 2
        # lighting 1
        # orange 6
        # walking 4
        # zoo 7
        ```
    + Demo 3
        ```python
        import nltk

        sent1 = "It might help to re-install Python if possible."
        sent2 = "It can help to install Python again if possible."
        sent3 = "It can be so helpful to reinstall C++ if possible."
        sent4 = "help It possible Python to re-install if might." 
        # This has the same words as sent1 with a different order.
        sent5 = "I love Python programming."

        ed_sent_1_2 = nltk.edit_distance(sent1, sent2)
        ed_sent_1_3 = nltk.edit_distance(sent1, sent3)
        ed_sent_1_4 = nltk.edit_distance(sent1, sent4)
        ed_sent_1_5 = nltk.edit_distance(sent1, sent5)

        print(ed_sent_1_2, 'Edit Distance between sent1 and sent2')
        print(ed_sent_1_3, 'Edit Distance between sent1 and sent3')
        print(ed_sent_1_4, 'Edit Distance between sent1 and sent4')
        print(ed_sent_1_5, 'Edit Distance between sent1 and sent5')
        # 14 Edit Distance between sent1 and sent2
        # 19 Edit Distance between sent1 and sent3
        # 32 Edit Distance between sent1 and sent4
        # 47 Edit Distance between sent1 and sent5
        ```

+ `nltk.edit_distance` method
    + Signature: `nltk.edit_distance(s1, s2, substitution_cost=1, transpositions=False)`
    + Docstring: Calculate the Levenshtein edit-distance between two strings.
    + Notes:
        + The edit distance is the number of characters that need to be substituted, inserted, or deleted, to transform s1 into s2.  For example, transforming "rain" to "shine" requires three steps, consisting of two substitutions and one insertion: "rain" -> "sain" -> "shin" -> "shine".  These operations could have been done in other orders, but at least three steps are needed.
        + Allows specifying the cost of substitution edits (e.g., "a" -> "b"), because sometimes it makes sense to assign greater penalties to substitutions.
        + This also optionally allows transposition edits (e.g., "ab" -> "ba"), though this is disabled by default.
    + Parameters
        + `s1`, `s2` (str): The strings to be analysed
        + `transpositions` (bool): Whether to allow transposition edits
        + `substitution_cost` (int)
    + Return: distance (int)


+ list of words
    + NLTK:  `words = nltk.corpus.words.words()`
    + Check answers of this [question](https://stackoverflow.com/questions/2213607/how-to-get-english-language-word-database).
    + Check lists at [Kaggle](https://www.kaggle.com/bittlingmayer/spelling).
    + Google: Search for “list of English words”.


+ Jaccard Distance
    + Jaccard Distance is a measure of how dissimilar two sets are.  The lower the distance, the more similar the two strings.
    + Jaccard Distance depends on another concept called “Jaccard Similarity Index” which is (the number in both sets) / (the number in either set) * 100

+ Jaccard Distance Python NLTK: Demo 1
    ```python
    import nltk

    mistake = "ligting"
    words = ['apple', 'bag', 'drawing', 'listing', 'linking', 'living', 'lighting', 'orange', 'walking', 'zoo']

    for word in words:
        jd = nltk.jaccard_distance(set(mistake), set(word))
        print(word, jd)
    # apple 0.875
    # bag 0.8571428571428571
    # drawing 0.6666666666666666
    # listing 0.16666666666666666
    # linking 0.3333333333333333
    # living 0.3333333333333333
    # lighting 0.16666666666666666
    # orange 0.7777777777777778
    # walking 0.5
    # zoo 1.0
    ```
+ Jaccard Distance Python NLTK: Demo 2
    ```python
    import nltk

    sent1 = set("It might help to re-install Python if possible.")
    sent2 = set("It can help to install Python again if possible.")
    sent3 = set("It can be so helpful to reinstall C++ if possible.")
    sent4 = set("help It possible Python to re-install if might.")
    # This has the same words as sent1 with a different order.
    sent5 = set("I love Python programming.")

    jd_sent_1_2 = nltk.jaccard_distance(sent1, sent2)
    jd_sent_1_3 = nltk.jaccard_distance(sent1, sent3)
    jd_sent_1_4 = nltk.jaccard_distance(sent1, sent4)
    jd_sent_1_5 = nltk.jaccard_distance(sent1, sent5)

    print(jd_sent_1_2, 'Jaccard Distance between sent1 and sent2')
    print(jd_sent_1_3, 'Jaccard Distance between sent1 and sent3')
    print(jd_sent_1_4, 'Jaccard Distance between sent1 and sent4')
    print(jd_sent_1_5, 'Jaccard Distance between sent1 and sent5')
    # 0.18181818181818182 Jaccard Distance between sent1 and sent2
    # 0.36 Jaccard Distance between sent1 and sent3
    # 0.0 Jaccard Distance between sent1 and sent4
    # 0.22727272727272727 Jaccard Distance between sent1 and sent5
    ```

+ `nltk.jaccard_distance` method
    + Signature: `nltk.jaccard_distance(label1, label2)`
    + Docstring: Distance metric comparing set-similarity.


+ n-gram
    + In general, n-gram means splitting a string in sequences with the length n.
    + n-grams can be used with Jaccard Distance. 
    + Demo: Character Level
        ```python
        import nltk

        sent1 = "It might help to re-install Python if possible."
        sent2 = "It can help to install Python again if possible."
        sent3 = "It can be so helpful to reinstall C++ if possible."
        sent4 = "help It possible Python to re-install if might." # This has the same words as sent1 with a different order.
        sent5 = "I love Python programming."

        ng1_chars = set(nltk.ngrams(sent1, n=3))
        ng2_chars = set(nltk.ngrams(sent2, n=3))
        ng3_chars = set(nltk.ngrams(sent3, n=3))
        ng4_chars = set(nltk.ngrams(sent4, n=3))
        ng5_chars = set(nltk.ngrams(sent5, n=3))

        jd_sent_1_2 = nltk.jaccard_distance(ng1_chars, ng2_chars)
        jd_sent_1_3 = nltk.jaccard_distance(ng1_chars, ng3_chars)
        jd_sent_1_4 = nltk.jaccard_distance(ng1_chars, ng4_chars)
        jd_sent_1_5 = nltk.jaccard_distance(ng1_chars, ng5_chars)

        print(jd_sent_1_2, "Jaccard Distance between sent1 and sent2 with ngram 3")
        print(jd_sent_1_3, "Jaccard Distance between sent1 and sent3 with ngram 3")
        print(jd_sent_1_4, "Jaccard Distance between sent1 and sent4 with ngram 3")
        print(jd_sent_1_5, "Jaccard Distance between sent1 and sent5 with ngram 3")

        ```
    + Demo: Token level
        ```python
        import nltk

        sent1 = "It might help to re-install Python if possible."
        sent2 = "It can help to install Python again if possible."
        sent3 = "It can be so helpful to reinstall C++ if possible."
        sent4 = "help It possible Python to re-install if might." 
        # This has the same words as sent1 with a different order.
        sent5 = "I love Python programming."

        tokens1 = nltk.word_tokenize(sent1)
        tokens2 = nltk.word_tokenize(sent2)
        tokens3 = nltk.word_tokenize(sent3)
        tokens4 = nltk.word_tokenize(sent4)
        tokens5 = nltk.word_tokenize(sent5)

        ng1_tokens = set(nltk.ngrams(tokens1, n=3))
        ng2_tokens = set(nltk.ngrams(tokens2, n=3))
        ng3_tokens = set(nltk.ngrams(tokens3, n=3))
        ng4_tokens = set(nltk.ngrams(tokens4, n=3))
        ng5_tokens = set(nltk.ngrams(tokens5, n=3))

        jd_sent_1_2 = nltk.jaccard_distance(ng1_tokens, ng2_tokens)
        jd_sent_1_3 = nltk.jaccard_distance(ng1_tokens, ng3_tokens)
        jd_sent_1_4 = nltk.jaccard_distance(ng1_tokens, ng4_tokens)
        jd_sent_1_5 = nltk.jaccard_distance(ng1_tokens, ng5_tokens)

        print(jd_sent_1_2, "Jaccard Distance between tokens1 and tokens2 with ngram 3")
        print(jd_sent_1_3, "Jaccard Distance between tokens1 and tokens3 with ngram 3")
        print(jd_sent_1_4, "Jaccard Distance between tokens1 and tokens4 with ngram 3")
        print(jd_sent_1_5, "Jaccard Distance between tokens1 and tokens5 with ngram 3")
        ```

+ `nltk.ngrams` method
    + Signature: `nltk.util.ngrams(sequence, n, pad_left=False, pad_right=False, left_pad_symbol=None, right_pad_symbol=None)`
    + Docstring: Return the ngrams generated from a sequence of items, as an iterator.
    + Parameters:	
        + `sequence` (sequence or iter): the source data to be converted into ngrams
        + `n` (int): the degree of the ngrams
        + `pad_left` (bool): whether the ngrams should be left-padded
        + `pad_right` (bool): whether the ngrams should be right-padded
        + `left_pad_symbol` (any): the symbol to use for left padding (default is None)
        + `right_pad_symbol` (any): the symbol to use for right padding (default is None)
    + Return: sequence or iter


## Solutions

+ Q1: What is the lexical diversity of the given text input? (i.e. ratio of unique tokens to the total number of tokens)
    ```python
    def answer_one():
        
        words = nltk.word_tokenize(moby_raw)
        
        return len(set(words))/len(words) # Your answer here

    answer_one()        # 0.08139566804842562
    ```

+ Q2: What percentage of tokens is 'whale'or 'Whale'?
    ```python
    def answer_two():
        
        dist = nltk.FreqDist(nltk.word_tokenize(moby_raw))
        
        return (dist['whale']+dist['Whale'])/len(nltk.word_tokenize(moby_raw))*100 # Your answer here

    answer_two()        # 0.4125668166077752
    ```

+ Q3: What are the 20 most frequently occurring (unique) tokens in the text? What is their frequency?
    ```python
    def answer_three():
        
        dist = nltk.FreqDist(nltk.word_tokenize(moby_raw))
        vocab1 = dist.keys()
        
        freqwords = [(w, dist[w]) for w in vocab1]
        
        return (sorted(freqwords, key=lambda x: (-x[1],x[0])))[:20] # Your answer here

    answer_three()
    # [(',', 19204), ('the', 13715), ('.', 7308), ('of', 6513), ('and', 6010), ('a', 4545), ('to', 4515),
    #  (';', 4173), ('in', 3908), ('that', 2978), ('his', 2459), ('it', 2196), ('I', 2097), ('!', 1767),
    #  ('is', 1722), ('--', 1713), ('with', 1659), ('he', 1658), ('was', 1639), ('as', 1620)]
    ```

+ Q4: What tokens have a length of greater than 5 and frequency of more than 150?
    ```python
    def answer_four():
        
        dist = nltk.FreqDist(nltk.word_tokenize(moby_raw))
        vocab1 = dist.keys()
        
        freqwords = [w for w in vocab1 if len(w) > 5 and dist[w] > 150]
        
        return sorted(freqwords) # Your answer here

    answer_four()
    # ['Captain', 'Pequod', 'Queequeg', 'Starbuck', 'almost', 'before', 'himself', 'little',
    #  'seemed', 'should', 'though', 'through', 'whales', 'without']
    ```

+ Q5: Find the longest word in text1 and that word's length.
    ```python
    def answer_five():
        
        words_len = sorted([(w, len(w)) for w in set(text1)], key=lambda x: (-x[1],x[0]))
        
        return words_len[0] # Your answer here

    answer_five()
    # ("twelve-o'clock-at-night", 23)
    ```

+ Q6: What unique words have a frequency of more than 2000? What is their frequency?
    ```python
    def answer_six():
        
        dist = nltk.FreqDist(nltk.word_tokenize(moby_raw))
        vocab1 = dist.keys()
        
        freqwords = [(dist[w], w) for w in vocab1 if dist[w] > 2000 and w.isalpha()]
        
        return sorted(freqwords, reverse=True) # Your answer here

    answer_six()
    # [(13715, 'the'), (6513, 'of'), (6010, 'and'), (4545, 'a'), (4515, 'to'), (3908, 'in'),
    #  (2978, 'that'), (2459, 'his'), (2196, 'it'), (2097, 'I')]
    ```

+ Q7: What is the average number of tokens per sentence?
    ```python
    def answer_seven():
        
        return len(nltk.word_tokenize(moby_raw))/len(nltk.sent_tokenize(moby_raw)) # Your answer here

    answer_seven()
    # 25.881952902963864
    ```

+ Q8: What are the 5 most frequent parts of speech in this text? What is their frequency?
    ```python
    def answer_eight():

        words = nltk.word_tokenize(moby_raw)

        word_tags = nltk.pos_tag(words)
        tags = [tag for (word, tag) in word_tags]

        dist = nltk.FreqDist(tags)
        tag1 = dist.keys()

        freqtags = [(w, dist[w]) for w in tag1]

        return (sorted(freqtags, key=lambda x: (-x[1],x[0])))[:5] # Your answer here

    answer_eight()
    # [('NN', 32730), ('IN', 28657), ('DT', 25867), (',', 19204), ('JJ', 17620)]
    ```

+ Q9: Jaccard distance on the trigrams of the two words
    ```python
    def answer_nine(entries=['cormulent', 'incendenece', 'validrate']):

        rlt = []
        for entry in entries:
            min_jd = 100.0
            jd = 100.0
            correct = ""
    #         print("\n", set(nltk.ngrams(entry, n=3)))
            for word in correct_spellings:
                if entry[0] == word[0]:
                    jd = nltk.jaccard_distance(set(nltk.ngrams(entry, n=3)), set(nltk.ngrams(word, n=3)))
                if min_jd > jd:
                    correct = word
                    min_jd = jd
    #                 print("{} -> {}({:.4f})".format(entry, word, min_jd))

            rlt.append(correct)
        return rlt # Your answer here

    answer_nine()
    # ['corpulent', 'indecence', 'validate']
    ```

+ Q10: Jaccard distance on the 4-grams of the two words
    ```python
    def answer_nine(entries=['cormulent', 'incendenece', 'validrate']):

        rlt = []
        for entry in entries:
            min_jd = 100.0
            jd = 100.0
            correct = ""
    #         print("\n", set(nltk.ngrams(entry, n=3)))
            for word in correct_spellings:
                if entry[0] == word[0]:
                    jd = nltk.jaccard_distance(set(nltk.ngrams(entry, n=4)), set(nltk.ngrams(word, n=4)))
                if min_jd > jd:
                    correct = word
                    min_jd = jd
    #                 print("{} -> {}({:.4f})".format(entry, word, min_jd))

            rlt.append(correct)
        return rlt # Your answer here

    answer_nine()
    # ['cormus', 'incendiary', 'valid']

+ Q11: Edit distance on the two words with transpositions.
    ```python
    def answer_eleven(entries=['cormulent', 'incendenece', 'validrate']):

        rlt = []
        for entry in entries:
            min_ed = 100.0
            ed = 100.0
            correct = ""

            for word in correct_spellings:
                if entry[0] == word[0]:
                    ed = nltk.edit_distance(entry, word, transpositions=True)
                if min_ed > ed:
                    correct = word
                    min_ed = ed
    #                 print("{} -> {}({:.4f})".format(entry, word, min_ed))

            rlt.append(correct)

        return rlt # Your answer here 

    answer_eleven()
    # ['corpulent', 'intendence', 'validate']
    ```

