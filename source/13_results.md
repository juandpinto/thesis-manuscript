\newpage

# The CHVL: A vocabulary list of conversational Modern Hebrew

The Conversational Hebrew Vocabulary List in its entirety can be found as an electronic supplement to this thesis (in CSV format) or at the following GitHub repository: <https://github.com/juandpinto/opus-lemmas>. A sample of the first 1,000 words is included in Appendix 1.

For discussion purposes, a small sample of the first 20 words is here presented.

|\# |LEMMA   | FREQUENCY| RANGE|UDP                |
|--:|-------:|---------:|-----:|:------------------|
1   |הוא     |23446109  |43455|0.9480170255915042|
2   |ל       |5638813   |43448|0.9420130372643667|
3   |ה       |9850733   |43458|0.929266134661147  |
4   |ב       |4812778   |43450|0.9292364864789281|
5   |את      |6846782   |43426|0.9285176069174289|
6   |לא      |5272808   |43433|0.9145688112131216|
7   |ש       |3880654   |43439|0.9088900047303463|
8   |של      |3892328   |43445|0.9067041511201389|
9   |על      |1766990   |43430|0.9042865019832009|
10  |זה      |5118759   |43441|0.9015544612816044|
11  |מה      |2362419   |43403|0.8922532708182579|
12  |היה     |2579370   |43420|0.8909904417204713|
13  |מ       |1061614   |43411|0.88900672760779   |
14  |כול     |1325676   |43414|0.8860074112131449|
15  |ו       |1906717   |43429|0.8852706380348441|
16  |יש      |1069358   |43376|0.8770543442171884|
17  |עם      |839575    |43331|0.8668140051895192|
18  |אם      |861163    |43321|0.8654587702150129|
19  |ידע     |1202416   |43323|0.8586088803742931|
20  |אבל     |921757    |42963|0.8519038846130076|




## Organization




## Use


## Expansion


## Challenges and future direction


### Using original-language movies exclusively

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
