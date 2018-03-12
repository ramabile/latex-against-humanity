# LaTeX Against Humanity

<p align="center"><img src="example/example_180312.png?raw=true" alt="latex cards against humanity table example"></p>

```
Give as a pretext your misanthropic friends
to enjoy a cathartic night with your own deviltry!
```

*LaTeX Against Humanity* is a *LaTeX* (*pdfLaTeX*-compiled) version of [**Cards Against Humanity**](https://www.cardsagainsthumanity.com/), a popular card game who has been attracting very polarized critics (either you love it or you hate it). This version provides the basics to make the ready-to-print document of your own game in three moves: download, write your own cards, compile it in one line. No crap.

## Quick Start
A very short workflow for lazy people like you.
The procedure is based on command-line interface and tested for GNU/Linux platform. Ask your favourite geeky friend if you don't get the fuck about what I am talking about before you proceed.
* Download the archive with the button *Clone or download* or clone the git
```
git clone https://github.com/ramabile/latex-against-humanity
```
* Create your own cards in *questions.csv* and *answers.csv* in the same folder (see **Deck**);
* Compile the document with the following command:
```
pdflatex against-humanity.tex
```

## Rationale

There exist different online versions of Cards Against Humanity. However, the most popular (according to the search engine) versions are falsely claimed to be editable, whereas actually it is a pain in the ass to modify them. The choice of LaTeX was natural to me since I use it on every day basis and - most importantly - automatically takes care of the layout ([WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG#Related_acronyms) philosophy).
You can find several attempts on the web. I found the Italian LaTeX version by [ilario](https://github.com/ilario) most fitting my needs, yet some design choice led me to make a new tex document.
I expressely thanks ilario since I was inspired by his works to put my version on github.

## Design

The main design choice is to separate the LaTeX code from the cards itself. This decision improves readability and maintainability. The intention is that even a LaTeX total newcomer can understand how to make its own version of the game.
The deck of cards is written in a comma-separated value (*csv*) file that is fed to the main tex file.

### Deck (*csv*)
The deck itself is written in a *csv* file. You can automate the creation of your deck with your favourite spreadsheet program (I suggest *LibreOffice Calc*), but even a plain text editor is fine.
The one-line header of your deck file sets the field keyword where you draw your options. Your file must start with *QA,Picture,TEXT* as first line.
* *QA*: a 0/1 question/answer switch. If 0, the card is a question (*"black"*) card. If it is 1, the card is an answer (*"white"*) card. Any other value raises an error.
* *Picture*: picture filename to be included in the card. If you don't want to include a picture, write *None* in the Picture field. Pictures are allowed only for black cards. White cards ignore the third field.
* *Text*: any simple text *but* the special character separator (see further). The text is output to your card and will be printed. If you want to insert blank spaces (*e.g.* for black cards), write *\underscores* in the Text field.
By design, questions and answers are given separately. Save the file *questions.csv* and *answer.csv* in the same directory of the tex file.

### Main (*tex*)
You are not intended to modify the main tex file. In principle, you can blindly use it. For advanced users, I explain here its structure.
* The layout of the cards is based on the 
[*ticket*](https://ctan.org/pkg/ticket) package. A floating box is used for the text inside the card. The logo *Cards Against Humanity* is added at the footer of each card. The background of the cards is changed to either black or white if the card is a question or an answer, respectively. The question cards take an additional argument as picture ("Picture") according to the name in the csv file. These pictures (even the "None" picture) should have the same background color as the question card.
The layout is encoded as a newcommand as if it were a "function" that gets the QA switch, the text, and the picture of the card (in this respective order), and returns the card itself.
* Each record of the csv file is fed to the card function to generate each card. The loop is done via the [*datatool*](https://ctan.org/pkg/datatool) package and runs until the end of the csv file. To compile the tex file, it is detrimental that the very first line of the csv file matches the field keyword in the text file, and there are *exactly* two separators per record.

### Advanced/Miscellanea
* By default, the comma-separated value files are unsurprisingly separated by commas. The default behaviour is somehow annoying since one'd want to add commas in their cards.
To edit this behaviour, you need to change your separating commas to a different character (_e.g._ the much-criticized/maligned/berated semicolons **";"**) in each of your csv file (don't forget the headers! *e.g.* if you like semicolons: *QA;Picture;Text*) and then add `\DTLsetseparator{;}` to your LaTeX code before `\DTLloaddb`. Spreadsheet programs can help you to add different separators between cells (LibreOffice asks which one when you save a spreadsheet in a csv file).
* Dimensions can be customize according to the number of cards you want per page and their size. Note that horizontal and vertical distances from the borders, as well as textwidth of text box inside the card, should be set manually if any of the page sizes are changed. An automatic tuning is To Be Implemented.

## Closing remarks

### Deployment / Built With / Contributing / Versioning
To Be Implemented.

### Improvements
* Picture background transparency. If picture is *None*, do not print a picture at all.
* Automatically choose either *draw* or *pick* according to the number of blank spaces in the black cards. The solution allows for third argument as optional pictures in the card. The only limit is your imagination.
* *\hoffset* and *\voffset* distances from the border of tickets set automatically.
* *\parbox* width of ticket text set automatically.

### Author
* **Roberto Amabile** \[[ramabile](https://github.com/ramabile/)\] - *Main-levolent contributor*.

### Acknowledgments
* [Cards Against Humanity](https://www.cardsagainsthumanity.com/)
* **Ilario Gelmetti** \[[ilario](https://github.com/ilario)\] for the [inspiration](https://github.com/ilario/Cards-Against-Humanity-ITA) and part of the underscore solution in the *tex* file.
* **Donald Kuhn**, TeX, its community.
* **Leslie Lamport**, LaTeX, its community.
* GNU/Linux and the FLOSS community in its broadest sense.
* Creative Commons and the free art community in its broadest sense.
* The other authors of packages and programs I use.
* **Billie Thompson** \[[PurpleBooth](https://github.com/PurpleBooth)\] and other contributors for [the template of this README.md](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2#file-readme-template-md).
* **Michael Mroczek** \[[michaelmroczek](https://unsplash.com/@michaelmroczek)\] for the [photo of the table](https://unsplash.com/photos/xVKEZ9wVIYM?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText).
* What the fuck.
* My long-running misantropic friends.
* The maieutics.
* The scientific materialism.
* Bernard Mandeville is dead. Long life to zombie Mandeville.
* The auto-hetero-directed troll inside me, getting out of my hands.

### Licensing
This work is licensed under [WTFNMFPL-1.0](http://www.adversary.org/wp/2013/10/14/do-what-the-fuck-you-want-but-its-not-my-fault/). Full text of the licence can be found also [here](https://github.com/ramabile/latex-against-humanity/blob/master/LICENSE.txt). If you are illiterate [there is a summary with colorful symbols](https://tldrlegal.com/license/do-what-the-fuck-you-want-to-but-it%27s-not-my-fault-public-license-v1-(wtfnmfpl-1.0)).
Logo of Cards Against Humanity and its related concepts are [Creative Commons BY-NC-SA 2.0 license](https://creativecommons.org/licenses/by-nc-sa/2.0/). That means you can use, remix, and share the game for free, but you can't sell it without their permission. Please do not steal their name or they will smash you.
