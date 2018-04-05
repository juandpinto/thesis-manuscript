# Methods: Creating the Conversational Hebrew Vocabulary List (CHVL)


## Overview

## The corpus

Before coding or analyzing anything, it's important to find an appropriate corpus to use and to become familiar with its structure. A useful place to begin is [OPUS](http://opus.nlpl.eu), which is part of the Nordic Language Processing Laboratory (NLPL), and hosted by the CSC IT center in Finland. OPUS is a database of many open, parallel corpora. These include corpora of movie and television subtitles, TED talks, web-crawled data, newspapers, and of course, books. The corpora are all free and open to the public.

The CHVL was created using one of OPUS's corpora, the [OpenSubtitles2018](http://opus.nlpl.eu/OpenSubtitles2018.php) corpus. The corpus can be downloaded in a variety of formats, and can be downloaded either as *parallel* corpora, or as a monolingual corpus. A parallel corpus consists of two languages interwoven together. For example, a line from the English subtitles of a movie will be paired with the same line from the French subtitles of the same movie. In theory, this means that each line of the corpus should have the same meaning in two different languages. The creation of parallel corpora has made possible many interesting and useful tools for linguistics, translators, and language learners. These include the open-source [CASMACAT](http://www.casmacat.eu) project and the [ReversoContext](http://context.reverso.net/translation/) tool.

For the purpose of creating a word list, a monolingual corpus is best. Note that parallel corpora will often be composed of less tokens than monolingual ones. This is because parallel corpora will only include movies for which the subtitles exist in both selected languages.

Though it's possible to download plain text files, the most useful format available for download is XML. Indeed, the most common file format used for large corpora is XML.<!-- source? --> The XML structure allows for nested key-value pairs, which are especially useful for parsed corpora that contain extensive metadata. XML is comparable to JSON, which we will use later to extract specific movie metadata directly from a database.

Another factor to consider is whether to download an untokenized, tokenized, or parsed corpus. An untokenized corpus contains simply the raw lines of text as found in the original subtitle files (divided into lines as they would appear while watching the movie, and labeled with the appropriate time for them to be shown):
```{.xml}
<s id="49">
  <time id="T39S" value="00:03:22,280" />
?מה אתה אומר, שרלוק
  <time id="T39E" value="00:03:24,120" />
</s>
```

A tokenized corpus has further been split into individual words and punctuation, such that each word is tagged on its own:

```{.xml}
<s id="49">
  <time id="T39S" value="00:03:22,280" />
  <w id="49.1">מה</w>
  <w id="49.2">אתה</w>
  <w id="49.3">אומר</w>
  <w id="49.4">,</w>
  <w id="49.5">שרלוק</w>
  <w id="49.6">?</w>
  <time id="T39E" value="00:03:24,120" />
</s>
```

A parsed corpus contains much more information for each token. The data included depends on the features of the language and on the parsing script used, but it can include things such as part of speech, syntactic role, lemma, and even specific features like gender, person, and number. Here is an example:

```{.xml}
<s id="49">
  <time value="00:03:22,280" id="T39S" />
  <w xpos="ADV" head="49.3" feats="PronType=Int" upos="ADV" lemma="מה"
      id="49.1" deprel="obj">מה</w>
  <w xpos="PRON" head="49.3" feats="Gender=Masc|Number=Sing|Person=2|
      PronType=Prs" upos="PRON" lemma="הוא" id="49.2" deprel="nsubj">אתה</w>
  <w xpos="VERB" head="0" feats="Gender=Masc|HebBinyan=PAAL|Number=Sing|
      Person=1,2,3|VerbForm=Part|Voice=Act" upos="VERB" misc="SpaceAfter=No"
      lemma="אמר" id="49.3" deprel="root">אומר</w>
  <w xpos="PUNCT" head="49.3" upos="PUNCT" lemma="," id="49.4"
      deprel="punct">,</w>
  <w xpos="NOUN" head="49.3" feats="Gender=Masc|Number=Sing" upos="NOUN"
      misc="SpaceAfter=No" lemma="שרלוק" id="49.5" deprel="obj">שרלוק</w>
  <w xpos="PUNCT" head="49.3" upos="PUNCT" misc="SpaceAfter=No" lemma="?"
      id="49.6" deprel="punct">?</w>
  <time value="00:03:24,120" id="T39E" />
</s>
```


All of the data used to create the CHVL came from a monolingual parsed corpus of Hebrew. The parsing was all done automatically using <!-- ?? -->.


## Cleaning the corpus

Once downloaded, the files inside the zipped folder are organized as follows:

```
Zipped folder in GZ format
 ├── Folder for year X
 │   ├── Folder for movie A
 │   │   ├── Zipped XML in GZ format
 │   │   ├── Zipped XML in GZ format
 │   │   └── Zipped XML in GZ format
 │   ├── Folder for movie B
 │   │   ├── Zipped XML in GZ format
 │   │   └── Zipped XML in GZ format
 ├── Folder for year Y
 │   ├── Folder for movie C
 │   │   └── Zipped XML in GZ format
 │   ├── Folder for movie D
 │   │   ├── Zipped XML in GZ format
 │   │   ├── Zipped XML in GZ format
 │   │   └── Zipped XML in GZ format
 │   ├── Folder for movie E
 │   │   ├── Zipped XML in GZ format
 │   │   └── Zipped XML in GZ format
 └── Folder for year Z
       └── Folder for movie F
           ├── Zipped XML in GZ format
           └── Zipped XML in GZ format
```

This organization is straight-forward, except for the fact that there are multiple XML files for each movie. The subtitle files that OPUS has collected, parsed, organized, and made available for mass download were all obtained from the [Open Subtitles]() project (hence the name of the corpus).<!-- reference --> Because this is a database where users can upload the subtitle files they extract from their own movie collection, there are often multiple uploads for the same movie. For our purposes, this results in movies that can have anywhere from a single subtitle file to dozens of them. Unfortunately, though the tokens in the files themselves are usually the same (with only minor variations in the XML metadata), this is not always true.

Part of cleaning the corpus, then, entails getting rid of these duplicates. As a means of simplifying the entire process, I chose simply to use the first file in each movie folder. I've included the short Python script for this in its entirety in [Appendix 3.3](link?). However, I will here explain what it does in detail so that it can be easily modified to fit different circumstances.

The script first makes a copy of the entire folder structure in the original downloaded (and unzipped!) corpus into a new directory. It then finds the first XML file in each movie folder and copies it into the appropriate place in the new folder structure. This means that it doesn't delete or otherwise change the files in the original corpus in any way.

The first block of code imports necessary modules that are used later in the script (`shutil` and `os`). Lines 7 and 8 define where the original corpus is (`source`), and where the new one will be placed (`destination`).

<!-- Does the downloaded corpus include _parsed in the name? If not, change here and in the actual script. -->

``` {#single_file_extract .python .numberLines startFrom="4"}
import shutil
import os

source = '../OpenSubtitles2018_parsed'
destination = './OpenSubtitles2018_parsed_single'
```

Next, a single line of code copies all directories and subdirectories into their new location.

``` {#single_file_extract .python .numberLines startFrom="11"}
shutil.copytree(source, destination, ignore=shutil.ignore_patterns('*.*'))
```

Lastly, we create a variable that holds all the XML files located in each movie folder, trim the list to just one, and copy that one into its new location. This process is carried out for one movie folder at a time. The originals are left untouched.

``` {#single_file_extract .python .numberLines startFrom="14"}
for dirName, subdirList, fileList in os.walk(source):
    for fname in fileList:
        if fname == '.DS_Store':
            fileList.remove(fname)
    if len(fileList) > 0:
        del fileList[1:]
        src = dirName + '/' + fileList[0]
        dst = destination + dirName[27:] + '/'
        shutil.copy2(src, dst)
```


## Reading data


## Counting and calculating







#### Using original-language movies exclusively

One of the potential downsides of using the OpenSubtitles2018 corpus is that it includes all subtitles of a specific language, even *translated* subtitles from movies filmed in other languages. The question is, does a translated script represent true conversational language as well as an original script?

This is a question that requires more research in order to answer satisfactorily. Though translated subtitles don't need to try to approximate the length and mouth shapes that a dubbed script does, its quality still largely depends on the skills of a translator. Most importantly, it's possible that a translation will not accurately reflect the register of the original. Again, these are important points to consider.

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




## The CHVL




## Challenges and future direction
