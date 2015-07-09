# DS Capstone Survival Guide

- [Prerequisites](#prerequisites)
- [Development environment](#development-environment)
- [Use of Unix command-line tools](#use-of-unix-command-line-tools)
- [Languages and libraries](#languages-and-libraries)
- [Common problems and troubleshooting](#common-problems-and-troubleshooting)
- [ShinyApps limits](#shinyapps-limits)
- [Time management and deadlines](#time-management-and-deadlines)
- [Slow or unreliable internet connections](#slow-or-unreliable-internet-connections)
- [Uploading to Rpubs issues](#uploading-to-rpubs-issues)
- [Useful resources](#useful-resources)
- [General remarks](#general-remarks)

## Prerequisites
*Some things you should know before you start.*

- While it is not required basic familiarity with Unix command-line tools can be extremly useful. If names like [`grep`](http://en.wikipedia.org/wiki/Grep), [`sed`](http://en.wikipedia.org/wiki/Sed) or [`wc`](http://en.wikipedia.org/wiki/Wc_%28Unix%29) doesn't mean anything to you it is a good idea to change that.
- You don't have to be an expert in [Natural Language Processing](http://en.wikipedia.org/wiki/Natural_language_processing) but understanding basic concepts and some experience with analyzing unstructured data will give you a serious advantage. If you're familiar with terms like [tokenization](http://en.wikipedia.org/wiki/Tokenization_%28lexical_analysis%29), [n-gram](http://en.wikipedia.org/wiki/N-gram) or [Markov chain](http://en.wikipedia.org/wiki/Markov_chain) you're good to go.
- You don't need a computer science degree to finish this course, but it is useful to understand basic data structures and algorithms. If you are familiar with [Big O notation](http://en.wikipedia.org/wiki/Big_O_notation) and you can analyze time and memory complexity of the operations like `for(i in 1:n) {foo <- c(i, foo)}` or `which(foo == round(runif(1, 1, n)))` you should be fine.
- While most of the heavy-lifting can be handled by Shiny some practical knowledge of the front-end technologies can make your life much easier.

## Development environment

- Keep your development environment as close as it is possible to the target platform. At this point shinyapps.io is using [Ubuntu 12.04](https://wiki.ubuntu.com/PrecisePangolin) with `en_US.UTF-8` locale. You can create similar environment using tools like [Docker](https://www.docker.com/), [Vagrant](https://www.vagrantup.com/) or [VirtualBox](http://virtualbox.org/).
- Create a reproducible R environment ([Packrat](https://rstudio.github.io/packrat/) is your friend) for your project. Dealing with broken dependencies is a painful and time-consuming process.
- If you execute memory/CPU intensive task try to avoid RStudio.
- As soon as possible build a Shiny test app and R-pres slides and publish them.
- Version-control your project by using a private repository (public ones are a no-no in the Capstone). They are very useful when you find that the new approach you try is como to a dead end.
- Test a lot. Test with different browsers and OS. Your app will be in the wild so test it with any input you can imagine.

## Use of Unix command-line tools
- Most operations involving identifying 'unique' words or n-grams, and counting them, can take hours in R and just a few seconds/minuts using Unix/Linux pipes.
- If you work on a Windows machine, keep in mind that you can use [Git Bash](https://msysgit.github.io/#bash) for Unix/Linux command-line tools.
- Using Linux/Unix does not mean you have to give up the ideals of reproducible research: the R function `system()` allows you to call OS commands; if you have a Windows machine, you can solve this problem by using cloud services such as [Domino](http://www.dominodatalab.com) which accept Linux/Unix commands.

## Languages and libraries

- Some libraries are more equal than others. Even if some library looks like a great fit it doesn't mean it can handle amount of data you have to process.
- JVM based libraries (RWeka, OpenNLP) can provide some very useful functions but it comes at a price. In a restricted environment like ShinyApps it can be a deal breaker.
- Some libraries which had beeen proven to be useful: [`stringi`](http://www.rexamine.com/resources/stringi/),  [Hadleyverse](http://adolfoalvarez.cl/the-hitchhikers-guide-to-the-hadleyverse/) tools ([`data.table`](http://cran.r-project.org/web/packages/data.table/index.html) in particular), [`hash`](http://cran.r-project.org/web/packages/hash/index.html).
- Most likely more trouble than it's worth: [`tm`](http://cran.r-project.org/web/packages/tm/index.html), [`RWeka`](http://cran.r-project.org/web/packages/RWeka/index.html). These are good packages but simply not well suited to Capstone specific workload.
- While you can use any tools you want to process input data and build your model the final project must be deployed on shinyapps.io. Running external code on ShinyApps is possible, but may violate [Terms of Use](http://www.rstudio.com/products/shiny-apps-terms-of-use/) and makes debugging even harder. Keep that in mind before you decide to use your-favorite-language.

## Common problems and troubleshooting

- If you don't know where to start or you are stuck be sure to check fora. To quote [@LaurentFranckx](https://github.com/LaurentFranckx) _they can make the difference between passing and failing_.
- If you ask a question regarding issues with your code, it is wise to provide the [SSCCE](http://sscce.org/) and all the additional information which can be useful (error messages, warnings, `sessionInfo`) to diagnose the problem. Describing [what have you tried](http://whathaveyoutried.com) is always welcome.
- Contrary to popular belief ShinyApps is not a devious trap created only to make your application fail but it is not a forgiving platform either. Even if your application works fine [on your own machine](http://jcooney.net/post/2007/02/01/New-Application-Certification-Program-It-Works-on-My-Machine.aspx) with lots of spare resources it doesn't mean it will behave in the same way after deployment. Take away message here is [deploy early and often](http://programmer.97things.oreilly.com/wiki/index.php/Deploy_Early_and_Often).
- If your problem concerns a deployed application be sure to provide [an application log](http://shiny.rstudio.com/articles/shinyapps.html#application-logging) and related errors visible in a browser console ([Firefox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Console), [Chrome](https://developer.chrome.com/devtools/docs/console)). You can use [logging](http://cran.r-project.org/web/packages/logging/index.html) package to create custom log messages.
- If you don't understand [R memory management](http://adv-r.had.co.nz/memory.html) you will most likely fail. You can use common monitoring tools, like [htop](http://en.wikipedia.org/wiki/Htop) or more advanced software like [Munin](http://munin-monitoring.org/) to monitor your application. If you see unexpected memory spikes use [lineprof](https://github.com/hadley/lineprof) to find the source of the problem.
- Keep shiny application directory clean. Uploading things like saved R workspace may have unexpected results.
- Double check submitted links especially if you use Rich Text Editor. What you see is not always what you get.
- [Locale](http://stat.ethz.ch/R-manual/R-devel/library/base/html/locales.html) matters. `en_US.UTF-8` is usually the best choice. If in doubt use `Sys.getlocale` and `Sys.setlocale`.
- Input file encoding matters as well. Be sure to understand how to use encoding parameter when you create [connections](https://stat.ethz.ch/R-manual/R-devel/library/base/html/connections.html) or use [`readLines`](https://stat.ethz.ch/R-manual/R-devel/library/base/html/readLines.html). If you still encounter problems (like embeded nulls) you can always [read and encode raw data](https://github.com/zero323/r-snippets/blob/master/R/read_and_reencode.R).
- [Handle exceptions](http://adv-r.had.co.nz/Exceptions-Debugging.html) and prepare fallback strategy. If there is an easy way to break your application you can be sure reviewers will find it.
- Deploying application on ShinyApps requires a current version of the `shinyapps` package. If you see `shinyapps package out of date` simply repeat [installation procedure](https://github.com/rstudio/shinyapps/#installation).
- Consider using `shiny::showReactLog` to track reactive dependencies.

## ShinyApps limits
- Manage shiny hours carefully. Archive any apps you don't need. Set the Instance Idle Timeout for a short period, particularly during your testing. Stop the app in the shiny console when you finish a testing session.
- Size of an application deployed using `deployApp` is limited to 1GB.
- _Free tier is restricted to [medium size](http://shiny.rstudio.com/articles/shinyapps.html#application-instances)_. In practice it means 512MB RAM at your disposal. Few orders of magnitude more than [the Apollo Guidance Computer](http://en.wikipedia.org/wiki/Apollo_Guidance_Computer) but most likely less than your smartphone. Use it wisely.
- Changes in a file system [won't persist beyond a single session](http://shiny.rstudio.com/articles/share-data.html).
- Considering ShinyApps architecture it is best to assume worst-case scenario, in which every user has to go through a whole starting process (including operations executed outside `shinyServer`) from scratch.

## Time management and deadlines

- Don't wait until the last moment to deploy your projects. If anything can go wrong, it will happened a day before deadline. Just ask anyone who finished this specialization.
- Grading weeks tend to be quite intensive and you have to be prepared to deal with some unexpected issues. Long story short don't leave town.
- Again, get started as early as possible. Unlike other previous courses in Data Science Specialization, Capstone is much more open-ended which requires more time to think, survey, trial and error. Even if you did pretty well on other 9 courses, it's still possible that you don't have a clue in the beginning.
- Plan for extra time for optimization issues. There's many items that your app would need for improvement: accuracy, performance, memory footprint, etc.


## Slow or unreliable internet connections

- If you have a slow internet connection redeploying your app can be a time-consuming process. Since your data most likely won't change as often as your code you can create a data only package, keep it on GitHub and let Shinyapps [handle dependencies](http://shiny.rstudio.com/articles/shinyapps.html#package-dependencies). If you're not sure how to do it take a look at `devtools::create`, `devtools::use_data` and `devtools::install_github`. Be sure to check [working with large files](https://help.github.com/articles/working-with-large-files/) guide.
- Seeing cryptic `Error in headers[["Content-Type"]] : subscript out of bounds` during deployment may suggest some kind of connection problem. If you're sure there is nothing wrong with your app please try again using different network.

## Uploading to Rpubs issues

People may get an SSL error when uploading to RPubs. This could be either needing to update software or your need configure your machine to use SSL uploads (normally through making an .RProfile file). Let's start with the update

-SSL error due to needing updates

A lot of SSL things have needed updating over the past year. If you are getting a SSL error when uploading to RPubs the first step is:

* Update RStudio to the latest version
* In the new version of RStudio, update the __bitops__ and __RCurl__ packages (the markdown package should update when you start using .Rmd documents, but if you are following an unusual path you may need to update the markdown package). Remember, the safe way to update is to unload the package (which you can do by taking the tick out of the box beside the package in the packages tab) then reinstall.
* in the new version, with bitops and RCurl loaded, try knitting and publishing to RPubs.

If still no luck, then (particularly if using Windows) you will need to use the command options(rpubs.upload.method = "internal") to have Internet Explorer handle the https transfer. if this works and you want to make the change permanent, put it in an .RProfie file.

To create a .Rprofile file can be a bit tricky as normally suffix files starting with a . are invisible on most computer systems. I suggest using RStudio, with the startup directory set to the folder with the .rmd file in it (Technically, R uses a multistage process of reading in settings and the help for Startup explains the other possible places)

* Use the File menu to make a New File -\> Text File
* Put in **options(rpubs.upload.method = "internal")** and no other text at all
* Use the Save command and save it with the name **.RProfile**
* Quit RStudio, restart RStudio, make sure your startup directory is set to the folder, then try to publish again. For other places the command could go see ?Startup

You can do the equivalent in Windows using the console (hat tip to Iman Tang for this tip) without actually creating the .Rprofile file.

```
install packages("markdown")  
library(markdown)  
rpubsUpload(title, htmlFile, id = NULL, properties = list(), method = getOption("rpubs.upload.method", "internal"))
```

_Please note that the last part is also ("rpubs.upload.method", "internal") as others have mentioned._

_This "rpubsUpload" function returns a "continueURL". A browser can then be used to open this "continueURL" and finish up the publishing in RPubs. For details, please type "Upload an HTML file to RPubs" in the help section of Rstudio._

## General remarks
- Be civil and try to have fun.
- Word clouds are evil and therefore should be forbidden.
- Using typical NLP pipelines (tokenization -> punctuation removal -> stop words removal -> stemming) is not the best approach. It will bite you sooner or later.
- Carefully review the Grading Rubrics.
- Document and explain your design choices and never assume that the reviewers are familiar with some proprietary product _x_.
- Don't hesitate to ask questions or look for feedback in the discussion forum of the course, you will find how helpful your classmates and community TA are.

## Useful resources

- Discussion lists and QA sites.
  * [ShinyApps Users Group](https://groups.google.com/forum/#!forum/shinyapps-users) - A great place to ask a question about the ShinyApps platform.
  * [Shiny Users Group](https://groups.google.com/forum/#!forum/shiny-discuss).
  * [Stack Overflow](http://stackoverflow.com/).
- Books
  * [Data Science at the Command Line](http://shop.oreilly.com/product/0636920032823.do).
  * [Advanced R](http://adv-r.had.co.nz/)
- MOOCs
 * [Natural Language Processing, Columbia University](https://www.coursera.org/course/nlangp).
 * [The Analytics Edge,  MITx](https://www.edx.org/course/analytics-edge-mitx-15-071x-0) - Unit 5: Text Analytics in particular.
 * [Text Retrieval and Search Engines, University of Illinois at Urbana-Champaign](https://www.coursera.org/course/textretrieval).
 * [Text Mining and Analytics, University of Illinois at Urbana-Champaign](https://www.coursera.org/course/textanalytics).
 * [Introduction to Linux, LinuxFoundationX](https://www.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-2).
- Other
 * [awesome-R](https://github.com/qinwf/awesome-R) - a curated list of awesome R frameworks, packages and software.
 * [How to make a great R reproducible example?](http://stackoverflow.com/questions/5963269/how-to-make-a-great-r-reproducible-example)
 * [Next word prediction benchmark](https://github.com/jan-san/dsci-benchmark).
 * [Bitbucket](https://bitbucket.org/) - unlimited private Git repositories.
 * [Shinyapps.io Scaling and Performance Tuning](http://shiny.rstudio.com/articles/scaling-and-tuning.html) - should give required knowledge about ShinyApps architecture.
 * [w3schools](http://www.w3schools.com/) - enough HTML/CSS/JavaScript to keep you going.
 * [Software development skills for data scientists](http://treycausey.com/software_dev_skills.html)

---
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">DS Capstone Survival Guide</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/ds-capstone-survival-guide/ds-capstone-survival-guide" property="cc:attributionName" rel="cc:attributionURL">Maciej Szymkiewicz and Authors </a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
