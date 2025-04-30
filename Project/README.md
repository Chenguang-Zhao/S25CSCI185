<!-- 
# Try It

Try the puzzles online in a Jupyter Notebook. No installs needed. 

Click here:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dfinke/Tiny-PowerShell-Projects/master)

-->
# CSCI-185-A PowerShell Projects
This project requires you to understand a problem from one chapter, analyze the provided solutions, and implement an alternative solution approach.

This code repository is adopted from [Tiny-PowerShell-Projects](https://github.com/dfinke/Tiny-PowerShell-Projects).

## Groups
A group can have 1-2 students.
Individual students can choose a problem from Chapters 2-11.
Groups of Two can choose a problem from Chapters 12-22.
## Deliverables 
Submit a team-written report to BB, which includes
1. Problem statement and analysis
2. Review of provided solutions
3. Implementation of your alternative solution and testing.
4. Screenshot the differences between the provided solution and your solution using https://text-compare.com/. Change justification.

Due @ 5-May 2025

## Rubric of Deliverable
## Deliverable Requirements

### 1. Problem Statement and Analysis (20 points)
| Criteria | Excellent (18-20) | Satisfactory (15-18) | Needs Improvement (0-14) |
|----------|-------------------|----------------------|--------------------------|
| Problem clarity | Problem is described with exceptional clarity, including inputs, outputs, constraints, and edge cases | Problem is adequately described but may be missing some details | Problem description is unclear or significantly incomplete |
| Technical Analysis | Thorough explanation of the technical context of PowerShell and relevance of the problem | Basic explanation of technical context provided | Little or no explanation of technical context |


### 2. Review of Provided Solutions (20 points)
| Criteria | Excellent (18-20) | Satisfactory (15-18) | Needs Improvement (0-14) |
|----------|-------------------|----------------------|--------------------------|
| PowerShell specifics | Detailed discussion of PowerShell-specific features utilized in solutions and how the provided code works | Basic discussion of PowerShell features and code functionality | Limited or no discussion of PowerShell features and code functionality |

### 3. Implementation of Alternative Solution (30 points)
| Criteria | Excellent (24-30) | Satisfactory (18-23) | Needs Improvement (0-17) |
|----------|-------------------|----------------------|--------------------------|
| Code quality | Code is well-structured, efficient, and follows PowerShell best practices | Code works but has minor structural or efficiency issues | Code has significant issues or doesn't work properly |
| Test-driven development | Implementation passes all the original tests provided in the repository | Implementation passes most tests with minor issues | Implementation fails multiple tests |

### 4. Solution Comparison using text-compare.com (20 points)
| Criteria | Excellent (16-20) | Satisfactory (12-15) | Needs Improvement (0-11) |
|----------|-------------------|----------------------|--------------------------|
| Screenshot quality | Clear, properly formatted screenshots showing text-compare.com differences | Readable screenshots showing differences | Unclear or incomplete screenshots |
| Change justification | Thorough justification for each significant change made in the alternative solution | Basic justification for changes | Limited or missing justification for changes |
| Improvement discussion | Insightful discussion of how differences represent improvements | Some discussion of improvements | Limited or no discussion of improvements |

### Overall Presentation Quality (10 points)
| Criteria | Excellent (8-10) | Satisfactory (6-7) | Needs Improvement (0-5) |
|----------|-------------------|----------------------|--------------------------|
| Visual clarity | Report uses consistent formatting, appropriate headings, and clear visual organization | Report is visually organized but has minor inconsistencies | Report lacks visual structure and organization |
| Content organization | Content flows logically with smooth transitions between sections | Content generally flows well with some awkward transitions | Content organization inhibits understanding with abrupt or missing transitions |
| Effective use of visuals | Screenshots, code samples, and other visual elements are well-integrated and enhance understanding | Visual elements are present but could be better integrated | Few or poorly implemented visual elements that don't enhance understanding |


## Project Discussion and Contribution

Original author ported it from the Manning Publications book, _Tiny Python Projects_, by Ken Youens-Clark:

- The Python repo is here: https://github.com/kyclark/tiny_python_projects
- The Python book is here: https://www.manning.com/books/tiny-python-projects?a_aid=youens&a_bid=b6485d52

One of the many cool aspects of this not only the approach to learning `PowerShell` this way, additionally, you can head over to the `Python` repo and see how it is done in that language. Could be you are here because you're a Pythonista, and want to see how PoShers do it.

Either way, it's the same puzzles implemented in both languages, and you can use the tests provided, to do Test Driven Development and prove these and your solutions work, as you make changes.

The Video: [Scripting Success A Deep Dive into Tiny PowerShell Projects]("https://youtu.be/BVDBRty5mCU?si=Pw_uSJSnAhQZKHqz&t=443").


## The approach

There is a directory for each chapter of the book.
There is a README to describe each exercise.
Each directory contains a `test.ps1` program you can use with `Invoke-Pester` to check that you have written the program correctly.

In addition, each directory has two `PowerShell` scripts, one called `AllTest.ps1`, and the other `solution1.ps1`.

## AllTest

`AllTest.ps1` does something very _beneficial_. It looks in that chapters directory for all files that match the wildcard `solution*.ps1`, and one by one copies it to a `ps1` that is expected in the `test.ps1`, and the last step, it calls `Invoke-Pester`.

This allows you to keep the original solution supplied, and you can then create as many solutions as you'd like to test different ways to solve the puzzle. This lets you experiment with different ways to use a regex, arrays, hash tables or other approaches, in order to figure out better ways to handle this. The different solutions can sit side by side with the others and the `test.ps1` can be automatically run against all. 

## Testing is Integral
The testing step is integral to writing and solving these challenges.

Using a "test-driven development" mentality, where you write tests _before_ you write code, is very much recommended.

The tests should define what it means for a program to be correct, and then you write programs to satisfy the tests.

All the tests have been written for you, and you should write your own functions and tests.
Practice is key.

You should run the test suite after every change to your program to ensure you are making progress!

## Chapters

* [Chapter 1: How to write and test a PowerShell program](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/01_hello) How to create a PowerShell program that prints a string and takes a parameter. [[source code]](./01_hello/hello.ps1)

* [Chapter 2: Crow's Nest](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/02_crowsnest) How to write a PowerShell program that accepts a single, positional argument and creates a newly formatted output string. [[source code]](./02_crowsnest/crowsnest.ps1)

* [Chapter 3: Picnic](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/03_picnic) Writing a PowerShell program that accepts multiple string arguments and formats the results depending on the number of items. [[source code]](./03_picnic/picnic.ps1)

* [Chapter 4: Jump The Five](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/04_jump_the_five) Writing a PowerShell program to encode the numerals in a given text using an algorithm called "Jump The Five." Use of a dictionary as a lookup table, characters not in the dictionary remain unchanged. Introduction to encoding/decoding text, basic idea of encryption. [[source code]](./04_jump_the_five/jump.ps1) 

* [Chapter 5: Howler](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/05_howler) Writing a PowerShell program that can process input text either from the command line or from a file.The output prints either to STDOUT or to a file.  Learning about how to read/write the contents of a file. [[source code]](./05_howler/howler.ps1)

* [Chapter 6: Word Count](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/06_wc) Writing a PowerShell program to emulate a word count program. Validates and processes multiple file inputs as well as STDIN and creates output of the counts of lines, words, and characters for each file. [[source code]](./06_wc/wc.ps1)

* [Chapter 7: Gashlycrumb](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/07_gashlycrumb) Writing a PowerShell program that processes an input file to build a lookup table (dictionary) that is used with multiple positional arguments to translate to the values from the file. [[source code]](./07_gashlycrumb/gashlycrumb.ps1)

* [Chapter 8: Apples and Bananas](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/08_apples_and_bananas) Writing a PowerShell program to find and replace elements in a string.  [[source code]](./08_apples_and_bananas/apples.ps1)

* [Chapter 9: Abuse](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/09_abuse) Writing a PowerShell program to generate Shakespearean insults by randomly combining some number of adjectives with a randomly chosen noun. Learning about randomness, seeds, and testing. [[source code]](./09_abuse/abuse.ps1)

* [Chapter 10: Telephone](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/10_telephone) Using probabilistic and deterministic approaches to randomly mutate a string. [[source code]](./10_telephone/telephone.ps1)

* [Chapter 11: Bottles of Beer](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/11_bottles_of_beer
) Writing a PowerShell program to produce the verse to the "99 Bottles of Beer" song from a given starting point. Learning to count down, format strings, algorithm design. A focus on writing a function and unit test, exploring ways to incorporate our function to generate the verses from for loops. [[source code]](./11_bottles_of_beer/bottles.ps1)

* [Chapter 12: Ransom](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/12_ransom) Writing a PowerShell program that will randomly capitalize letters in a given piece of text for the nefarious purpose of creating a ransom note. [[source code]](./12_ransom/ransom.ps1)

* [Chapter 13: Twelve Days of Christmas](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/13_twelve_days) Writing a PowerShell program to create the verses for "The Twelve Days of Christmas" from a given day. Learning how to write a function and the test for it, then using the function in a list to generate the output. [[source code]](./13_twelve_days/twelve_days.ps1)

* [Chapter 14: The Rhymer](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/14_rhymer) Writing a PowerShell program that can split off any initial consonants from a word and append a list of prefixes to create new rhyming "words." Exploration of regular expressions to handle words with no initial consonants, with one or more leading consonants, and nothing but consonants. [[source code]](./14_rhymer/rhymer.ps1)

* [Chapter 15: The Kentucky Friar](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/15_kentucky_friar) In this chapter we delve further into regular expressions, first learning how to split a string using a regex so we can separate things that look like "words" from non-words like punctuation and whitespace. Then we try to identify the word "you" (case-insensitive) to turn into "y'all" and any 2-syllable words ending in "-ing" so we can replace the final "g" with an apostrophe so that "cooking" becomes "cookin'" but "swing" would remain "swing." We then apply this to an entire body of text to Kentucky fry the words with amusing results. [[source code]](./15_kentucky_friar/friar.ps1)

* [Chapter 16: The Scrambler](https://github.com/dfinke/Tiny-PowerShell-Projects/tree/master/16_scrambler) Writing a PowerShell program to find each "word" in a body of text and then scramble the letters such that the first and last letters remain in place, then reconstructing the text for output. Using regular expressions to split text, using `Sort-Object { Get-Random }`. [[source code]](./16_scrambler/scrambler.ps1)
* 
## Acknowledgments
This project is derived from the original [Tiny-PowerShell-Projects](https://github.com/dfinke/Tiny-PowerShell-Projects) and builds upon its foundation to provide a comprehensive learning experience for PowerShell scripting.

