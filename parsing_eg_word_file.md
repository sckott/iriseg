install some packages


```r
install.packages(c("rmarkdown", "xml2"))
```

load them


```r
library("rmarkdown")
library("xml2")
```

Convert a word file to html


```r
rmarkdown::pandoc_convert("Language_History_Questionnaire.docx", output = "stuff.html")
```

Read it back in to R


```r
txt <- paste0(readLines("stuff.html"), collapse = "\n")
```

Take a peak at it


```r
cat(txt)
```

```
## <p><strong>Participant Code:</strong></p>
## <p>(1) (a) Are you a native speaker of English? Yes __ No __</p>
## <p>(b) If not, what is your first language? ______________________</p>
## <p>(2) At what age did you start to learn French? ______________________</p>
## <p>(3) For how many years have you studied French? ______________________</p>
## <p>(4) If you have completed your studies, how long ago was it that you studied French? _____________________________</p>
## <p>(5) Please indicate which levels of study you have completed:</p>
## <ol style="list-style-type: lower-alpha">
## <li><p>GCSE/O Level __ Grade:</p></li>
## <li><p>A level __ Grade:</p></li>
## <li><p>1<sup>st</sup> year of degree __</p></li>
## <li><p>2<sup>nd</sup> year of degree __</p></li>
## <li><p>3<sup>rd</sup> year of degree __</p></li>
## <li><p>4<sup>th</sup> year of degree __</p></li>
## <li><p>Degree __</p></li>
## <li><p>Other (please specify) __</p></li>
## </ol>
## <p>(6) Have you ever lived in France, and if so, for how long? ______________________</p>
## <p>(7) If you have completed your studies, how often do use French now?</p>
## <ol style="list-style-type: lower-alpha">
## <li><p>Never __</p></li>
## <li><p>Rarely (i.e. once a year) __</p></li>
## <li><p>Frequently __</p></li>
## </ol>
## <p>(8) (a) Have you studied any other languages? Yes __ No __</p>
## <p>(b) If yes, please state which language(s) ______________________</p>
## <p>(c) For how many years did you study it/them? ______________________</p>
## <p>(d) What level did you attain? ______________________</p>
## <p>(9) Please use the space below to add any additional comments that you think might be relevant for us._______________________________________________________________</p>
## <p>___________________________________________________________________________</p>
## <p>___________________________________________________________________________</p>
## <p>(10) Date of birth _______ Gender _______</p>
## <p><strong>Thank you very much for taking part in this study and for completing this questionnaire! </strong></p>
```

Read with `xml2` into an object that can then be sliced and diced by a researcher


```r
html <- xml2::read_html(txt)
html
```

```
## {xml_document}
## <html>
## [1] <body><p><strong>Participant Code:</strong></p>\n<p>(1) (a) Are you  ...
```

e.g., find all `li` elements


```r
xml2::xml_find_all(html, "//li")
```

```
## {xml_nodeset (11)}
##  [1] <li>\n  <p>GCSE/O Level __ Grade:</p>\n</li>
##  [2] <li>\n  <p>A level __ Grade:</p>\n</li>
##  [3] <li>\n  <p>1<sup>st</sup> year of degree __</p>\n</li>
##  [4] <li>\n  <p>2<sup>nd</sup> year of degree __</p>\n</li>
##  [5] <li>\n  <p>3<sup>rd</sup> year of degree __</p>\n</li>
##  [6] <li>\n  <p>4<sup>th</sup> year of degree __</p>\n</li>
##  [7] <li>\n  <p>Degree __</p>\n</li>
##  [8] <li>\n  <p>Other (please specify) __</p>\n</li>
##  [9] <li>\n  <p>Never __</p>\n</li>
## [10] <li>\n  <p>Rarely (i.e. once a year) __</p>\n</li>
## [11] <li>\n  <p>Frequently __</p>\n</li>
```
