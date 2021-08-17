# OpenITIdiffViewer

Link: https://pverkind.github.io/OpenITIdiffViewer/

This app displays the differences between two strings of characters.
Contrary to most other diff viewers, it is geared towards comparing texts
rather than code, especially texts from the [OpenITI corpus](https://github.com/OpenITI)
and text reuse date created by [passim](https://github.com/dasmiq/passim) for the
[KITAB project](https://kitab-project.org).

The diff viewer leverages the [wikEd diff library](https://en.wikipedia.org/wiki/User:Cacycle/diff)
developed for Wikipedia (javascript code [here](https://en.wikipedia.org/wiki/User:Cacycle/diff.js)).
This library does not only detect text that was added or deleted, but also
text that was moved from one place to another.

The OpenITIdiffViewer modifies the output from the wikEd tool in two ways:

* the wikEd tool displays the differences between two texts in one
  composite text rather than side-by-side.
  
  ![wikEd: inline display](img/sample_text_wikEd.png)
  
  The OpenITI diff viewer analyses the output of the wikEd tool and displays the
  result side by side:
  
  ![OpenITIdiffViewer: side-by-side display](img/sample_text_side_by_side.png)

* the wikEd tool seems to have difficulties with Arabic's prefixes
(for example, if text A has *wa-faʿala* and text B *fa-faʿala*, both words would be
marked as different). The OpenITIdiffViewer adds a refining step of the wikEd
output to deal with this issue (in the example above, only *wa-* and *fa-* would
be marked).

## Usage

There are two basic ways to use the diff viewer:

* You can paste two texts to compare into the two text fields,
and click the "Display diff" button
(if you don't have two texts ready, you can also load an example by clicking
the "example" link in the header);

* Alternatively, you can click the "Upload from file" button to upload a passim
output tsv file.
  - This will open a popup with a button that allows you to select
a tsv file from your own computer.
  - Once loaded (this may take a while for large files), you can select the rows
  you want to display.
  - You can use a search filter to select rows: e.g., writing "كتاب" in the
  filter field and hitting the Enter key will filter out only rows in which at
  least one of the texts contain the word "kitāb". The filter accepts regular
  expressions: typing كتا?ب will select rows that contain either *kitāb*
  or *kutub/kataba/...* . You can also filter on milestone ids (e.g., "ms1\d\d"
  will select only milestones between 100 and 199).
  - Once you have selected the rows you are interested in, click the
  "Load selected rows" button to display the diff for each row.

## options

Click the "Options" button to view the options:

* by default, all OpenITI tags and punctuation are removed from the input texts,
since they don't belong to the original texts; you can uncheck the OpenITI tags
and punctuation checkboxes if you don't want to remove these.
* by default, Arabic text is normalized to some extent:
  - alifs with and without hamza / madda
  - alif maqṣūra and final yā'
  - tā marbūṭa and final hā'
* the wikEd output is refined by Heckel's algorithm (Paul Heckel, "A Technique
for Isolating Differences Between Files", Programming Techniques 21/4, 1978),
using shingled character n-grams (that is, breaking down the string into
overlapping sequences of "n" characters; e.g., the string "this is an example"
can be broken down into the following shingled character 10-grams: "this is an",
"his is an ", "is is an e", "s is an ex", " is an exa", "is an exam", "s an examp",
" an exampl", "an example"). By default, trigrams are used, but the user can
change the size of the n-grams.
* to make the output more easily readable, the string can be broken down into
lines, each of which starts with text that both input texts have in common.
You can decide the minimum number of shared characters to be displayed on each line
before splitting the text (the default is 20).
* the inline wikEd output optionally can be displayed below the side-by-side view.

The options can be reset to their defaults by clicking the "Reset options" button.

## resizing the output and downloading

You can resize the width of the output table by grabbing and dragging the
right-side border of the table.

The font size can be changed by clicking the "Options" button.

Once you are happy with the size of the table and the font, you can download the
output as a png image (most useful for use in printed documents) or as an svg
image (most useful for online publication, as it allows unlimited zooming) using
the "Download png" and "Download svg" buttons.

If you uploaded multiple text pairs using the tsv upload function, you can
download png or svg images for all files at once using the "Download all as png"
and "Download all as svg" buttons.
