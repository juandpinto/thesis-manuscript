\pagenumbering{arabic}
\setcounter{page}{1}

# Introduction

This thesis provides an in-depth look at the creation of the *Frequency Dictionary of Spoken Hebrew* (FDOSH)—a list of the most common words in spoken Modern Hebrew. Its two-fold aim is (1) to explore the theory behind the creation of the FDOSH, along with implications for similar projects, and (2) to describe the methods and provide the tools to make the process as reproducible as possible.

The complete dictionary itself, consisting of 5,000 items, is included as an electronic supplement and can be downloaded free of charge.^[All supplementary materials, including the *Frequency Dictionary of Spoken Hebrew* and the scripts used to create it, are licensed as open source materials. They are available at *<https://doi.org/10.5281/zenodo.1239886>* [@PintoSupplementarymaterialscreating2018].] A partial list that includes the first 1,000 items can be found in [*Appendix A*](#appendix-a).

A review of the literature will first highlight the difficulties that exist for less commonly taught languages (LCTLs). Because the overwhelming majority of previous research on vocabulary frequency lists has focused on English (and a handful of other European languages), some important nuances are yet to be addressed. More often than not, the few non-English frequency dictionaries that do exist, along with much of the research in vocabulary acquisition, have taken at face value some of the findings of this limited-scope research—often without questioning whether the same methodologies and conclusions should be applied to different languages.

The present paper is, therefore, an effort to partially fill that gap in order to help educators interested in creating and/or using frequency dictionaries for their own classrooms, for wider dissemination, or simply for general research purposes. In doing so, it will provide an overview of some of the key decisions that must be taken into account for such a project.

The various uses of word frequency lists can be loosely classified into research applications and practical applications. Examples of research applications include traditional linguistic studies that look for common morphological patterns, corpus-linguistic studies seeking to understand language through “real world” texts, and psycholinguistic studies that explore connections between a speaker’s mental lexicon and word frequency. Practical applications of frequency lists include curriculum and textbook planning for language teachers, vocabulary selection for graded readers and dictionaries, and even independent language study.

Of course, some of the most influential studies straddle both sides of this divide and attempt to answer questions such as: How can vocabulary knowledge be appropriately tested and measured [@McLeancreationnewvocabulary2015; @NationResearchinganalyzingvocabulary2010; @NationMakingusingword2016]? What is the role of extensive reading (as opposed to intensive reading) in incidental vocabulary acquisition [@RestrepoRamosIncidentalvocabularylearning2015]? What level of vocabulary do learners need in order to read extensively for pleasure [@HirshWhatvocabularysize1992; @Schmittpercentagewordsknown2011; @NationHowlargevocabulary2006]? What level of vocabulary do learners need in order to succeed in an academic setting [@Xueuniversitywordlist1984; @Coxheadnewacademicword2000; @CoxheadReflectingCoxhead20002016]? What role does specialized vocabulary play in reaching understanding [@NationWherewouldgeneral1995]? These questions and their answers rely heavily on the creation and use of trustworthy frequency dictionaries. Yet due to the resources and effort required to create these lists, they are rarely found for less commonly taught languages.


The primary research question guiding this project is this:

> What are the most common words in spoken Modern Hebrew?

The resulting study also addresses the following secondary research questions:

> What is an effective alternative for a corpus of spoken language when one is lacking in the desired language, as is often the case for less commonly taught languages?

> How can the process of creating a frequency dictionary be simplified so that it is easy to reproduce while maintaining a high level of customizability?

> What implications might these findings have for frequency list creation and use as it pertains to other less commonly taught languages?


The literature review will serve as background for many of the important decisions that went into the creation of the FDOSH. These will be explained more in-depth in the [*methods*](#methods) chapter, where the entire process will be laid out in detail. For the sake of clarity, these key decisions are listed here at the outset. They are as follows:


Corpus size
:   The corpus from which the FDOSH was created needed to contain a minimum of 20 million tokens, though 50 million was preferred. In the end, it used a corpus of nearly 200 million tokens.\

Corpus text types
:   In order to best fit with the FDOSH's intended audience (Hebrew learners), the corpus consists of a single text type: conversation. But because of a lack of large corpora of spoken Hebrew, a corpus of film subtitles was used instead. The reasoning for and validity of such an approach will be elaborated on.\

Use
:   The primary intended audience for the FDOSH is composed of beginning-to-low-intermediate learners of Hebrew as a foreign language. It is designed for both receptive and productive language use.\

Word family levels
:   The word family level that is best suited for the FDOSH’s intended audience is the lemma, consisting of a word and all of its inflected forms, but counting derived forms as separate words.\

Criteria
:   The FDOSH was created using exclusively objective criteria, meaning that it is the product of calculations, and it was not manually tweaked in any way. The words are sorted by dispersion (specifically, Gries' *U~DP~*), and also include the measures of frequency and range.


Following the review of the literature and explanation of theory, the process of the FDOSH's creation will be explained in detail, along with some findings from the project. As already mentioned, the goal of this is to make the process easy to follow and reproduce for other languages. Finally, the FDOSH and all scripts used will be provided in the appendices.
