## Introduction
Simple script that extracts the notes from a presentation using the python-pptx module.

Uses the [python-pptx](https://python-pptx.readthedocs.io/en/latest/) module and in particular the section [Working with Notes Slides](https://python-pptx.readthedocs.io/en/latest/user/notes.html) 

Output - basic markdown text to stdout, including:
- One header per slide including the slide title 
- One subheader with the slide note contents
- Note:  Other slide contents not included

Note: This script uses `click` to process command line arguments. The only reason for using click is that I wanted to test / play with it.  Other methods can be used to process the arguments.   


## Basic Operation 
Default behavior - skip slides with no notes.  In the example below, slide #4 is not included in the output:
```
$ python extract-notes.py Presentation1.pptx --header "Test Presentation" 
Test Presentation
## [1/5] - Presentation Title 
### Note:
Note in Presentation title slide
Loren Ipsum

## [2/5] - Here is the second slide (first content slide)
### Note:
Note in second slide 
Below are some text bullets (ignored by the script):
Line 1
Line 2
Line 3

## [3/5] - Here is ...the third slide 
### Note:
Note in third slide – all for matting is ignored by the script.  
TODO: verify if it can be extracted from the presentation by python-pptx
Bold text
Underlined text
Bold and underlined text

Numbered list below (numbering also lost :-( )
Item 1
Item 2
Item 3
Item 4


## [5/5] - THIS IS … the fifth Slide
### Note:
A note in Slide 5
A boring rambling note...

Test Presentation: Found 4 slides with non-empty notes in Presentation1.pptx
```

## Options
**--header** - provide a simple text that will be added at the beginning and the end of the output. See examples elsewhere in the document.
**--print-all** -  flag that determines if (titles of) slides without notes are included in the output. See example below

### Using the `--print-all` option
Includes in the output the slides with no notes (slide #4 in the example):
```
$ python extract-notes.py Presentation1.pptx --header "Test Presentation" --print-all
Test Presentation
## [1/5] - Presentation Title 
### Note:
Note in Presentation title slide
Loren Ipsum

## [2/5] - Here is the second slide (first content slide)
### Note:
Note in second slide 
Below are some text bullets (ignored by the script):
Line 1
Line 2
Line 3

## [3/5] - Here is ...the third slide 
### Note:
Note in third slide – all for matting is ignored by the script.  
TODO: verify if it can be extracted from the presentation by python-pptx
Bold text
Underlined text
Bold and underlined text

Numbered list below (numbering also lost :-( )
Item 1
Item 2
Item 3
Item 4

## [4/5] - Believe it or Not, Fourth slide has no Notes

## [5/5] - THIS IS … the fifth Slide
### Note:
A note in Slide 5
A boring rambling note...

Test Presentation: Found 4 slides with non-empty notes in Presentation1.pptx
```