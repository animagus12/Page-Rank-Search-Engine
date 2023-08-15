# Page-rank
Page rank exercise coursera Python for everybody

Python Search Spider, Page Rank Calculator, and Visualization Tool

Introducing a collection of software applications designed to simulate various functionalities of a search engine. These programs utilize an SQLITE3 database named 'spider.sqlite' to store their data. To restart the process, you can safely delete this file at any time.

To interact with and manipulate the databases, it is recommended to install the SQLite browser, which can be obtained from:

```
http://sqlitebrowser.org/
```


The primary purpose of this program is to crawl a website, capturing a sequence of web pages into the database while recording the relationships between them.

Note: Windows may encounter difficulties displaying UTF-8 characters in the console. To address this, you may need to execute the following command before running the code in each console window:

    chcp 65001

For further information, refer to: http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how

To initiate the program on a Mac, execute the following commands:
```
rm spider.sqlite
python3 spider.py
```

On Windows, use the following commands:
```
del spider.sqlite
spider.py
```

You will be prompted to input a web URL or press Enter. For example:
```
Enter web url or enter: http://www.dr-chuck.com/
['http://www.dr-chuck.com']
How many pages:2
1 http://www.dr-chuck.com/ 12
2 http://www.dr-chuck.com/csev-blog/ 57
How many pages:
```
You can specify the number of pages you want to retrieve. The program will pull these pages and populate the database. Subsequent executions will only crawl new pages, and upon restarting, the program will begin from a random non-crawled page, thus incrementally building the database.

```
Mac: python3 spider.py 
Win: spider.py
```

```
Enter web url or enter: http://www.dr-chuck.com/
['http://www.dr-chuck.com']
How many pages:3
3 http://www.dr-chuck.com/csev-blog 57
4 http://www.dr-chuck.com/dr-chuck/resume/speaking.htm 1
5 http://www.dr-chuck.com/dr-chuck/resume/index.htm 13
How many pages:
```

You can have multiple starting points in the same database - 
within the program these are called "webs".   The spider
chooses randomly amongst all non-visited links across all
the webs.

If you want to dump the contents of the spider.sqlite file, you can 
run spdump.py as follows:

```
Mac: python3 spdump.py 
Win: spdump.py
```
```
(5, None, 1.0, 3, u'http://www.dr-chuck.com/csev-blog')
(3, None, 1.0, 4, u'http://www.dr-chuck.com/dr-chuck/resume/speaking.htm')
(1, None, 1.0, 2, u'http://www.dr-chuck.com/csev-blog/')
(1, None, 1.0, 5, u'http://www.dr-chuck.com/dr-chuck/resume/index.htm')
4 rows.
```

This shows the number of incoming links, the old page rank, the new page
rank, the id of the page, and the url of the page.  The spdump.py program
only shows pages that have at least one incoming link to them.

After a few pages are present in the database, you can perform Page Rank calculations on the pages using the 'sprank.py' program. This program requires the number of Page Rank iterations you wish to run. For instance:
```
Mac: python3 sprank.py
Win: sprank.py
How many iterations: 2
1 0.546848992536
2 0.226714939664
[(1, 0.559), (2, 0.659), (3, 0.985), (4, 2.135), (5, 0.659)]
```

To view the updated Page Rank information, you can employ 'spdump.py' to dump the contents of the 'spider.sqlite' file.
```
Mac: python3 spdump.py 
Win: spdump.py
```
```
(5, 1.0, 0.985, 3, u'http://www.dr-chuck.com/csev-blog')
(3, 1.0, 2.135, 4, u'http://www.dr-chuck.com/dr-chuck/resume/speaking.htm')
(1, 1.0, 0.659, 2, u'http://www.dr-chuck.com/csev-blog/')
(1, 1.0, 0.659, 5, u'http://www.dr-chuck.com/dr-chuck/resume/index.htm')
4 rows.
```

You can run sprank.py as many times as you like and it will simply refine
the page rank the more times you run it.  You can even run sprank.py a few times
and then go spider a few more pages sith spider.py and then run sprank.py
to converge the page ranks.

If you want to restart the Page Rank calculations without re-spidering the 
web pages, you can use spreset.py

```
Mac: python3 spreset.py 
Win: spreset.py 
```
```
All pages set to a rank of 1.0
```

Additionally, for visualizing the top pages in terms of Page Rank, you can use 'spjson.py' to generate JSON output. This data can be visualized using the 'force.html' file in a web browser. It provides an interactive representation of nodes and links, allowing you to click and drag nodes, as well as double-click on a node to access its corresponding URL.

```
Mac: python3 spjson.py 
Win: spjson.py 
```

```
Creating JSON output on spider.js...
How many nodes? 30
Open force.html in a browser to view the visualization
```

These utilities collectively offer the ability to emulate a search engine's functions, calculate Page Ranks, and visualize web page relationships.