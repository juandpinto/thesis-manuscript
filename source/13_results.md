\newpage

# The CHVL: A vocabulary list of conversational Modern Hebrew

## Overview

The Conversational Hebrew Vocabulary List in its entirety can be found as an electronic supplement to this thesis (in CSV format) or at the following GitHub repository: *<https://github.com/juandpinto/opus-lemmas>*. It contains the most common 5,000 lemmas of conversation Modern Hebrew, as found in the OpenSubtitles2018 corpus. A sample of the first 1,000 lemmas is included in [*Appendix 1*](#appendix-1).

For discussion purposes, a small sample of the first 20 items is here presented.<!-- expand to 30 items? and fix formatting -->

| <!----> | LEMMA | FREQUENCY | RANGE | U~DP~              |
|--------:|------:|----------:|------:|:-------------------|
|       1 |   הוא |  23446109 | 43455 | 0.9480170255915042 |
|       2 |     ל |   5638813 | 43448 | 0.9420130372643667 |
|       3 |     ה |   9850733 | 43458 | 0.929266134661147  |
|       4 |     ב |   4812778 | 43450 | 0.9292364864789281 |
|       5 |    את |   6846782 | 43426 | 0.9285176069174289 |
|       6 |    לא |   5272808 | 43433 | 0.9145688112131216 |
|       7 |     ש |   3880654 | 43439 | 0.9088900047303463 |
|       8 |    של |   3892328 | 43445 | 0.9067041511201389 |
|       9 |    על |   1766990 | 43430 | 0.9042865019832009 |
|      10 |    זה |   5118759 | 43441 | 0.9015544612816044 |
|      11 |    מה |   2362419 | 43403 | 0.8922532708182579 |
|      12 |   היה |   2579370 | 43420 | 0.8909904417204713 |
|      13 |     מ |   1061614 | 43411 | 0.88900672760779   |
|      14 |   כול |   1325676 | 43414 | 0.8860074112131449 |
|      15 |     ו |   1906717 | 43429 | 0.8852706380348441 |
|      16 |    יש |   1069358 | 43376 | 0.8770543442171884 |
|      17 |    עם |    839575 | 43331 | 0.8668140051895192 |
|      18 |    אם |    861163 | 43321 | 0.8654587702150129 |
|      19 |   ידע |   1202416 | 43323 | 0.8586088803742931 |
|      20 |   אבל |    921757 | 42963 | 0.8519038846130076 |

Besides lemmas and their number in the list, the CHVL includes three pieces of information: frequency, range, and U~DP~. Frequency in this case is the raw frequency, or the total number of times the lemma appears in the OpenSubtitles2018 corpus.<!--I should probably change this to show freq/million tokens--> The range is the number of sub-corpora—or in this case, movies—the lemma appears in.

The most important piece of information the list provides, however, is the U~DP~, which refers to Griers' usage coefficient for dispersion.<!--source--> This is discussed more in-depth in the methods section above. U~DP~ is also used as the sorting measure for the CHVL.

The percentage of the corpus that is covered by the first *n* items on the list is referred to as coverage. This is a simple matter of finding the total number of tokens in the corpus, and dividing from it the sum of all the *raw* frequencies from the first *n* items.

For example, the sum of the frequencies of the first 20 lemmas in the sample above (84,656,819) divided by the total size of the corpus (193,755,220) is 0.436926649. In theory, this means that by knowing just the first 20 lemmas on the CHVL one would be able to understand 43.7% of the words in the entire OpenSubtitles2018 corpus! That is a clear example of the power of Zipf's Law (see [*Introduction*](#introduction) for more on Zipf's Law).

Here is a listing of some important coverages provided by different amounts of lemmas on the CHVL:

*n* Lemmas | Frequency Sum | ÷ Corpus Size | = Coverage
----------:|:-------------:|:-------------:|:---------:
       374 |  135,767,644  |  193,755,220  |    70%
       939 |  155,016,588  |  193,755,220  |    80%
     4,246 |  174,380,519  |  193,755,220  |    90%
    13,758 |  184,067,666  |  193,755,220  |    95%

The entire CHVL consists of 5,000 lemmas. This number was chosen in order for it to include the required items for 90% coverage, while also making it an even factor of 1,000. In its entirety, the CHVL covers 90.8% of the corpus from which it is created.

<!--
## Use

The purpose of the CHVL is to provide a list of the most commonly-used lemmas in conversational Modern Hebrew.
 -->




## Challenges and future direction

Throughout the course of this project, I have encountered several issues that are worth discussing. Some of these are questions that require further study in order to address adequately. Others are technical issues related to the complex task of pre-processing and parsing the corpus—something not directly dealt with in this thesis. Others yet are simple suggestions that I simply did not have time to implement given this project's time constraints. And finally, there are limitations that are the inevitable result of the tools at hand.

I have divided all of these issues into two categories: methodological challenges of a bigger nature, and functional challenges of a more limited scope.


### Methodological challenges

One of the more obvious issues of this project is the use of a corpus of movie subtitles as substitute for a corpus of true conversational language. This issue in a way forms the backbone of the CHVL, and it is at the heart of what this project is all about. Though I discuss several points related to this in the *Background* section of this thesis, I will here discuss some of its implications for future work.


#### Ideal vs. practical corpora

The use of a subtitle corpus has both positive and negative aspects. As mentioned earlier, the early research that has been done on the topic indicates that movie subtitles share many features with spontaneous, spoken language.<!-- sources --> This includes a high level of correlation between the two <!-- sources -->, as well as a strong ability to predict the outcomes of a lexical decision task <!-- sources -->.

One especially positive aspect of subtitle corpora is their accessibility. Thanks to the efforts of organizations such as *<http://opensubtitles.com>* and [OPUS](http://opus.nlpl.eu), very large corpora are available to the public for free. And they already come pre-processed, as an additional incentive for the time-constrained researcher.

This free and open nature makes subtitle corpora excellent tools for research in languages that don't yet have large, high-quality corpora of spoken language. Though advances in technology are rapidly making this type of data-collection more accessible, the costs remain too high for many less-commonly taught languages as of now. This is largely due to the arduous process of transcribing audio recordings.[@IzreelTranscribingSpokenIsraeli2004]

An ideal corpus for this sort of task would consist of many millions of tokens of recorded, transcribed, and parsed, spontaneous spoken language. Several attempts have been made to create a corpus of this nature in Hebrew.

The most prominent of these is the [Corpus of Spoken Israeli Hebrew (CoSIH)](http://cosih.com/), created at Tel Aviv University between 2000 and 2002.[@IzreelDesigningCoSIHCorpus2001] Designed and initiated by a team of distinguished scholars, it unfortunately ran out of funding long before its goals were met. The CoSIH website (*<http://cosih.com/>*) makes available to the public a total of 13.5 hours of recorded Hebrew, with just over five hours of it having been transcribed.

Though a few publications have used data from CoSIH, these have been primarily methodological studies for the design of the project itself.[@AmirCharacteristicsIntonationUnit2004; @IzreelIntonationUnitsStructure2005; @MettouchiOnlyProsodyPerception2007] At least one dissertation, by Nurit Dekel, uses data exclusively from CoSIH. Her entire corpus consists of 44,000 tokens. [-@Dekelmattertimetense2010, p.7]

Other corpora of spoken Hebrew include the Haifa Corpus of Spoken Hebrew [@YaelHaifaCorpusSpoken2014] and the Hebrew CHILDES corpus [@AlbertHebrewCHILDEScorpus2013; @GretzParsingHebrewCHILDES2015]. The first consists of 17.5 hours of audio recordings, along with a limited selection of transcribed text. The latter is a collection of recordings of interactions between adults and children, comprising a total of 417,938 transcribed tokens. The CHILDES corpus is unique in that the transcriptions are provided using a Latin-based phonemic transliteration. This was done in order to avoid many of the textual ambiguities of using the Hebrew script, which are addressed below under *Functional challenges*.

Though ideal in some ways, these corpora remain far too small to be effectively used for the creation of frequency lists. Even combined into a single corpus (which would introduce a series of new issues to solve), the total size would not be bigger than two million tokens. As discussed earlier in this thesis, Sorell provides evidence to suggest that a corpus of 20–50 million tokens is the minimum for a stable word list.[-@Sorellstudyissuestechniques2013]

Are movie and television subtitles an suitable substitute for spontaneous, spoken language? Early studies suggest it is at least adequate, but much more research is needed to answer this question definitively. For now, it remains as one practical option.


#### Using original-language movies exclusively

One of the potential downsides of using the OpenSubtitles2018 corpus not yet discussed is that it includes all subtitles of a specific language, even *translated* subtitles from movies filmed in other languages. The question is, does a translated script represent true conversational language as faithfully as an original script?

This is a question that requires more research in order to answer satisfactorily. Though translated subtitles don't need to try to approximate the utterance length and visual cues that a dubbed script does, its quality still largely depends on the skills of a translator. Most importantly, a translation may not accurately reflect the register of the original, no longer serving as a representation of conversational language. Again, these are important points to consider.

One solution is to simply use movies that were originally filmed in the target language of the corpus. In theory, each XML file in a monolingual OpenSubtitles2018 file should contain a tag that identifies the original language of the movie.<!-- cite article --> In practice, I found that the overwhelming majority of the files contained an empty `<lang>` tag instead. Luckily, there is a way to obtain the desired metadata for each movie in the corpus.

This can be done with a script that uses an application programming interface (API) to fetch specific information from an online movie database. The name of each movie folder in the corpus, which is simply a series of numbers, corresponds to that movies IMDb ID, which is a unique ID registered with the [Internet Movie Database](http://www.imdb.com/). This makes the process relatively easy, as we simply need to query the database using this ID to receive all of the movie's metadata.

Though IMDb does provide their own API, I decided instead to use an API created for the [Open Movie Database (OMDb)](http://www.omdbapi.com/). This API can be used free-of-charge, but it has a 1,000 movie limit per day. Since the OpenSubtitles2018 Hebrew corpus contains nearly 50,000 movies, I decided instead to pay for a daily limit of 100,000 movies. This only requires a $1.00 donation for each month that one is registered to use the OMDb API.

Once an API key is obtained, a script can be written to obtain the information desired for every movie all at once. In this case, we want to know the original language(s) for each movie.

This script in its entirety is found in [Appendix 2.2](14_appendix_2.md). It uses an imported Python wrapper for the API, written by [Derrick Gilland](https://github.com/dgilland), which can be found at <https://github.com/dgilland/omdb.py>. This package can be installed through PIP by entering `pip install omdb` into the command line.<!-- I need to have a small section or at least a footnote that explains the level of knowledge of Python required to use my scripts -->

For practical purposes, the script requires one to enter a specific year (or, more accurately, corpus folder name). If desired, an asterisk can act as wildcard: `python OMDb-fetch.py 1988` will fetch data for movies from 1988, while `python OMDb-fetch.py 198*` will do it for all movies in the 1980s. In order to fetch data for all movies in the database at once, use `python OMDb-fetch.py *`. I don't recommend this, however, since it may overload the server and cause the script to time out.

The script begins by creating a list of all movie directory paths for the desired year.

``` {#OMDb-fetch .python .numberLines startFrom="15"}
for name in glob.glob(
        './OpenSubtitles2018_parsed_single/parsed/he/' + year + '/*/'):
    IDs.append(name)
```

Each item in the list is then trimmed to include only the name of the movie folder, which is *almost* equivalent to the IMDb ID.

``` {#OMDb-fetch .python .numberLines startFrom="20"}
IDs = [os.path.basename(os.path.dirname(str(i))) for i in IDs]
```

In order to make the IDs match those in the database, additional zeros must be added to the beginning until they are seven digits long.

``` {#OMDb-fetch .python .numberLines startFrom="23"}
for i in IDs:
    while len(i) < 7:
        IDs[IDs.index(i)] = '0' + i
        i = '0' + i
```

The list is then sorted numerically in order to more easily interpret the results: `IDs.sort()`{.python}.

The API key is set in line 32, but be sure to replace `906517b3` with your own key, which can be obtained at <http://www.omdbapi.com/>.

``` {#OMDb-fetch .python .numberLines startFrom="32"}
omdb.set_default('apikey', '906517b3')
```

The script then prints a table header, fetches the title, year, and language(s) for each movie, and prints the results directly into the computer terminal.

``` {#OMDb-fetch .python .numberLines startFrom="35"}
print('# ' + year + '\n' +
      'IMDb ID\tTitle\tYear\tLanguage(s)')
```

``` {#OMDb-fetch .python .numberLines startFrom="39"}
      for i in IDs:
          doc = omdb.imdbid('tt' + i)
          print('tt' + i + '\t' +
                doc['title'] + '\t' +
                doc['year'] + '\t' +
                doc['language'])
```


### Functional challenges

A quick scan of the CHVL reveals some notable items. Some of these are mere quirks of the automatic parser, while others are the result of ambiguities.

For example, the very first lemma on the list is a bit unexpected. "הוא" is certainly not the most common lemma in Modern Hebrew. A quick look at some of the files in the corpus, however, reveals that all pronouns are grouped under this lemma. That is, אתה (you), היא (she), and אנחנו (we), just to name a few, are parsed as belonging to the lemma "הוא." Considering how common pronouns are in the majority of spoken dialogue (in many languages), its place at the top of the list ceases to be a surprise.<!-- source (Nation) -->

Another thing to note is that verbs are all listed in their traditional third-masculine-singular past conjugation. The first verb on the list is "היה"—a lemma referring to all forms of the verb להיות, including the infinitive. The same is true of "ידע" (item 19) and "דיבר" (item 60).

Many of the most common lemmas on the CHVL are prepositions. Note that even inseparable prepositions, such as -ה and -ב are considered independent lemmas by the parser, and are listed respectively as the lemmas "ה" and "ב".

Other issues, however, are more difficult to explain.


#### Textual ambiguity of Hebrew orthography

The flexible spelling conventions of Hebrew are at the root of many of the problems with the CHVL. For example, דִּבֵּר *he spoke* can be written as either דיבר ("full spelling") or דבר ("defective spelling"). There is also a noun, דָּבָר *thing*, that looks identical to the verb's defective spelling (דבר). Though the difference is usually clear from context, the automatic parser has some difficulty with this orthographic ambiguity.

The lemma "דבר" (item 27) includes instances of both the verb and the noun, which are completely unrelated. A simple search through the corpus reveals multiple examples of the noun דבר tagged with `lemma="דבר"`:

```{.xml}
<w xpos="NOUN" head="579.3" feats="Gender=Masc|Number=Sing" upos="NOUN" lemma="דבר" id="579.2" deprel="nsubj">דבר</w>

<w xpos="NOUN" head="200.11" feats="Gender=Masc|Number=Plur" upos="NOUN" lemma="דבר" id="200.12" deprel="obj">דברים</w>
```

We also find plenty of examples of the verb with the same lemma tag:

```{.xml}
<w xpos="VERB" head="0" feats="Gender=Fem|HebSource=ConvUncertainHead|Number=Sing|Person=3|Tense=Past" upos="VERB" lemma="דבר" id="2346.4" deprel="root">דברה</w>

<w xpos="VERB" head="0" feats="Gender=Fem,Masc|Number=Plur|Person=1|Tense=Past" upos="VERB" lemma="דבר" id="1270.2" deprel="root">דברנו</w>

<w xpos="VERB" head="0" feats="Gender=Fem,Masc|Number=Plur|Person=3|Tense=Past" upos="VERB" lemma="דבר" id="368.4" deprel="root">דברו</w>
```

A different lemma, "דיבר" (item 61), is the expected lemma for the verb since it follows the standard third masculine plural conjugation. Interestingly, however, the parser applies this lemma only to attestations of the word with an inserted *yod*, or with a *mem* or *lamed* prefix (present tense or infinitive). All other instances are parsed as the lemma "דבר." Though unexpected and simply wrong, at least this issue is consistent.

```{.xml}
<w xpos="VERB" head="840.4" feats="Gender=Fem,Masc|HebBinyan=HITPAEL|Number=Plur|Person=1|Tense=Past" upos="VERB" lemma="דיבר" id="840.16" deprel="conj">דיברנו</w>

<w xpos="VERB" head="1451.12" feats="Gender=Masc|HebBinyan=PIEL|Number=Sing|Person=1,2,3|VerbForm=Part|Voice=Act" upos="VERB" lemma="דיבר" id="1451.20" deprel="obl">מדבר</w>
```

To complicate matters more, we also find the unexpected lemmas "דיברה" (item 1184), "שדיבר" (item 2588), and "שדיברה" (item 4106).




Which, based on context (<!--sentence example(s)-->), should clearly be parsed as two separate lemmas, "ש" and "דיבר."

These are just a few among many examples of the difficulties encountered by the automatic parser. Though the parsing was carried out by the OPUS team as part of the corpus's pre-processing stage, it is valuable to at least have an idea of how it works its magic. I will here explain the basics of the process and some of the implications entailed.


<!--
Many more examples of specific issues can be included in this section. Examples:

The lack of vowels makes it so that the clearly different words עִם and עַם are combined into the single lemma "עם."

מ and מן are listed separately.
-->


#### Automatic parsing

Automatic parsing refers to the process of having a computer program create a syntactic tree for a corpus of natural language. Natural language, as opposed to artificial or constructed language, is notoriously complex in its structure. Natural language processing (NLP) is an entire field of research, currently at the forefront of computer science. Parsing can serve many purposes, from theoretical linguistic research to machine translation or even the creation of artificial intelligences such as Siri or Alexa. For our purposes, a parsed text is important in order to use lemmas as the word family level for the CHVL.<!-- source from Nation --> This decision is discussed under [*Identifying Words*](#identifying-words-word-family-levels) in this thesis.

Two distinct types of syntactic parsers exist, contituency parsers and dependency parsers. These are based on the two respective linguistic theories of syntax, constituent grammar (sometimes referred to as phrase structure grammar) and dependency grammar.

Constituent grammar is the classic syntax tree structure taught in introductory-level linguistics classes. It is essentially a theory of the logic structure of language as a whole. Dependency grammar is a competing theory that treats words as more directly interconnected to each other. A thorough description of these ideas is outside the scope of this thesis, and is not pertinent to the project. What is important to know is that dependency grammar, and thus dependency parsers, have played an important role in the advancement of NLP and computational linguistics as a whole. The term "automatic parser", therefore, most often refers to an automatic *dependency* parser.<!-- source(s)? -->

Some parsers proceed in a two-step process of morphological tagging (part of speech) and then dependency parsing (syntactic role and conjugations). In all cases, tokenization must first take place, which refers to splitting the text into individual lemmas.

Most automatic parsers are "trained" using a small corpus that has been manually parsed by a human previously, or at least one that was automatically parsed and then checked and corrected by the researcher.<!-- source:*Parsing Hebrew CHILDES transcripts* --> These "gold-standard" pre-parsed corpora are called treebanks, and repositories of them they have been created for many languages. Building on existing databases of knowledge, these many of these parsers use statistical models to determine the most likely syntactic structure and conjugation for each word in each sentence.

Some parsers, however, are instead simply given entirely unparsed corpora and no knowledge of the language's syntactic structure. Working with nothing but the text itself, the program seeks out patterns and begins to create links and relationships that it deems significant.

Unfortunately, though automatic parsers have achieved surprising levels of accuracy in recent years, even the best continue to produce erroneous parsings. Some researchers have claimed as 95% or higher accuracy, including for some Hebrew parsers.<!-- I think? source --> When dealing with such a large corpus, such as the Hebrew OpenSubtitles2018 corpus consisting of nearly 200 million tokens, a best-case scenario for a 5% error threshold results in nearly 10 million incorrectly parsed words.

Undoubtedly, this can have a negative impact on the accuracy of lemma frequency counts. Many of the issues found in the CHVL are not due to orthographic ambiguity, but simply to inaccurate parsing. Some, as shown in the previous section, are even caused by erroneous automatic tokenization (consider the lemma "שדיבר").

The good news is that automatic parsers are continually improving in accuracy. This is a problem that exists across the board, regardless of the corpus being used—unless it is manually parsed and lemmaticized, which is nearly impossible for such large corpora. The tools and techniques outlined in this thesis do not directly deal with the process of parsing. 
