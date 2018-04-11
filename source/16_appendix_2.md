\newpage

# Appendix 2: Scripts {#appendix-2 .unnumbered}

## Appendix 2.1: HebrewLemmaCount.py {#appendix-2.1 .unnumbered}

``` {#HebrewLemmaCount .python .numberLines}
#! /usr/bin/env python3
# -*- coding: utf-8 -*-

import re
import os
import gzip
from collections import defaultdict


############################################################
# ----------------- INITIALIZE VARIABLES ----------------- #
############################################################

# Define path for topmost directory to search. Make sure this points to
# the correct location of your corpus.
corpus_path = './OpenSubtitles2018_parsed_single'

# Initialize dictionaries
lemma_by_corpus_dict = {}
lemma_totals_dict = {}
token_count_dict = {}
lemma_DPs_dict = defaultdict(float)
lemma_UDPs_dict = defaultdict(float)

total_tokens_int = 0
table_list = []

# Set size of final list
list_size_int = 5000


############################################################
# ------------------- DEFINE FUNCTIONS ------------------- #
############################################################


# Open XML file and read it.
def open_and_read(file_loc):
    with gzip.open(file_loc, 'rt', encoding='utf-8') as f:
        read_data = f.read()
    return read_data


# Search for lemma and add counts to "frequency{}".
def find_and_count(doc):
    corpus = str(f)[38:-4]
    match_pattern = re.findall(r'lemma="[א-ת]+"', doc)
    for word in match_pattern:
        if word[7:-1] in lemma_by_corpus_dict:
            count = lemma_by_corpus_dict[word[7:-1]].get(corpus, 0)
            lemma_by_corpus_dict[word[7:-1]][corpus] = count + 1
        else:
            lemma_by_corpus_dict[word[7:-1]] = {}
            lemma_by_corpus_dict[word[7:-1]][corpus] = 1


############################################################
# -------------------- OPEN AND READ --------------------- #
############################################################

# Open and read all files. If calculating only for a specific language,
# comment out this code and uncomment the large block that follows.
#
for dirName, subdirList, fileList in os.walk(corpus_path):
    if len(fileList) > 0:
        f = dirName + '/' + fileList[0]
        find_and_count(open_and_read(f))

############################################################
# ---------------- LANGUAGE-SPECIFIC BLOCK -----------------
#
# This large block of code is for creating a list using only movies #
# with a specific primary language (in this case, Hebrew). Be sure to #
# uncomment the relevant lines of code, and to comment out the block #
# above. #
#
#
# Create list of IDs for movies with Hebrew as primary language. #
# This makes use of a text file that must already exist with this list. #
#
# Hebrew_IDs_list = []
# with open('./Hebrew_originals.txt', 'r', encoding='utf-8') as f:
#     read_data = f.read()
#     Hebrew_IDs_list = re.findall(r'\s\stt[0-9]+\t', read_data)
# Hebrew_IDs_list = [line[4:-1] for line in Hebrew_IDs_list]
#
#
# Delete extra 0s at the beginning of Hebrew movie IDs. #
#
# for item in Hebrew_IDs_list:
#     if item[0] == '0':
#         Hebrew_IDs_list[Hebrew_IDs_list.index(item)] = item[1:]
# for item in Hebrew_IDs_list:
#     if item[0] == '0':
#         Hebrew_IDs_list[Hebrew_IDs_list.index(item)] = item[1:]
#
#
# Open and read files for movies with Hebrew as the primary language. #
#
# for dirName, subdirList, fileList in os.walk(corpus_path):
#     if len(fileList) > 0:
#         f = dirName + '/' + fileList[0]
#         folders = re.split('/', dirName)
#         if folders[len(folders)-1] in Hebrew_IDs_list:
#             find_and_count(open_and_read(f))
#
# ------------- END OF LANGUAGE-SPECIFIC BLOCK -------------
############################################################


############################################################
# --------------------- CALCULATIONS --------------------- #
############################################################

# Calculate token count per corpus
for lemma in lemma_by_corpus_dict:
    for corpus in lemma_by_corpus_dict[lemma]:
        token_count_dict[corpus] = token_count_dict.get(
            corpus, 0) + lemma_by_corpus_dict[lemma][corpus]

# Calculate total frequencies per lemma
for lemma in lemma_by_corpus_dict:
    lemma_totals_dict[lemma] = sum(lemma_by_corpus_dict[lemma].values())

# Calculate total token count
for corpus in token_count_dict:
    total_tokens_int = total_tokens_int + token_count_dict.get(corpus, 0)

# Calculate DPs
for lemma in lemma_by_corpus_dict.keys():
    for corpus in lemma_by_corpus_dict[lemma].keys():
        lemma_DPs_dict[lemma] = lemma_DPs_dict[lemma] + abs(
            (token_count_dict[corpus] /
             total_tokens_int) -
            (lemma_by_corpus_dict[lemma][corpus] /
             lemma_totals_dict[lemma]))
lemma_DPs_dict = {lemma: DP/2 for (lemma, DP) in lemma_DPs_dict.items()}

# Calculate UDPs
lemma_UDPs_dict = {lemma: 1-DP for (lemma, DP) in lemma_DPs_dict.items()}


############################################################
# -------------- SORT LIST AND CREATE TABLE -------------- #
############################################################

# Sort entries by UDP
UDP_sorted_list = [(k, lemma_UDPs_dict[k]) for k in sorted(
    lemma_UDPs_dict, key=lemma_UDPs_dict.__getitem__,
    reverse=True)]

# Create list of tuples with all values (Lemma, Frequency, Range, UDP)
for k, v in UDP_sorted_list[:list_size_int]:
    table_list.append((k, lemma_totals_dict[k], sum(
        1 for count in lemma_by_corpus_dict[k].values() if count > 0),
        v))

############################################################
# ---------------- SORT-BY-FREQUENCY BLOCK -----------------
#
# Sort entries by raw frequency (total lemma count). To sort the final #
# list by frequency instead of UDP, comment out the above code within the #
# "SORT LIST AND CREATE TABLE" section, and also uncomment the relevant #
# lines of code in this block. #
#
#
# Sort entries by raw frequency #
#
# frequency_sorted_list = [(k, lemma_totals_dict[k]) for k in sorted(
#     lemma_totals_dict, key=lemma_totals_dict.__getitem__,
#     reverse=True)]
#
#
# Create list of tuples with all values (Lemma, Frequency, Range, UDP) #
#
# for k, v in frequency_sorted_list[:list_size_int]:
#     table_list.append((k, v, sum(
#         1 for count in lemma_by_corpus_dict[k].values() if count > 0),
#         lemma_UDPs_dict[k]))
#
# ------------- END OF SORT-BY-FREQUENCY BLOCK -------------
############################################################

# Calculate list size for 80% coverage and set that as the list size. Note
# that if the initial list_size_int (set near the beginning of the script)
# provides less than the desired coverage, it will default to that instead.
#
# added_freq_int = 0
# count = 0
# for k, v in UDP_sorted_list:
#     if added_freq_int / total_tokens_int < 0.8:
#         added_freq_int = added_freq_int + lemma_totals_dict[k]
#         count = count + 1
#     else:
#         break
# list_size_int = count

# Write final tallies to CSV file
result = open('./export/HebrewWordList2.csv', 'w')
result.write('LEMMA, FREQUENCY, RANGE, UDP\n')
for i in range(list_size_int):
    result.write(str(table_list[i][0]) + ', ' +
                 str(table_list[i][1]) + ', ' +
                 str(table_list[i][2]) + ', ' +
                 str(table_list[i][3]) + '\n')
result.close()

# Print final tallies. Uncomment this code to see the results
# printed instead of writing them to a file.
#
# for i in range(list_size_int):
#     print('Lemma: ' + table_list[i][0] +
#           '\tFrequency: ' + str(table_list[i][1]) +
#           '\tRange: ' + str(table_list[i][2]) +
#           '\tUDP: ' + str(table_list[i][3]))
```




\newpage
## Appendix 2.2: OMDb-fetch.py {#appendix-2.2 .unnumbered}

``` {#OMDb-fetch .python .numberLines}
#! /usr/bin/env python3
# -*- coding: utf-8 -*-

# import re
from sys import argv
import os
import glob
import omdb

# year = '1996'
script, year, id_start = argv

dirs = []
p = []


for name in glob.glob(
        '../OpenSubtitles2018_parsed/parsed/he/' + year + '/*/'):
    p.append(name)
# p = Path('../OpenSubtitles2018_parsed/parsed/he')
# p = list(p.glob('[198-199]*/*/*.xml'))

p = [os.path.basename(os.path.dirname(str(i))) for i in p]

for i in p:
    if i not in dirs:
        dirs.append(i)

for i in dirs:
    while len(i) < 7:
        dirs[dirs.index(i)] = '0' + i
        i = '0' + i

dirs.sort()

# for i in dirs:
#     print('tt' + i)

print('# ' + year + '\n' +
      'IMDb ID\tTitle\tYear\tLanguage(s)')


omdb.set_default('apikey', '906517b3')

for i in dirs:
    if id_start != '':
        if i > id_start:
            print('tt' + i + '\t', end="", flush=True)
            doc = omdb.imdbid('tt' + i)
            # if doc['language'] == 'Hebrew':
            print(doc['title'] + '\t' +
                  doc['year'] + '\t' +
                  doc['language'])
    else:
        print('tt' + i + '\t', end="", flush=True)
        doc = omdb.imdbid('tt' + i)
        # if doc['language'] == 'Hebrew':
        print(doc['title'] + '\t' +
              doc['year'] + '\t' +
              doc['language'])
```




\newpage
## Appendix 2.3: single_file_extract.py {#appendix-2.3 .unnumbered}

``` {#single_file_extract .python .numberLines}
#! /usr/bin/env python3
# -*- coding: utf-8 -*-

import shutil
import os

source = '../OpenSubtitles2018_parsed'
destination = './OpenSubtitles2018_parsed_single'

# Copy the directory tree into a new location
shutil.copytree(source, destination, ignore=shutil.ignore_patterns('*.*'))

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
