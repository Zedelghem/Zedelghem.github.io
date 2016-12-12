---
title: Bash / shell one-liner for macOS to list page count of PDF files in a directory
updated: 2016-12-12 19:35
---
I found this pipeline on StackOverflow, added a variable, put into /usr/locale/bin on a Mac and lo, behold.

```
#!/bin/bash
mdls -name kMDItemFSName -name kMDItemNumberOfPages ./$1/*.pdf | cut -d= -f 2 | paste - -
```

Super useful in estimating the number of pages to be printed from multiple files. All you need to do is call the script with a directory name as an argument, eg.:

```
$ pdf-count desktop/my_pdfs
```

When called without an argument, it works on the current directory. The output is in the '"File name"   page_count' format.

If you want even less effort involved, you can use the following script to extract just the number of pages from the files in a directory and sum them up using awk.

```
#!/bin/bash
mdls -name kMDItemNumberOfPages ./$1/*.pdf | cut -d= -f 2 | awk '{s+=$1} END {print s}'
```

Here the output is an integer.
