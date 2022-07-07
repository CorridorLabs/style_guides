# python_styleguide
A style guide on the basics of how we write Python code. This guide will be regularly updated. 

NL, 07/07/22
____________________________

### Meta: 
At Corridor Labs, it is [our understanding that we write codes for humans, not machines](https://afifsohaili.com/write-code-for-humans-not-for-machines/#writing-code-is-writing-so-pick-your-audience-right-hint-it-s-your-team-members). This is why it's useful to have a common style that is adhered to across all code written throughout the company. 

We want to achieve a bunch of things:
- *Readability across time*. Once years have gone by and we haven't checked in with our code, we want to be able to jump back in and easily understand what's going on, and not have to spend hours concentrating hard on what it may have been that we meant
- *Modularity within and across projects*. If we write good code once, we can reuse it later. This saves us time and money.
- *Accountability to clients and collaborators*. Many people know how to read code. Everyone makes mistakes or writes inefficient code that can be improved. We want to make it easy to spot either, for everyone.

### Python-specific:
- We use Python 3. While we want to strive to be using the newest version, for a given project it makes sense to stick with one version and not necessarily update it throughout the process. 
- When in doubt, and you want to write especially *stylish* code and you find a facet of your code that isn't referenced here, consider checking the [official Python style guide](www.pep8.org), 'PEP8', and follow their recommendations.
- However, we're not dogmatic about adhering to PEP8 style guide, and indeed find some of the recommendations not that useful, most importantly: an 80-character limit for a line. It's more important to have informative object names than for everything to fit within 80 lines. However, let's not use more than 120 characters in a line unless it's useful. 

## 1. script/file core components, or 'the overall of our file' 
### A. The front matter of our script/file
1. At the top of a .py file, we always want the name of the file. 
2. We then want one or two paragraphs on what this script/file/module does, keeping it as short and simple as possible, e.g.:
```
this script pulls in data for the @realDonaldTrump account from the Twitter API, extracts a few core quantities from it 
and writes it to our SQLite database, while logging events to logfiles at /mnt/logfiles/DDMMYYY_donaldmetrics.log
```
3. This will contain info on :
  - data inputs of the scripts
  - data outputs of the scripts
  - potential other things we really might want to know

4. If it makes sense, we also want to have a reference in the top to related files. You can indicate this using `see also:`
5. We then want a quick description of how we might use this script/file, e.g.:
```
USAGE: python3 myscript.py [--arg]
```
or 
```
USAGE: import myscript as my
```
6. Finally, we want to keep track of our update history. I know that we can also do this using our github commit history, but it helps to know what went on when we made significant changes to our file. We do this by adding initials, a date, and a super-short description of what was done on this major change. We add this below the last dated change, like so.
```
NL, 01/01/22 - added plotting functionality using seaborn
```

### B. Sections of our script/file
There are a bunch of sections that any script or file we write will contain. We want these sections to be indicated very clearly to the reader, and we also want them to be easily searchable using cmd/ctrl+f, allowing us to easily navigate to where we want to be. For this purpose, we indicate our core sections using a number of hash-symbols, and text in caps, like so: 
```
############
# IMPORTS
############
```
The core sections that each of our script should have are: 
- imports
- paths & constants
- init
- 'the thing' (this is perhaps an unconventional way of indicating the core body of a file/script, but it's fairly descriptive)

Besides that, there are other sections we may want to indicate, such as:
- exceptions (i.e. custom errors we define)
- CLI (if we're using `argparse` to allow the user of the script to pass arguments


## 2. Notes on how to *write*
1. Give objects names that are very descriptive, even if they are longer than they should perhaps ideally be. So, rather than using `dt`, we want our dataframe containing trump's tweets to be called `trump_tweets_df`. 
2. If using pandas, every pandas dataframe has to have the suffix `_df`. So, rather than calling the dataframe `trump_tweets`, we call it `trump_tweets_df`
3. Every function you write should have a docstring. This docstring should contain all function arguments, their type, and what that argument does
4. Try to always specify the data type of a function argument -- this saves us from bugs down the line
5. We want to try and write lean code if possible. If we can achieve a goal without importing pandas and numpy, but instead simply reading a file line-by-line, then we'll prefer the latter, as we can deploy it on a server with less cpu/memory (which will be cheaper)
6. Comments are great. While some advanced programmers feel that comments are only for those who can't write self-explanatory code, it's best to always assume that the person reading your code *doesn't* know what's going on. 
7. We write functions in lower-case, separated by an underscore, like so: `pull_tweets(account)`. 
8. We write constants in all-caps, like so: `DATA_PATH`
9. We write exceptions/errors in camel-case, starting with a capital letter, like so: `DataNotFoundError()`
10. We **never** write potentially sensitive information into a file commited to github, like an API key or a password. 
11. Empty lines are great. Readability is key. Empty lines within functions or loops are also great. Let the script breathe. 
