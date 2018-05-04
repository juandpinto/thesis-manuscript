\newpage

# Conclusion

This thesis has served as an in-depth look at the creation of the *Frequency Dictionary of Spoken Hebrew* (FDOSH). It has explained both the theory and the process, and in so doing has provided tools to facilitate the creation of similar frequency lists.

By identifying the decisions and outcomes of past studies, the literature review set the background for the most important factors to consider when undertaking such a project. These include corpus size and text type(s), the purpose of the frequency dictionary, the word family level to use, and the criteria by which to rank the list.

The methods chapter described—in detail—the process used to create the FDOSH. It explained how the corpus was found and cleaned, how the necessary data was extracted from it, how various measures were calculated, and how the frequency list was then sorted and exported into a full frequency dictionary. The relevant code was also explained, as well as instructions on specific changes that can be made depending on the needs of other researchers.

The organization and uses of the FDOSH were described in the last chapter. Most importantly, some of the challenges encountered during the process were discussed, along with possible directions for future projects. Some of the weaknesses of the FDOSH were also described.

Finally, the appendices to this thesis include a limited list of the FDOSH, along with all of the scripts used in their entirety. The code and full dictionary can be accessed as part of this thesis's supplementary materials at *<https://doi.org/10.5281/zenodo.1239886>* [@PintoSupplementarymaterialscreating2018], or at the project's GitHub repository: *<https://github.com/juandpinto/frequency-dictionary>*.

The primary research question asked at the outset of this thesis was the following:

> What are the most common words in spoken Modern Hebrew?

Despite some deficiencies in the *Frequency Dictionary of Spoken Hebrew*, this question has been tentatively answered by the ranking of its words. *Most common words* in this case has been operationalized to mean most highly ranked lemmas by the usage coefficient of Gries's deviation of proportions, or *U~DP~* [@GriesDispersionsadjustedfrequencies2008; @GriesDispersionsadjustedfrequencies2010]. Of course, there can be no absolute, definitive answer to such a question, but the FDOSH provides one possibility.

The secondary research questions have been answered thus:

> What is an effective alternative for a corpus of spoken language when one is lacking in the desired language, as is often the case for less commonly taught languages?

A corpus of film and television subtitles offers an effective alternative. Though more study is needed in this area, the preliminary studies are in agreement on this point [@BrysbaertMovingKuceraFrancis2009; @Newusefilmsubtitles2007]. Importantly, this thesis has shown how obtaining and using such a corpus can be done easily despite the lack of resources that often plagues research for less commonly taught languages.

> How can the process of creating a frequency dictionary be simplified so that it is easy to reproduce while maintaining a high level of customizability?

This project aimed at making the entire dictionary-creation process as reproducible as possible while allowing for flexibility and transparency in the tools used. By using well-documented open-source scripts written in an easily readable programming language (Python) the result succeeds in this regard. The scripts themselves are a product of this project as much as the frequency dictionary is.

> What implications might these findings have for frequency list creation and use as it pertains to other less commonly taught languages?

The findings of this thesis are applicable to the task of frequency list creation for all languages. They are especially useful, however, to languages that lack the resources to compile and use corpora of spoken language. By tackling this problem, I hope that the current project serves as a catalyst for future research that may build upon the ideas discussed here. The development and open dissemination of tools such as these can only lead to greater cooperation among educators and researchers, to the benefit of all involved.
