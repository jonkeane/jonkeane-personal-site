---
title: Software
weight: 2
---

Some interesting and hopefully helpful tools for others — mostly from my academic days


### MocapGrip

[MocapGrip](https://github.com/jonkeane/mocapGrip) is a complete data processing and analysis pipeline R package. MocapGrip contains a full pipeline for motion capture data collection, from initial data processing to statistical modelling and report generation. The package includes functions to check human annotated data for consistency and errors, as well as a flexible analysis and reporting system for use by novice users.

This was my first large-scale foray into building a stand-alone R package. For a number of reasons, I adopted a test-drive development approach to this package. Being test driven allowed me to better address (and ensure that I was reliable in addressing) data validation as well as providing feedback to users when there were errors was consistent and accurate. As the project grew, the number of possible edge-case errors exploded. Testing each one manually was unsustainable and error-prone. Whereas, using unit (and integration) tests through the [testthat package](https://github.com/hadley/testthat) being constantly run using [travis {{< smallcaps ci >}}](https://travis-ci.com).

### Pyelan

I've developed [pyelan](https://github.com/jonkeane/pyelan), a python module that allows for eas[y | ier] extraction and manipulation of annotation data from [elan](http://www.lat-mpi.eu/tools/elan/) files. Although this is a work in progress, some core functionality has been implemented. Pyelan can read, write, and preform some manipulations of eaf files. Pyelan now also allows for linking csv files to be viewed in the timeseries viewer. Please feel free to use, fork, submit issues, and submit pull requests.

### The Articulatory Model of Handshape {#amohs}

For my dissertation, I implemented a computational model of the phonetics-phonology interface, that I call the Articulatory Model of Handshape. The implementation is as the [amohs](https://github.com/jonkeane/amohs) python module. This module not only implements automatic translation from phonological features to various types of phonetic representations (including joint angle targets), but it also uses an external library to render {{< smallcaps 3d >}} images of hands.

The Articulatory Model of Handshape uses a slightly modified version of <a class="cite" href="https://scholar.google.com/scholar?q=%22A+Prosodic+Model+of+Sign+Language+Phonology%22" title="D. Brentari. A Prosodic Model of Sign Language Phonology. The MIT Press, 1998.">Brentari's 1998</a> Prosodic Model of handshape for a phonological representation of handshape. It than provides representations for phonetic specifications either as tract variables (at a categorical level), and as phonetic joint angle targets (a continuous level) for handshapes. Using these representations, comparisons between handshapes can be made deriving a theory-driven metric of handshape similarity.

On top of the computational implementation described above, the module uses an external library, [LibHand](http://www.libhand.org/) to render images of synthesized handshapes. Currently, the model only renders isolated handshapes, but in the future could be extended to sequences of handshapes (including transitions), that is, video of handshapes moving over time. Because they are based on representations that can be linked to multiple levels of phonetics and phonology, these videos could include information about coarticulation (contextual dependencies) of the kind that was demonstrated in my dissertation.

At the time that I was trying, [LibHand](http://www.libhand.org/) failed to compile on modern versions of OS X. I help maintain [a repository](https://github.com/libhand/libhand) that includes the changes needed to compile LibHand on modern linux, OS X, and windows systems. Compiling via [homebrew](http://brew.sh/) is possible, with some [alterations](https://github.com/jonkeane/homebrew-libhand) to ogre as well.

### SLGloss LaTeX package

In collaboration with [Itamar Kastner](https://files.nyu.edu/ik747/public/), I've helped developed [the SLGloss LaTeX package](https://github.com/itamarkast/slgloss) to make it easier to typeset sign language glosses. It has three main features:
<ol>
  <li> It typesets sign glosses in smallcaps to integrate typographically with surrounding text, as well as allows for non-manual markings over specific constituents.</li>
  <li> It typesets fingerspelled words in small caps with hyphens between the letters</li>
  <li>It typesets lists of individual fingerspelled letters with hyphens on either side.</li>
  </ol>

### Fflipper

I've developed [fflipper](https://github.com/jonkeane/fflipper), a python module that allows for extraction of clipped videos based on the annotations extracted from an [elan](http://www.lat-mpi.eu/tools/elan/) file.

### {{< smallcaps asl >}} fingerspelling chart

<img src="images/Asl_alphabet_gallaudet.jpg" alt="Chart of ASL fingerspelling handshapes" />

After seeing many charts that were licensed and reproduced with permission, I decided to recreate a fingerspelling chart and release it using a very liberal content license so researchers and educators that need this chart can use it (nearly) freely. The handshapes are based on the font from David Rakowski.

There a few problems with this chart. The biggest problem is that the orientation of many letters is altered to show the configuration of the fingers. In reality, all of the handshapes are made with the palming facing out, away from the signer with the exception of {{< smallcaps -g- >}} (in, towards the signer), {{< smallcaps -h- >}} (in, towards the signer), {{< smallcaps -p- >}} (down), {{< smallcaps -q- >}} (down) and the end of {{< smallcaps -j- >}} (to the side)

Download the [full sized, completely vector-based {{< smallcaps pdf >}} version](Asl_alphabet_gallaudet.pdf).

<a rel="license" href="https://creativecommons.org/licenses/by-sa/3.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><p>This work is licensed under a <a rel="license" href="https://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.


### Better type for LaTeX

In the pursuit of better typography for LaTeX I've found a couple of good walkthroughs, and a couple of invaluable tools. All of the following have been tested on TeX Live 2009, 2010, and 2011 on both OS X 10.5, 10.6, and 10.7. 

#### Minion Pro
I've created [a bash script](https://github.com/jonkeane/MinionProforLaTeX) that installs Minion Pro to a local TeX Live tree with very little user intervention.

#### otfinst.py

John Owens has developed [a great python tool](http://www.ece.ucdavis.edu/~jowens/code/otfinst/) that installs many OpenType fonts. The only stumbling block I found besides some font incompatibilities was assigning (making up) [Berry names](http://www.tex.ac.uk/tex-archive/info/fontname/fontname.pdf) to the fonts that I wanted to install, which have to be added to the script. I have made up names for the following that seem to adhere most of the conventions. If anyone knows of more widespread names for these typefaces, please [let me know](mailto:jonkeane@uchicago.edu).

<ul>
  <li>'Neutraface Text' : 'fne'</li>
  <li>'Neutraface Display' : 'fn3'</li>
  <li>'Gotham' : 'fg7'</li>
  <li>'Gotham Rounded' : 'fg8'</li>
</ul>