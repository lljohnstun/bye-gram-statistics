bye-gram-statistics
===================

Parse and tag abstracts, index 3 training models using Lucene and Shingle, and query to define collocations.
A repostitory for Java based solutions to a Lab assignment in BMI NLP for Biomedical Text.

•	Dr. Graciela Gonzalez PhD, Arizona State University, Biomedical Informatics 

Find and analyze bigrams in a pubmed corpus
•	Find possible collocations, using at least two statistical tests
•	Build an n-gram model
•	Exercise Lucene deployment


Corpus:  CALBC-SSC-III-Small (http://www.ebi.ac.uk/Rebholz-srv/CALBC/corpora/resources/small/175k-allcomer-xtype.gz) 

1.	Write an XML parser to extract the text from the abstracts contained in the corpus, split the sentences, and tag sentences for parts of speech. The parser should also be able to represent the tagged named entities from the corpus as tag, as opposed to the name. That is, instead of using a multi-token gene name for a gene entity, represent it with a tag such as GENE_ENTITY. Your parser should be able to do this for all tagged named entities in the corpus.
Replace with some other label. So POS tagger does not get confused with the multiword names of genes.

Parser
	Extract
	Split sentences
	Tag Sentences – POS
	Represent multi-token entities with a single tag

Exception error if no abstract

2.	Divide the corpus into a training set and a testing set. What percent of corpus is for training? How will you split your training and test set? What factors of the corpus are you considering when splitting? Defend your decisions. 

Decide & defend how to divide the corpus

3.	Build a Lucene index with the training set with each document being a 1-, 2-, or 3-gram. Index all three. These counts will be used to look at bigrams and collocations and be used to create a tri-gram model. It up to you for how you want to handle stop-words and stemming.  For this question, explain the choices you made in creating your model, and why you made such choices.
Porter stemmer
Stop words data analyzer
Shingle analyzer for Lucene
Use Lucene 2.4 jar file in Lucene archive for past versions

Build Lucene Index
	Tokens indexed as  1, 2 or 3 gram 
	Use uniqueId document field – text, n[1,2,3], part of speech, count
	Use Update document method of index writer

Example document fields: uniqueId, text, n [1, 2, 3], part of speech string, count. 

Note: There will be a large amount of 3-grams, so for memory purposes you may have to build the Lucene index as you process the training text. This will involve using the update document method of the index writer, with a term based on the UniqueId. 

4.	Query your Lucene index for the 100 most common bigrams, using the POS field to filter for parts-of-speech patters. For these 100 most common bigrams, calculate the t-score (as described in section 5.3.1). 
Ask Azadeh
a.	Provide your POS filters and defend your choice of the filters
b.	Provide a list of the top 20 bigrams, ranked by t-score
c.	Rank the top 5 bigrams by difference between count and t-score. Provide an explanation for the discrepancies between count and t-score in these examples.

Query Index for bigrams
Calculate  the t-score

5.	Use your GENE_ENTITY tag and one other named entity tag of your choice, create a set containing all the bigrams for each tag. For both sets, perform the Dunning’s Likelihood ratio test for every bigram witthing the set. Create a table to list the top 20 bigrams, ranked by the Dunning’s likelihood test, for each set. Are any of the bigrams in the tables a collocation? Defend your answer.

Create a set of  bigrams with GENE_Enitity and other tag of choice
	Dunning’s likelihood Ratio Test for every bigram in set
	Create a table
	Support the identification of collocations
		Counts, patterns

6.	With the 1-, 2-, and 3-gram counts from your training set, build three different models: Model A: Simple model with no smoothing, and just use the training frequency counts; Model B: Smooth using Lidstone’s law; and Model C: Smooth using Good-Turing estimation and either linear interpolation or back-off. Describe the choices you made for each model and explain why you made the choices you made (especially when choosing parameters).
 Build three different models
	Model A – no smoothing
	Model B – smooth with Lidstone’s law
	Model C – Good- Turning and either linear or back-off smoothing
Lucene has some smoothing

7.	Choose 3 sentences, a short, medium length and long sentence, at random from your test set. Find the probability for each sentence with each of your models. What does the probability tell you about each model and each sentence?

Find the probability of a short, medium and a long sentence using each model.
What is the significance of the probability for each sentence using each model


8.	For each model, find the cross-entropy and perplexity for the test set. Present and explain your results. Discus what the cross-entropy and perplexity scores mean for each model, and what conclusions you can draw about each model based on the scores.

For each model – find the cross entropy and perplexity for the test set.
Explain the results
Explain the significance of the results in each case.
What does it tell you about each model?
