\newpage

# Methods: Creating the *Frequency Dictionary of Spoken Hebrew* (FDOSH) {#methods}

As we have seen, the majority of research into high-quality frequency list creation has focused on *English* frequency lists. Outside of the English-speaking world, and especially when dealing with less commonly taught languages, it can be difficult to find well-researched frequency dictionaries, if they exist at all. Why have not more educators—those who may benefit from these dictionaries the most—decided to undertake such a task? Does it simply seem like too daunting of a project?

Some tools already exist that aid in the process of creating a frequency dictionary. One affordable example is the web tool [*SketchEngine*](https://www.sketchengine.eu), a European-based database of hundreds of corpora in many different languages. As is common for similar products, however, SketchEngine does not provide access to the raw corpora themselves—even though most of the corpora are available free of charge from their creators. Instead, it acts as a search portal through which one may peek into a corpus's data. This and other restrictions severely limit what researchers can do and the insights they can gain.

Rather than using SketchEngine or similar tools, I chose to create a series of simple scripts to create the *Frequency Dictionary of Spoken Hebrew*. They are designed to be easily customizable to suit researchers' needs.

The two most widely-used languages for the type of data analysis involved in creating a frequency dictionary are Python and R. I chose to use Python for this project. Python was designed specifically to be a very readable programming language. That is, it is easy to read and understand the purpose and flow of the code. This was one of my primary reasons for choosing to use it, since it increases the ease with which this project can be reproduced by other researchers and educators to create their own frequency lists. R, on the other hand, requires a deeper familiarity with the syntax and conventions of the language in order to understand and modify its scripts.

The second characteristic that makes Python ideal for an open-source project of this nature is its mild learning curve. Though considerable effort must be made to learn any programming language, Python is widely considered good for beginners because of its simplicity. With only a rudimentary knowledge of Python, even educators or enthusiasts without a coding background will be able to modify the scripts used here to suit their own needs. To that end, this chapter will carefully explain what, exactly, the code does.

Though all of the code is included in this thesis ([*Appendix B*](#appendix-b)), it can also be found as part of the project's supplementary materials [@PintoSupplementarymaterialscreating2018] at *<https://doi.org/10.5281/zenodo.1239886>*. This DOI serves as a permanent link to the latest stable release of the materials. Alternatively, the development repository can be accessed directly through GitHub at *<https://github.com/juandpinto/frequency-dictionary>*. This repository can be cloned, or individual files can be downloaded, for modification and use. The repository uses the version control system [*Git*](https://git-scm.com), which keeps track of all changes that have been made to each file. This makes it possible to search through the file histories to observe the project's creation process or to revert to an earlier stage.^[For a thorough introduction to Git and GitHub, see Chacon and Straub [-@ChaconProGit2014].]

Suggestions for improvements can also be submitted through the GitHub interface, allowing for a system of cooperation and incremental innovation among researchers. The exported *Frequency Dictionary of Spoken Hebrew*, in its entirety, can also be found within the repository.

This thesis, then, beyond explaining the theory behind the creation of the FDOSH, aims to make the process as reproducible as possible. This chapter contributes to that aim by carefully documenting each step of the process.


## The corpus

Before any coding or analyzing can be done, it's important to find an appropriate corpus to use and to become familiar with its structure. A useful place to begin is [OPUS](http://opus.nlpl.eu), which is part of the Nordic Language Processing Laboratory (NLPL), and hosted by the CSC IT center in Finland. OPUS is a database of many open, parallel corpora. These include corpora of film and television subtitles, TED talks, web-crawled data, newspapers, and of course, books. The corpora are all free and open to the public.

The FDOSH was created using one of OPUS's corpora, the [*OpenSubtitles2018*](http://opus.nlpl.eu/OpenSubtitles2018.php) corpus. The corpus can be found in a variety of formats, and it can be downloaded either as a *parallel* corpus or as a monolingual corpus. A parallel corpus consists of two or more languages interwoven together. For example, a line from the English subtitles of a movie will be paired with the same line from the French subtitles of the same movie. This means that each line of the corpus will theoretically carry the same meaning in multiple languages. The creation of parallel corpora has made possible many interesting and useful tools for linguists, translators, and language learners. These include the open-source [CASMACAT](http://www.casmacat.eu) project and the [ReversoContext](http://context.reverso.net/translation/) tool.

For the purpose of creating a frequency dictionary, a monolingual corpus is best. Note that parallel corpora will often be composed of fewer tokens than monolingual ones. This is because parallel corpora will only include movies for which the subtitles exist in all of the selected languages.

Though it is possible to download plain text files, the most useful format available is XML. Indeed, this is the most common file format used for large corpora. The XML structure allows for nested key-value pairs, which are especially useful for parsed corpora that contain extensive metadata. XML is comparable to JSON—a similar format of nested tags based on the JavaScript language—which we will use in the next chapter to extract specific movie metadata directly from an online database.

Another factor to consider is whether to download an untokenized, tokenized, or parsed corpus. An untokenized corpus contains simply the raw lines of text as found in the original subtitle files (divided into lines as they would appear while watching the movie, and labeled with the appropriate time for them to be shown):

```{.xml}
<s id="49">
  <time id="T39S" value="00:03:22,280" />
?שרלוק ,אומר אתה מה
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


All of the data used to create the FDOSH came from a monolingual parsed corpus of Hebrew. The parsing was all done automatically—a process that will be discussed in the [*automatic parsing*](#automatic-parsing) section of the next chapter.


## Cleaning the corpus

Unlike many corpora, the OpenSubtitles2018 corpus as presented in its downloadable form has already undergone significant preprocessing by the OPUS team [@LisonOpenSubtitles2016Extractinglarge2016]. This is good news, since data cleaning is often the most laborious part of the process. However, there is one task that must be addressed before the corpus can be used to create a frequency list: deduplication.

The files inside the downloaded folder are organized as follows:

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

This organization is straightforward, but there is the issue of having duplicate XML files for each movie. The subtitle files that OPUS has collected, parsed, organized, and made available for mass download were all obtained from the [*Open Subtitles*](https://www.opensubtitles.org/) project (hence the name of the corpus). Because this is a database where users can upload the subtitle files they extract from their own movie collection, there are often multiple uploads for the same movie. For our purposes, this results in movies that can have anywhere from a single subtitle file to dozens of them. Unfortunately, though the tokens in the files themselves are usually the same (with only minor variations in the XML metadata), this is not always true. A few of the variant files do seem to be different translations.

Part of cleaning the corpus, then, entails getting rid of these duplicates. As a means of simplifying the entire process, I chose simply to use the first file in each movie folder. I've included the short Python script for this,`single_file_extract.py`, in [*Appendix B.2*](#appendix-b.2). I will here explain what it does in detail so that it can be easily modified to fit different circumstances.

The script first makes a copy of the entire folder structure in the original downloaded (and unzipped!) corpus into a new directory. It then finds the first XML file in each movie folder and copies it into the appropriate place in the new folder structure. This means that it doesn't delete or otherwise change the files in the original corpus in any way.

The first block of code imports necessary modules that are used later in the script (`shutil` and `os`). Lines 7 and 8 define where the original corpus is (`source`), and where the new one will be placed (`destination`).

``` {#single_file_extract .python .numberLines startFrom="4"}
import shutil
import os

source = '../OpenSubtitles2018_parsed'
destination = './OpenSubtitles2018_parsed_single'
```

Next, a single line of code copies all directories and subdirectories into their new location.

``` {#single_file_extract .python .numberLines startFrom="10"}
# Copy the directory tree into a new location
shutil.copytree(source, destination,
                ignore=shutil.ignore_patterns('*.*'))
```

Lastly, we create a variable that holds all the XML files located in each movie folder, trim the list to just the first file, and copy that one into its new location. This process is carried out for one movie folder at a time. The originals are left untouched.

``` {#single_file_extract .python .numberLines startFrom="14"}
# Copy the first file in each folder into the new tree
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

With a newly organized version of the corpus, it's now possible to begin the process of reading and processing data. At this stage, I took some time to gather metadata for all the movies in the corpus in order to identify movies that were originally filmed with Hebrew as their primary language (as opposed to translated subtitles). Because I ultimately decided against this approach for the creation of the FDOSH, I will skip that step here. However, a description of that entire process will be discussed in the next chapter under [*using original-language movies exclusively*](#using-original-language-movies-exclusively).


## Extracting data

Before calculating any measures, such as frequency or range, individual lemmas must be extracted from the XML files in the downloaded corpus. There are two ways to go about this. Because XML consists of nested tags and key-value pairs, a dedicated XML parsing tool can be used to extract specific information. In this case, we would be creating a list of all *values* in the `lemma` *key* within each `<w>` *tag*. The value that corresponds to the `lemma` tag below for the word אומר is "אמר".

``` {.xml}
<w xpos="VERB" head="0" feats="Gender=Masc|HebBinyan=PAAL|Number=Sing|
    Person=1,2,3|VerbForm=Part|Voice=Act" upos="VERB" misc="SpaceAfter=No"
    lemma="אמר" id="49.3" deprel="root">אומר</w>
```

A different approach is to use *regular expressions* to search for a specific string of characters and extract every instance of that string. This is a more brute-force approach, since it ignores the structure of the XML file and treats it all simply as raw text. To find a lemma, a very simple regular expression is sufficient: `lemma="[א-ת]+"`. This will search for any instance of the characters `lemma="`, followed by a combination of any number of Hebrew letters (at least one), followed by the character `"`.

Despite the existence of various Python modules for parsing XML files, I found a simple search using regular expressions to be more efficient for various reasons. First, not all *<w>* elements in the parsed corpus contain *lemma* attributes. Second, punctuation and non-Hebrew words are often lemmatized. This means that even after extracting all the *lemma* values in a file, I would still need to use regular expressions to search through the results and delete any that contain non-Hebrew characters. I chose instead to skip the XML parsing step altogether.

I will now explain the code in the script used to create the FDOSH, `create-freq-list.py`. As with the other code, the script in its entirety can be found in [*Appendix B*](#appendix-b).

After importing necessary packages and initializing variables, two functions near the beginning of the script serve to open a file and extract a list of lemmas from it.

``` {#create-freq-list .python .numberLines startFrom="40"}
# Open XML file and read it.
def open_and_read(file_loc):
    with gzip.open(file_loc, 'rt', encoding='utf-8') as f:
        read_data = f.read()
    return read_data
```

``` {#create-freq-list .python .numberLines startFrom="47"}
# Search for lemmas and add counts to "lemma_by_file_dict{}".
def find_and_count(doc):
    file = str(f)[40:-3]
    match_pattern = re.findall(r'lemma="[א-ת]+"', doc)
    for word in match_pattern:
        if word[7:-1] in lemma_by_file_dict:
            count = lemma_by_file_dict[word[7:-1]].get(file, 0)
            lemma_by_file_dict[word[7:-1]][file] = count + 1
        else:
            lemma_by_file_dict[word[7:-1]] = {}
            lemma_by_file_dict[word[7:-1]][file] = 1
```

We then run both of these functions for each XML file in the corpus directory (defined earlier in the `corpus_path` variable).

``` {#create-freq-list .python .numberLines startFrom="67"}
for dirName, subdirList, fileList in os.walk(corpus_path):
    if len(fileList) > 0:
        total_files_int = total_files_int + 1
        f = dirName + '/' + fileList[0]
        find_and_count(open_and_read(f))
```

The `find_and_count()`{.python} function finds each instance of the string described above using a regular expression, then adds the Hebrew part of the string—the lemma itself—to a dictionary. The dictionary is named `lemma_by_file_dict`, and its underlying structure looks like this:

```{.sh}
'lemma': {'path of file': 'frequency of lemma in file'}
```

A Python dictionary is at its core a list of *key*:*value* pairs. Much like an actual dictionary consists of words and their definitions, this dictionary's keys are made up of all the individual lemmas found by our search. For each lemma, the value is another dictionary—thus making it a nested dictionary, or a dictionary within a dictionary. The keys for each inner dictionary are the paths of all the XML files (movies) that the lemma appears in, and the value of each is an integer that represents how many times that lemma appears in that particular file (frequency).

After the script reads each file, it returns a complete dictionary. Here is a simplified example:

```
'ב': {
        '/he/0/5753574/6853341.xml': 168,
        '/he/0/3607000/5764778.xml': 94},
'פרק': {
        '/he/0/5753574/6853341.xml': 3},
'קודם': {
        '/he/0/5753574/6853341.xml': 6,
        '/he/0/3607000/5764778.xml': 2,
        '/he/0/1278351/3777598.xml': 1}
```

Throughout the rest of the script, this nested dictionary serves as the basis for all of the necessary calculations.


## Calculations

For each lemma, the FDOSH includes three measures: frequency, range, and dispersion. Dispersion is used as the sorting value. Though the theoretical underpinnings of each have already been discussed in the [*objective design*](#objective-design) section of the previous chapter, I will here give a brief reminder of what each measure is and explain how it is calculated by the `create-freq-list.py` script. Range will be addressed afterward in the (*sort and export*)[#sort-and-export] section, since the script calculates it on the spot as the list is created.


### Frequency {#methods-frequency}

Since we've already calculated the frequency of each lemma for each individual file, calculating total frequency per lemma is straightforward. The script simply creates a new dictionary, `lemma_totals_dict`, and adds to it every lemma in the corpus as its keys, with the corresponding value being a sum of the frequencies in all files for that lemma. In other words, `{'lemma1':'frequency1', 'lemma2':'frequency2', 'lemma3':'frequency3', . . . }`.

``` {#create-freq-list .python .numberLines startFrom="119"}
# Calculate total raw frequencies per lemma
for lemma in lemma_by_file_dict:
    lemma_totals_dict[lemma] = \
        sum(lemma_by_file_dict[lemma].values())
```

Following the simplified example from the previous section, this would result in the following dictionary:

```
262:'ב',
3:'פרק',
9:'קודם'
```

We now have raw frequency counts, but we need to turn them into normalized frequencies, using 1,000,000 as our normalizing figure. To do this, we perform the following equation for each lemma:

$$\textbf{normalized frequency}\ =\ \frac{frequency\ of\ lemma}{total\ tokens\ in\ corpus}\ \times\ 1,000,000$$

In order to find the token count for the entire corpus, we first make a dictionary—`token_count_dict`—that contains an entry for each file in the corpus and the number of tokens in that file, using the *key*:*value* pairs of *file*:*tokens*. Since we already have a dictionary variable that contains the number of times each lemma appears in each file, `lemma_by_file_dict`, we don't need to open and read the files again. Instead, we can add the values in this dictionary and rearrange them into what we want.

``` {#create-freq-list .python .numberLines startFrom="124"}
# Calculate token count per file
for lemma in lemma_by_file_dict:
    for file in lemma_by_file_dict[lemma]:
        token_count_dict[file] = token_count_dict.get(
            file, 0) + lemma_by_file_dict[lemma][file]
```

We can now add each of these entries to find the total count and save it in an integer variable, `total_tokens_int`. We took the intermediary step of creating the dictionary `token_count_dict` because we will later need the values it holds (tokens in each file) in order to calculate dispersion.

``` {#create-freq-list .python .numberLines startFrom="130"}
# Calculate total token count
for file in token_count_dict:
    total_tokens_int = \
        total_tokens_int + token_count_dict.get(file, 0)
```

The script now calculates all the normalized frequencies using the equation described earlier. The value by which the frequencies will be normalized can easily be modified in line 136 of the code.

``` {#create-freq-list .python .numberLines startFrom="135"}
# Set value for normalized frequency (freq per x words)
freq_per_int = 1000000

# Calculate normalized frequencies per lemma
for lemma in lemma_totals_dict:
    lemma_norm_dict[lemma] = \
        lemma_totals_dict[lemma] / total_tokens_int * freq_per_int
```

The dictionary `lemma_norm_dict` now contains the normalized frequency of each lemma.


### Dispersion (*U~DP~*) {#methods-dispersion}

Calculating dispersion is more complicated. In theory, it should provide a single quantifiable measure that incorporates both frequency and range, and which can then be used to sort the frequency list. The model of dispersion I have chosen to follow for this project is a usage coefficient of Gries's deviation of proportions, or *U~DP~* [@GriesDispersionsadjustedfrequencies2008; @GriesDispersionsadjustedfrequencies2010].

In order to calculate *U~DP~* for lemma~x~, we must first make two calculations for each file in the corpus (file~i~): the lemma's *expected frequency* if it were perfectly distributed, and its *observed frequency*—or its actual frequency.

$$\textbf{expected frequency}\ =\ \frac{tokens\ in\ file_i}{tokens\ in\ corpus}$$

$$\textbf{observed frequency}\ =\ \frac{frequency\ of\ lemma_x\ in\ file_i}{frequency\ of\ lemma_x\ in\ corpus}$$

We must then subtract the lemma's observed frequency from its expected frequency, which will return a value between -1 and 1. We can normalize this result by finding the absolute value. Now the closer the result is to 0, the closer that lemma's frequency is in that particular file to what we would expect if it were perfectly distributed throughout the corpus. A higher number (closer to 1), would indicate a heavier load in that file than we would expect.

By performing this calculation for every file in the corpus, adding them all together, and dividing the result by two (since we're using the absolute value and are therefore adding values that originally existed in both a positive and a negative direction), we now have Gries's *DP*. Where `n` is the number of files:

$$\textbf{DP}\ =\ 0.5 \sum_{i=1}^{n} |\ \text{expected frequency}\ -\ \text{observed frequency}\ |$$

A *DP* of 0 represents a perfectly even dispersion, and a *DP* close to 1 means a more uneven distribution, where fewer files contain a larger load of the lemma's overall frequency. A *DP* of 1 is not actually possible.

Gries's usage coefficient, or *U~DP~*, is an attempt to make this number more useful. *DP* is first subtracted from 1 and the result is multiplied by the lemma's total frequency. The full equation for *U~DP~* is as follows:

\begin{small}

$$\mathbf{U_{DP}}\ =\ \left(1 - 0.5 \sum_{i=1}^{n} \left|\ \frac{file_i\ tokens}{total\ tokens}\ -\ \frac{frequency_x\ in\ file_i}{total\ frequency_x}\ \right|\ \right) \times total\ frequency_x$$

\end{small}

In order to calculate this, the script must first find the number of tokens in each file. Luckily, we already did this while calculating normalized frequency, above. The dictionary `token_count_dict` contains these token counts. We've also already taken the step of adding these values together into the integer variable `total_tokens_int`, also while preparing to calculate normalized frequency.

With all of these measures in place, the script can now calculate *DP* and then *U~DP~* using the equations described above. It does this for each lemma, saving the new measures into their respective dictionaries, `lemma_DPs_dict` and `lemma_UDPs_dict`.

``` {#create-freq-list .python .numberLines startFrom="143"}
# Calculate DPs
for lemma in lemma_by_file_dict.keys():
    for file in lemma_by_file_dict[lemma].keys():
        lemma_DPs_dict[lemma] = lemma_DPs_dict[lemma] + abs(
            (token_count_dict[file] /
             total_tokens_int) -
            (lemma_by_file_dict[lemma][file] /
             lemma_totals_dict[lemma]))
lemma_DPs_dict = {lemma: DP/2 for (lemma, DP) in
                  lemma_DPs_dict.items()}

# Calculate UDPs
lemma_UDPs_dict = {lemma: (1-DP)*lemma_norm_dict[lemma] for
                   (lemma, DP) in lemma_DPs_dict.items()}
```

With these values calculated and saved for each lemma, the only thing left is to sort and export the final list.


## Sort and export

In order to ensure that the words on the list do not have an abnormally high frequency in some subcorpora (movies) and are nearly absent in others, some have suggested setting a minimum range or dispersion and discarding words below this threshold (see the [*objective design*](#objective-design) section in the previous chapter).

Rather than setting an arbitrary bar, the FDOSH is sorted entirely by *U~DP~*. This *modus operandi* ensures that the order of words itself—not just which words make it onto the list and which don't—is decided by a combination of both relevant measures: frequency and dispersion. This approach also has the added benefit of being entirely objective.

Since we've already calculated the *U~DP~* for each lemma, sorting the list is simple.

``` {#create-freq-list .python .numberLines startFrom="163"}
# Sort entries by UDP
UDP_sorted_list = [(k, lemma_UDPs_dict[k]) for k in sorted(
    lemma_UDPs_dict, key=lemma_UDPs_dict.__getitem__,
    reverse=True)]
```

A final table is then created (using a list of tuples, `table_list`), with each line consisting of a lemma, its rank, its *U~DP~*, its normalized frequency, and its normalized range. The table is created in an already-sorted order.

Because the script has not yet calculated range by this point, it must do so on the spot as it is entering each lemma into the table. It does this with a simple dictionary comprehension that quickly adds the number of files included in the `lemma_by_file_dict`. Since the FDOSH will display range as a percentage, the script takes this new sum of files in which each lemma appears, divides it by the total number of files in the corpus (`total_files_int`), and multiplies the result by 100.

Here is the resulting code:

``` {#create-freq-list .python .numberLines startFrom="170"}
i = 0
for k, v in UDP_sorted_list[:list_size_int]:
    i = i + 1
    row = (k,
           i,
           '{0:,.2f}'.format(v),
           '{0:,.2f}'.format(lemma_norm_dict[k]),
           '{0:,.2f}'.format(sum(1 for count in
                                 lemma_by_file_dict[k].values() if
                                 count > 0) /
                             total_files_int * 100))
    table_list.append(row)
```

Lastly, now that everything is organized into a table, the script opens—or creates, if it doesn't already exist—a TSV file, writes a header line into it (`LEMMA RANK DISPERSION FREQUENCY RANGE`), and exports the entire table into the file. It then closes it to clear the computer's memory cache.

``` {#create-freq-list .python .numberLines startFrom="226"}
result = open('./export/frequency-dictionary.tsv', 'w')
result.write('LEMMA\tRANK\tDISPERSION\tFREQUENCY\tRANGE\n')
for i in range(list_size_int):
    result.write(str(table_list[i][0]) + '\t' +
                 str(table_list[i][1]) + '\t' +
                 str(table_list[i][2]) + '\t' +
                 str(table_list[i][3]) + '\t' +
                 str(table_list[i][4]) + '\n')
result.close()
```

The frequency dictionary is now complete. The next chapter will explore the FDOSH itself more in-depth.
