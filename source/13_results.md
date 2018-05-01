\newpage

# The FDOSH: A vocabulary list of conversational Modern Hebrew

The *Frequency Dictionary of Spoken Hebrew* in its entirety can be found as an electronic supplement to this thesis (in CSV format) or at the following GitHub repository: *<https://github.com/juandpinto/opus-frequencies>*. It contains the most common 5,000 lemmas of conversation Modern Hebrew, as found in the *OpenSubtitles2018* corpus. A sample of the first 1,000 lemmas is included in [*Appendix A*](#appendix-a).

For discussion purposes, a small sample of the first 30 entries is here presented.

|    LEMMA | RANK | DISPERSION |  FREQUENCY |  RANGE |
|---------:|-----:|-----------:|-----------:|-------:|
|      הוא |    1 | 114,718.51 | 121,008.92 |  99.99 |
|        ה |    2 |  47,244.93 |  50,841.12 | 100.00 |
|       את |    3 |  32,811.28 |  35,337.28 |  99.92 |
|        ל |    4 |  27,415.19 |  29,102.77 |  99.97 |
|       לא |    5 |  24,888.86 |  27,213.76 |  99.94 |
|       זה |    6 |  23,817.89 |  26,418.69 |  99.96 |
|        ב |    7 |  23,081.75 |  24,839.48 |  99.98 |
|       של |    8 |  18,214.68 |  20,088.89 |  99.97 |
|        ש |    9 |  18,203.83 |  20,028.64 |  99.95 |
|      היה |   10 |  11,861.33 |  13,312.52 |  99.91 |
|       מה |   11 |  10,879.07 |  12,192.80 |  99.87 |
|        ו |   12 |   8,711.82 |   9,840.85 |  99.93 |
|       על |   13 |   8,246.82 |   9,119.70 |  99.93 |
|      כול |   14 |   6,062.08 |   6,842.01 |  99.90 |
|      ידע |   15 |   5,328.40 |   6,205.85 |  99.69 |
|       כן |   16 |   5,011.86 |   6,232.26 |  99.46 |
|        מ |   17 |   4,871.00 |   5,479.15 |  99.89 |
|       יש |   18 |   4,840.57 |   5,519.12 |  99.81 |
|      עשה |   19 |   4,180.99 |   4,941.68 |  99.66 |
|      אבל |   20 |   4,052.79 |   4,757.33 |  98.86 |
|      טוב |   21 |   3,954.48 |   4,891.35 |  99.61 |
|      רצה |   22 |   3,949.30 |   4,671.67 |  99.41 |
|       אם |   23 |   3,846.61 |   4,444.59 |  99.68 |
|       עם |   24 |   3,756.06 |   4,333.17 |  99.71 |
|      אמר |   25 |   3,515.24 |   4,128.07 |  99.39 |
|       אז |   26 |   3,370.31 |   4,052.24 |  99.41 |
|      סדר |   27 |   3,197.62 |   4,305.52 |  98.33 |
|     צריך |   28 |   2,862.13 |   3,501.64 |  99.18 |
|       רק |   29 |   2,543.93 |   2,996.30 |  99.65 |
|      חשב |   30 |   2,511.54 |   3,021.85 |  99.09 |

Table: Sample of the first 30 entries on the FDOSH.\label{FDOSH_sample}


Besides each lemma and its respective rank on the list, the FDOSH includes three pieces of information: frequency, range, and dispersion. Frequency, in this case, is not raw frequency—the total number of times the lemma appears in the corpus—but rather how many times the lemma appears for every million tokens in the corpus. Using this normalized frequency measure makes the number more meaningful since it aims to reflect the per-million count of all spoken Hebrew, not just the OpenSubtitles2018 corpus. It also makes it easier to compare frequencies with those found in other corpora.

The range has also been normalized. It describes the *percentage* of the number of sub-corpora—or, in this case, movies—that the lemma appears in, in proportion to the number of movies in the entire corpus.

The most important piece of information the list provides, however, is dispersion, which acts as the ranking measure for the FDOSH and is discussed more in-depth in the [*dispersion*](##methods-dispersion) section of the previous chapter.

The percentage of the corpus that is covered by the first *n* entries on the list is referred to as coverage. This is a simple matter of finding the total number of tokens in the corpus, and dividing from it the sum of all the *raw* frequencies from the first *n* entries.

For example, the sum of the frequencies of the first 20 lemmas in *Table \ref{FDOSH_sample}* (84,656,819) divided by the total size of the corpus (193,755,220) is 0.436926649. In theory, this means that by knowing just the first 20 lemmas on the FDOSH one would be able to understand 43.7% of the words in the entire OpenSubtitles2018 corpus! That is a clear example of the power of Zipf's Law (see the [*introduction*](#introduction) for more on Zipf's Law).

Table \ref{coverages} presents a listing of some important coverages provided by different amounts of lemmas on the FDOSH.

<!-- need to double-check these coverage figures now that I've changed the list using UDP ranking -->

*n* Lemmas | Frequency Sum | ÷ Corpus Size | = Coverage
----------:|:-------------:|:-------------:|:---------:
       374 |  135,767,644  |  193,755,220  |    70%
       939 |  155,016,588  |  193,755,220  |    80%
     4,246 |  174,380,519  |  193,755,220  |    90%
    13,758 |  184,067,666  |  193,755,220  |    95%

Table: Breakdown of coverage percentages.\label{coverages}


The entire FDOSH consists of 5,000 lemmas. This number was chosen in order for it to include the required items for 90% coverage, while also making it an even factor of 1,000. In its entirety, the FDOSH covers 90.8% of the corpus from which it is created.

<!-- Other observations:
- Count words with changed rank due to dispersion (as opposed to freq alone). Use table?

Nation (2016), p. 103:
> Carroll, Davies and Richman (1971) found in their study that frequency and their measure of dispersion correlated at .8538 (page xxix), showing that the more widely used a word is, the more likely it is to be frequent. Some words however are frequent in just one or two texts or sub-corpora and may not even occur in others. The use of a range or dispersion figure or both can indicate such words.

-->


## Use

The purpose of the *Frequency Dictionary of Spoken Hebrew* is to provide a list of the most commonly-used lemmas in conversational Modern Hebrew. As described in this thesis's [*introduction*](#introduction), frequency dictionaries can serve a number of purposes, generally classified as either research applications or practical applications. Though primarily designed with the goal of aiding vocabulary acquisition, the FDOSH can similarly fill a multitude of roles.

This project originally began with a desire to evaluate whether the findings of some influential studies regarding English vocabulary would hold true for Hebrew vocabulary. Specifically, I was interested in measuring the amount of vocabulary necessary for learners of Hebrew to comfortably read extensively for pleasure, following the lead of previous studies by Schmitt et al. [-@Schmittpercentagewordsknown2011], Nation [-@NationHowlargevocabulary2006], and Hirsch and Nation [-@HirshWhatvocabularysize1992], among others. I quickly realized that the frequency dictionary necessary for such a project did not exist for Hebrew, so I chose to focus on designing such a dictionary first.

With the FDOSH now created, my hope is that it will serve as a basis for future studies of this type. As Gries [-@GriesDispersionsadjustedfrequencies2010] explains:

> In some theoretical approaches, such as cognitive linguistics or usage-based grammar, frequency data are now regularly used in the domains of first- and second/foreign-language acquisition, the study of language and culture, grammaticalization, phonological reduction, morphological processing, syntactic alternations, etc. (p. 197)

The possible research applications of such a dictionary are the reason I chose to include so much data with each entry.

I also hope that educators will find use in the lemmas and their rankings, either for identifying the vocabulary to include in their textbooks, to teach in their classrooms, or to focus on in their conversation groups. The FDOSH can similarly serve independent learners, or students of Hebrew who wish to take greater control of the vocabulary they deliberately study.

Even more than all of this, however, the FDOSH can serve as an example for future frequency dictionaries. I have chosen to place heavy emphasis on the creation process itself in order to make it easily reproducible for comparable projects in other languages. In so doing, my hope is that similar educational resources and research tools will become widely available.


## Challenges and future direction

Throughout the course of this project, I have encountered several issues that are worth discussing. Some of these are questions that require further study in order to address adequately. Others are technical issues related to the complex task of pre-processing and parsing the corpus—something not directly dealt with in this thesis. Others yet are suggestions that I simply did not have time to implement given this project's time constraints. And finally, there are limitations that are the inevitable result of the tools at hand.

I have divided all of these issues into two categories: methodological challenges of a bigger nature, and functional challenges of a more limited scope.


### Methodological challenges

One of the more obvious issues of this project is the use of a corpus of movie subtitles as a substitute for a corpus of true conversational language. This issue in a way forms the backbone of the FDOSH, and it is at the heart of what this project is all about. Though I discuss several points related to this in the *Background* section of this thesis, I will here discuss some of its implications for future work.


#### Ideal vs. practical corpora

The use of a subtitle corpus has both positive and negative aspects. As described in the literature review, the early research that has been done on the topic indicates that movie subtitles share many features with spontaneous, spoken language [@Newusefilmsubtitles2007; @BrysbaertMovingKuceraFrancis2009]. This includes a high level of correlation between the two, as well as a strong ability to predict the outcomes of a lexical decision task.

One especially positive aspect of subtitle corpora is their accessibility. Thanks to the efforts of organizations such as *<http://opensubtitles.com>* and [OPUS](http://opus.nlpl.eu), very large corpora are available to the public for free. And they already come pre-processed, as an additional incentive for the time-constrained researcher.

This free and open nature makes subtitle corpora excellent tools for research in languages that don't yet have large, high-quality corpora of spoken language. Though advances in technology are rapidly making this type of data-collection more accessible, the costs remain too high for many less-commonly taught languages as of now. This is largely due to the arduous process of transcribing audio recordings.[@IzreelTranscribingSpokenIsraeli2004]

An ideal corpus for this sort of task would consist of many millions of tokens of recorded, transcribed, and parsed spontaneous spoken language. Several attempts have been made to create a corpus of this nature in Hebrew.

The most prominent of these is the [*Corpus of Spoken Israeli Hebrew* (CoSIH)](http://cosih.com/), created at Tel Aviv University between 2000 and 2002 [@IzreelDesigningCoSIHCorpus2001]. Designed and initiated by a team of distinguished scholars, it unfortunately ran out of funding long before its goals were met. The CoSIH website (*<http://cosih.com/>*) makes available to the public a total of 13.5 hours of recorded Hebrew, with just over five hours of it having been transcribed.

Though a few publications have used data from CoSIH, these have been primarily methodological studies for the design of the project itself [@AmirCharacteristicsIntonationUnit2004; @IzreelIntonationUnitsStructure2005; @MettouchiOnlyProsodyPerception2007]. At least one dissertation, by Nurit Dekel, uses data exclusively from CoSIH. Her entire corpus consists of 44,000 tokens [@Dekelmattertimetense2010, p.7].

Other corpora of spoken Hebrew include the Haifa Corpus of Spoken Hebrew [@YaelHaifaCorpusSpoken2014] and the Hebrew CHILDES corpus [@AlbertHebrewCHILDEScorpus2013; @GretzParsingHebrewCHILDES2015]. The first consists of 17.5 hours of audio recordings, along with a limited selection of transcribed text. The latter is a collection of recordings of interactions between adults and children, comprising a total of 417,938 transcribed tokens. The CHILDES corpus is unique in that the transcriptions are provided using a Latin-based phonemic transliteration. This was done in order to avoid many of the textual ambiguities of using the Hebrew script, which are addressed below under [*functional challenges*](#functional-challenges).

Though ideal in some ways, these corpora remain far too small to be effectively used for the creation of frequency lists. Even combined into a single corpus (which would introduce a series of new issues to solve), the total size would not be bigger than two million tokens. As discussed earlier in this thesis, Sorell [-@Sorellstudyissuestechniques2013] provides evidence to suggest that a corpus of 20–50 million tokens is the minimum for a stable word list.

Are movie and television subtitles a suitable substitute for spontaneous, spoken language? Early studies suggest it is at least adequate, but much more research is needed to answer this question definitively. For now, it remains as a practical and appealing option.


#### Using original-language movies exclusively

One of the potential downsides of using the OpenSubtitles2018 corpus is that it includes all subtitles of a specific language, even *translated* subtitles from movies filmed in other languages. The question is, does a translated script represent true conversational language as faithfully as an original script?

This is a question that requires more research in order to answer satisfactorily. Though translated subtitles don't need to try to approximate the utterance length and visual cues that a dubbed script does, their quality still largely depends on the skills of a translator. Most importantly, a translation may not accurately reflect the register of the original, no longer serving as a representation of conversational language. Again, these are important points to consider.

One solution is to simply use movies that were originally filmed in the target language of the corpus. Another possibility is to calculate frequency measures for original and translated subtitles separately, then average them. This latter approach was used by New et al. [-@Newusefilmsubtitles2007]. In either case, the first step is to extract the subtitle files that represent the original language of the movie, in this case Hebrew. In theory, each XML file in a monolingual *OpenSubtitles2018* file should contain a tag that identifies the original language of the movie [@LisonOpenSubtitles2016Extractinglarge2016]. In practice, I found that the overwhelming majority of the files contained an empty `<lang>` tag instead. Luckily, there is a way to obtain the desired metadata for each movie in the corpus.

This can be done with a script that uses an application programming interface (API) to fetch specific information from an online movie database. The name of each movie folder in the corpus, which is simply a series of numbers, corresponds to that movie's IMDb identifier, which is a unique ID registered with the [Internet Movie Database](http://www.imdb.com/). This makes the process relatively easy, as we simply need to query the database using this ID to receive all of the movie's metadata.

Though IMDb does provide their own API, I decided instead to use an API created for the [Open Movie Database (OMDb)](http://www.omdbapi.com/). This API can be used free-of-charge, but it has a 1,000 movie limit per day. Since the OpenSubtitles2018 Hebrew corpus contains nearly 50,000 movies, I decided instead to pay for a daily limit of 100,000 movies. This only requires a $1.00 donation for each month that one is registered to use the OMDb API.

Once an API key is obtained, a script can be written to obtain the information desired for every movie all at once. In this case, we want to know the original language(s) for each movie.

This script in its entirety is found in [Appendix B.2](#appendix-b.2). It uses an imported Python wrapper for the API, written by [Derrick Gilland](https://github.com/dgilland), which can be found at <https://github.com/dgilland/omdb.py>. This package can be installed through PIP by entering `pip install omdb` into the command line.

For practical purposes, the script requires one to enter a specific year (or, more accurately, corpus folder name). If desired, an asterisk can act as a wildcard: `python OMDb-fetch.py 1988` will fetch data for movies from 1988, while `python OMDb-fetch.py 198*` will do it for all movies in the 1980s. In order to fetch data for all movies in the database at once, use `python OMDb-fetch.py *`. I don't recommend this, however, since it may overload the server and cause the script to time out.

I also found that, unfortunately, OMDb does not contain every movie in its database. However, these mystery movies were few.

The script begins by creating a list of all movie directory paths for the desired year.

``` {#OMDb-fetch .python .numberLines startFrom="15"}
for name in glob.glob(
        './OpenSubtitles2018_parsed_single/parsed/he/' +
        year + '/*/'):
    IDs.append(name)
```

Each item in the list is then trimmed to include only the name of the movie folder, which is *almost* equivalent to the IMDb ID.

``` {#OMDb-fetch .python .numberLines startFrom="21"}
IDs = [os.path.basename(os.path.dirname(str(i))) for i in IDs]
```

In order to make the IDs match those in the database, additional zeros must be added to the beginning until they are seven digits long.

``` {#OMDb-fetch .python .numberLines startFrom="24"}
for i in IDs:
    while len(i) < 7:
        IDs[IDs.index(i)] = '0' + i
        i = '0' + i
```

The list is then sorted numerically in order to more easily interpret the results: `IDs.sort()`{.python}.

The API key is set in line 32, but be sure to replace `906517b3` with your own key, which can be obtained at <http://www.omdbapi.com/>.

``` {#OMDb-fetch .python .numberLines startFrom="33"}
omdb.set_default('apikey', '906517b3')
```

The script then prints a table header, fetches the title, year, and language(s) for each movie, and prints the results directly into the computer terminal.

``` {#OMDb-fetch .python .numberLines startFrom="36"}
print('# ' + year + '\n' +
      'IMDb ID\tTitle\tYear\tLanguage(s)')
```

``` {#OMDb-fetch .python .numberLines startFrom="40"}
for i in IDs:
    doc = omdb.imdbid('tt' + i)
    print('tt' + i + '\t' +
          doc['title'] + '\t' +
          doc['year'] + '\t' +
          doc['language'])
```

Using a simple search program that allows for extraction of specific lines, such as those labeled with the language `Hebrew`, one can make a list of all the subtitle files that represent the original primary language of the movie. I used the open-source coding program [*Atom*](https://atom.io) to do this, though many options exist.

I modified the main script to use only movies from this list. The instructions for how to do this are included in the comments within the main script itself, which can be found in [*Appendix B.1](#appendix-b.1).

In the end, however, I found that the total token count for this entire mini-corpus of original Hebrew subtitles was only 615 thousand. This was well below my minimum goal of a 20-million-token corpus. In comparison, the entire Hebrew *OpenSubtitles2018* corpus that I used (with translated and original language subtitles) contains over 194 million tokens. I have explained how to use the scripts for this purpose so that they can be used for languages that have sufficient original subtitles. The *Frequency Dictionary of Spoken Hebrew*, however, is created using the entire corpus. As I mention in the [*conversation text type*](#conversation-text-type) section of the literature review, the findings of a study by New et al. [-@Newusefilmsubtitles2007] suggest that translated subtitles may be a valid alternative, but more research is needed in this area.


### Functional challenges

A quick scan of the FDOSH reveals some notable entries. Some of these are mere quirks of the automatic parser, while others are the result of ambiguities.

For example, the very first lemma on the list is a bit unexpected. "הוא" is certainly not the most common lemma in Modern Hebrew. A quick look at some of the files in the corpus, however, reveals that all pronouns are grouped under this lemma. That is, אתה (you), היא (she), and אנחנו (we), just to name a few, are parsed as belonging to the lemma "הוא." Considering how common pronouns are in the majority of the spoken dialogue of many languages (especially the first and second person pronouns), its place at the top of the list ceases to be a surprise.<!-- source -->

Another thing to note is that verbs are all listed in their traditional third-masculine-singular past conjugation. The first verb on the list is "היה"—a lemma referring to all forms of the verb להיות, including the infinitive. The same is true of "ידע" (entry 19) and "דיבר" (entry 60).

Many of the most common lemmas on the FDOSH are prepositions. Note that even the definite article (-ה) and inseparable prepositions, such as -ל and -ב are considered independent lemmas by the parser, and are listed respectively as the lemmas "ל" ,"ה" and "ב".

Other issues, however, are more difficult to explain.


#### Textual ambiguity of Hebrew orthography

The flexible spelling conventions of Hebrew are at the root of many of the problems with the FDOSH. For example, דִּבֵּר *he spoke* can be written as either דיבר ("full spelling") or דבר ("defective spelling"). There is also a noun, דָּבָר *thing*, that looks identical to the verb's defective spelling (דבר). Though the difference is usually clear from context, the automatic parser has some difficulty with this orthographic ambiguity.

The lemma "דבר" (entry 27) includes instances of both the verb and the noun, which are completely unrelated. A simple search through the corpus reveals multiple examples of the noun דבר tagged with `lemma="דבר"`:

```{.xml}
<w xpos="NOUN" head="579.3" feats="Gender=Masc|Number=Sing" upos="NOUN" lemma="דבר" id="579.2" deprel="nsubj">דבר</w>

<w xpos="NOUN" head="200.11" feats="Gender=Masc|Number=Plur" upos="NOUN" lemma="דבר" id="200.12" deprel="obj">דברים</w>
```

We also find plenty of examples of the verb with the same lemma tag:

```{.xml}
<w xpos="VERB" head="0" feats="Gender=Fem|HebSource=ConvUncertainHead|Number=Sing| Person=3|Tense=Past" upos="VERB" lemma="דבר" id="2346.4" deprel="root">דברה</w>

<w xpos="VERB" head="0" feats="Gender=Fem,Masc|Number=Plur|Person=1|Tense=Past" upos="VERB" lemma="דבר" id="1270.2" deprel="root">דברנו</w>

<w xpos="VERB" head="0" feats="Gender=Fem,Masc|Number=Plur|Person=3|Tense=Past" upos="VERB" lemma="דבר" id="368.4" deprel="root">דברו</w>
```

A different lemma, "דיבר" (entry 61), is the expected lemma for the verb since it follows the standard third masculine plural conjugation. Interestingly, however, the parser applies this lemma only to attestations of the word with an inserted *yod*, or with a *mem* or *lamed* prefix (present tense or infinitive). All other instances are parsed as the lemma "דבר." Though unexpected and simply wrong, at least this issue is consistent.

```{.xml}
<w xpos="VERB" head="840.4" feats="Gender=Fem,Masc|HebBinyan=HITPAEL|Number=Plur|Person=1| Tense=Past" upos="VERB" lemma="דיבר" id="840.16" deprel="conj">דיברנו</w>

<w xpos="VERB" head="1451.12" feats="Gender=Masc|HebBinyan=PIEL|Number=Sing|Person=1,2,3| VerbForm=Part|Voice=Act" upos="VERB" lemma="דיבר" id="1451.20" deprel="obl">מדבר</w>
```

To complicate matters more, we also find the unexpected lemmas "דיברה" (entry 1184), "שדיבר" (entry 2588), and "שדיברה" (entry 4106). Based on their context<!--sentence example(s)-->, these should clearly be parsed as two separate lemmas, "ש" and "דיבר."

These are just a few among many examples of the difficulties encountered by the automatic parser. Though the parsing was carried out by the OPUS team as part of the corpus's pre-processing stage, it is valuable to at least have an idea of how it works its magic. I will here explain the basics of the process and some of the implications entailed.


<!--
Many more examples of specific issues can be included in this section. Examples:

The lack of vowels makes it so that the clearly different words עִם and עַם are combined into the single lemma "עם."

מ and מן are listed separately.
-->


#### Automatic parsing

Automatic parsing refers to the process of having a computer program create a syntactic tree for a corpus of natural language. Natural language, as opposed to artificial or constructed language, is notoriously complex in its structure. Natural language processing (NLP) is an entire field of research, currently at the forefront of computer science. Parsing can serve many purposes, from theoretical linguistic research to machine translation or even the creation of artificial intelligence assistants such as Siri or Alexa. For our purposes, a parsed text is important in order to use lemmas as the word family level for the FDOSH. This decision is discussed under [*identifying words (word family levels)*](#identifying-words) in this thesis.

Two distinct types of syntactic parsers exist, constituency parsers and dependency parsers. These are based on the two respective linguistic theories of syntax, constituent grammar (sometimes referred to as phrase structure grammar) and dependency grammar.

Constituent grammar is the classic syntax tree structure taught in introductory-level linguistics classes. It is essentially a theory of the logic structure of language as a whole. Dependency grammar is a competing theory that treats words as more directly interconnected to each other. A thorough description of these ideas is outside the scope of this thesis and is not pertinent to the project. What is important to know is that dependency grammar, and thus dependency parsers, have played an important role in the advancement of NLP and computational linguistics as a whole. The term "automatic parser", therefore, most often refers to an automatic *dependency* parser.<!-- source(s)? -->

Some parsers proceed in a two-step process of morphological tagging (part of speech) and then dependency parsing (syntactic role and conjugations). In all cases, tokenization must first take place, which refers to splitting the text into individual lemmas.

Most automatic parsers are "trained" using a small corpus that has been manually parsed by a human previously, or at least one that was automatically parsed and then checked and corrected by the researcher [@GretzParsingHebrewCHILDES2015]. These "gold-standard" pre-parsed corpora are called treebanks, and repositories of them they have been created for many languages. Building on existing databases of knowledge, these many of these parsers use statistical models to determine the most likely syntactic structure and conjugation for each word in each sentence.

Some parsers, however, are instead simply given entirely unparsed corpora and no knowledge of the language's syntactic structure. Working with nothing but the text itself, the program seeks out patterns and begins to create links and relationships that it deems significant.

Unfortunately, though automatic parsers have achieved surprising levels of accuracy in recent years, even the best continue to produce erroneous parsings. Some researchers have claimed 95% or higher accuracy, including for some Hebrew parsers.<!-- I think? source --> When dealing with such a large corpus, such as the Hebrew *OpenSubtitles2018* corpus consisting of nearly 200 million tokens, a best-case scenario for a 5% error threshold results in nearly 10 million incorrectly parsed words.

Undoubtedly, this can have a negative impact on the accuracy of lemma frequency counts. Many of the issues found in the FDOSH are not due to orthographic ambiguity, but simply to inaccurate parsing. Some, as shown in the previous section, are even caused by erroneous automatic tokenization (consider the lemma "שדיבר").

The good news is that automatic parsers are continually improving in accuracy. This is a problem that exists across the board, regardless of the corpus being used—unless it is manually parsed and lemmatized, which is nearly impossible for such large corpora. The tools and techniques outlined in this thesis do not directly deal with the process of parsing.
