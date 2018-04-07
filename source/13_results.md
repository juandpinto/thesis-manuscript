\newpage

# The CHVL: A vocabulary list of conversational Modern Hebrew

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
