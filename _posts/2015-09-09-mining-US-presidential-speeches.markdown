---
layout: post
title:  "Mining US Presidential Speeches"
date:   2015-09-09 00:40:54
---

Candidates seeking nomination for the President of the United States declare their intentions at a Presidential Announcement Speech. These speeches contain a large amount of information and I wondered what a quick text analysis would spit out.

## Working with n-grams ##

n-grams are contiguous sequences of n items from a piece of text. They are particularly useful in searching and also in providing understanding of textual data. I was first introduced to n-grams when I worked on full-text searching on [PianoShelf](http://pianoshelf.com/sheetmusic) (a project I worked on with [Ankit Sardesai](http://ankitsardesai.ca) and [Winston Wu](http://github.com/winxton)). We use ElasticSearch as the search engine and n-gram filters to analyse and index  the data. This means we support queries like 'beeth exp' which would search for expert music by Beethoven. In it's simplest form, ElasticSearch would build substrings (3-grams, 4-grams...) and index these substrings to make it searchable.

I decided to start off by generating uni-grams over the speeches. I decided to use [NLTK](http://nltk.org/) since I've heard lots of good things about it.

# Unigram Analysis #

I grabbed transcripts of the announcement speeches of Barack Obama in 2007, Mitt Romney in 2012, Hillary Clinton in 2015 and Donald Trump in 2015. I ran a regular expression tokenizer to get all the words in the speech. Here are the top 30 uni-grams generated for Mitt Romney's speech.

![RomneyUnigramsNoStopWords]({{ site.url }}/images/romney_unigrams_no_stopwords.png)

This is useless. All the common words in the English language turned up. Luckily, NLTK has a stop-word list so I can happily ignore them. Also, I ran a lemmatizer to stem the words to their parent/root. For example, 'I see a future with jobs, robots and flying cats' would be tokenized to ['I', 'see', 'a', 'future', 'with', 'jobs', 'robots', 'and', 'flying', 'cats']. It would then be lemmatized to ['I', 'see', 'a', 'future', 'with', 'job', 'robot', 'and', 'fly', 'cat']. Stemming the words is particularly useful in search because you would expect articles related to 'fishing' come up when you search for 'fish' on Google. In this case, we are interested in seeing the words the candidates speak the most and having both 'job' and 'jobs' show up in the analysis isn't really helpful. Here's a refined version of Romney's speech.

![RomneyUnigramsStopWords]({{ site.url }}/images/romney_unigrams_stopwords.png)

This makes more sense. It is no surprise that some of the top words in there are economy, tax, and work. However, it's strange that he mentions 'Obama' a fair number of times in his speech. I also find it weird that 'year' is repeated so often. Maybe a bi-gram analysis will provide more information.

For comparison, I've posted Obama's and Clinton's speech analysis below.

![ObamaUnigramsStopWords]({{ site.url }}/images/obama_unigrams_stopwords.png)

Obama doesn't seem to mention 'economy', 'tax', 'work' at all. He focuses on words like 'generation', 'people', 'health', 'school' and 'together'. It seems like his speech is more about the people versus Romney's speech being focused on more national aspects like 'economy', 'tax', 'nation', 'world'. Interesting.

![ClintonUnigramsStopWords]({{ site.url }}/images/clinton_unigrams_stopwords.png)

If you notice the scale, you will notice that the words are repeated way more often compared to the previous graphs. Again, a bi-gram analysis would be really helpful here. It seems like Clinton's speech is similar to that of Obama's.

Here's Donald Trump's 2015 Presidential Announcement Speech.

![TrumpUnigramsStopWords]({{ site.url }}/images/trump_unigrams_stopwords.png)

What? There's no mention of America, tax, work, school, health or economy anywhere. I see 'China' as one of the top words. I should probably do a bi-gram analysis.

# Bigram Analysis #

NLTK makes it really easy to generate bigrams and the frequency score using [collocations](http://www.nltk.org/howto/collocations.html).

![RomneybigramsStopWords]({{ site.url }}/images/romney_bigrams_stopwords.png)

Romney's speech seems to mention Obama pretty frequently. I was curious to why 'three year' was on top of the list. I searched through his speech to find this.

*"Barack Obama has failed America.*

*When he took office, the economy was in recession. He made it worse. And he made it last longer.*

*Three years later, over 16 million Americans are out of work or have just quit looking. Millions more are underemployed.*

*Three years later, unemployment is still above 8%, a figure he said his stimulus would keep from happening.*

*Three years later, foreclosures are still at record levels.*

*Three years later the prices of homes continue to fall.*

*Three years later, our national debt has grown nearly as large as our entire economy."*

That's not that helpful. Maybe there exists a way to ignore figures of speech using NLTK, just haven't figured it out yet.

![ObamabigramsStopWords]({{ site.url }}/images/obama_bigrams_stopwords.png)

![ClintonbigramsStopWords]({{ site.url }}/images/clinton_bigrams_stopwords.png)

These graphs make more sense. I would have expected to see something like this.

![TrumpUnigramsStopWords]({{ site.url }}/images/trump_bigrams_stopwords.png)

This still seems to be an outlier amongst the other speeches. I'm not sure what to make of it.

## Insight ##

In my opinion, this was an interesting experiment. It gives a rough idea of what candidates are actually focusing on. I'm sure people who write these speeches go through a similar sort of analysis before they give it to their candidates.

I was thinking if we could run these analysis tools against lecture transcripts at university, it could possibly tell us what they key concepts to focus on would be. That would be awesome.

Shoot me an email if you have any additional thoughts!


