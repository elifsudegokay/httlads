
Most and Least Common UN words
==============================

Before we tackle most common and least common words we need to
understand a couple of things about text processing. First we are going
to want to clean up our text, and second we need to learn about stop
words. If you think about it for a minute you can probably answer the
question of the most used words already they will be words like ‘a’,
‘an’, ‘the’, ‘and’ etc. These words are pretty useless if we are trying
to extract some meaning from long texts. Our initial list of cleaening
tasks is as follows:

1. Convert all text to lower case
2. Remove all punctuation
3. Break the string into a list of words
4. Remove stop words from the list

.. code:: ipython3

    speeches_1970 = undf[undf.year == 1970].copy()


.. code:: ipython3

    speeches_1970['text'] = speeches_1970.text.apply(lambda x: x.lower())

.. code:: ipython3

    speeches_1970['text'] = speeches_1970.text.apply(lambda x: x.translate(str.maketrans(string.punctuation, ' '*len(string.punctuation))))


.. code:: ipython3

    speeches_1970['word_list'] = speeches_1970.text.apply(nltk.word_tokenize)

.. code:: ipython3

    from collections import Counter
    c = Counter(speeches_1970.word_list.sum())

.. code:: ipython3

    c.most_common(10)




.. parsed-literal::

    [('the', 25077),
     ('of', 16265),
     ('and', 9224),
     ('to', 9134),
     ('in', 6668),
     ('a', 4530),
     ('that', 3919),
     ('is', 3322),
     ('for', 2563),
     ('which', 2471)]



.. code:: ipython3

    c.most_common()[-10:]




.. parsed-literal::

    [('shabby', 1),
     ('predatory', 1),
     ('siphoned', 1),
     ('crop', 1),
     ('outflow', 1),
     ('ashes', 1),
     ('pr', 1),
     ('bystander', 1),
     ('antiimperialist', 1),
     ('earn', 1)]



::

   LookupError:
   **********************************************************************
     Resource stopwords not found.
     Please use the NLTK Downloader to obtain the resource:

     >>> import nltk
     >>> nltk.download('stopwords')

     Searched in:
       - '/Users/bradleymiller/nltk_data'
       - '/usr/share/nltk_data'
       - '/usr/local/share/nltk_data'
       - '/usr/lib/nltk_data'
       - '/usr/local/lib/nltk_data'
       - '/Users/bradleymiller/.local/share/virtualenvs/httlads--V2x4wK-/bin/../nltk_data'
       - '/Users/bradleymiller/.local/share/virtualenvs/httlads--V2x4wK-/bin/../share/nltk_data'
       - '/Users/bradleymiller/.local/share/virtualenvs/httlads--V2x4wK-/bin/../lib/nltk_data'
   **********************************************************************

.. code:: ipython3

    sw = set(stopwords.words('english'))
    len(sw)




.. parsed-literal::

    179



.. code:: ipython3

    speeches_1970['word_list'] = speeches_1970.word_list.apply(lambda x: [y for y in x if y not in sw])

.. code:: ipython3

    c = Counter(speeches_1970.word_list.sum())

.. code:: ipython3

    c.most_common(25)




.. parsed-literal::

    [('nations', 1997),
     ('united', 1996),
     ('international', 1251),
     ('world', 1101),
     ('peace', 1019),
     ('countries', 908),
     ('states', 897),
     ('organization', 763),
     ('would', 677),
     ('people', 649),
     ('development', 649),
     ('security', 594),
     ('general', 571),
     ('peoples', 567),
     ('assembly', 552),
     ('charter', 551),
     ('government', 544),
     ('one', 535),
     ('must', 474),
     ('also', 454),
     ('economic', 450),
     ('us', 401),
     ('years', 392),
     ('time', 371),
     ('great', 369)]



.. code:: ipython3

    c.most_common()[-25:]




.. parsed-literal::

    [('reliably', 1),
     ('polish', 1),
     ('sqon', 1),
     ('ultra', 1),
     ('nonapplicability', 1),
     ('statutory', 1),
     ('2391', 1),
     ('renovation', 1),
     ('russia', 1),
     ('gbout', 1),
     ('•', 1),
     ('prediction', 1),
     ('oceania', 1),
     ('fat', 1),
     ('1848th', 1),
     ('shabby', 1),
     ('predatory', 1),
     ('siphoned', 1),
     ('crop', 1),
     ('outflow', 1),
     ('ashes', 1),
     ('pr', 1),
     ('bystander', 1),
     ('antiimperialist', 1),
     ('earn', 1)]



Practice
~~~~~~~~

Redo the analysis of the most common and least common words for 2015

Normalize the data so that you are looking at percentages not raw
counts.

Build a graph to compare 1970 and 2015

Look at the documentation for the wordcloud package. Make a word cloud
for both 1970 and 2015



