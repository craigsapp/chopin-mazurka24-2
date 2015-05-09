Score/Performance Alignment Demonstration
=========================================

A live demonstration can be found at http://www.ccarh.org/chopin/op24n2 .  If
you are using Chrome or Firefox (but not Safari), try clicking on notes
in the score to start the audio playback from that note.

There are three main components for preparation of the animated score:

1 Score production
2 Performance time extraction and alignment mapping to the score
3 Display interface

Score production
===================

Scores are typeset in the SCORE music editor.  Data entry can
be facilitated by OMR with [SharpEye](http://www.visiv.co.uk). SharpEye
files can be converted directly into SCORE data with
[mro2score](http://www.ccarh.org/courses/253/lab/mro2score). Then
the scorelib program
[mrofix](https://github.com/craigsapp/scorelib/blob/master/src-programs/mrofix.cpp)
can be used to cleanup some systematic fixes, and final edition
can be done in the SCORE editor (mostly manual refinements
of slurs).  The SCORE data files for each page are then marked
with timestamps and split into separate system files with the
[webscore](https://github.com/craigsapp/scorelib/blob/master/src-programs/webscore.cpp)
program.

The SCORE data for each system is converted into
EPS files in SCORE, then converted into SVG image with
[seps2svg](https://github.com/th-we/seps2svg).  When preparing the SCORE
data for printing, note serial numbers are added as Font-99 markers which
are converted into PostScript comments in the EPS output from SCORE. These
comments are then processed and converted into SVG &lt;g&gt;
elements with class tags indicating noteon and noteoff times in terms of
quarter notes for the note (as well as any other interesting class tags,
such as the current measure, the chord groupings, beam groupings, item
type, etc).


Performance time extraction
===========================

Performance timing extraction is done using Sonic Visualiser:

http://sonic-visualiser.org

Here is a basic outline of the data extraction process:

http://wiki.ccarh.org/wiki/Op27

The extracted timing data is aligned with quarter-note timestamps 
generated from the score.  Here is a sample from the start of the
time-to-quarter-note mapping for a performance:

	{"qstamp":0,	"tstamp":1.739},
	{"qstamp":1,	"tstamp":2.182},
	{"qstamp":2,	"tstamp":2.548},
	{"qstamp":3,	"tstamp":2.908},
	{"qstamp":4,	"tstamp":3.268},
	{"qstamp":5,	"tstamp":3.624},
	{"qstamp":6,	"tstamp":3.978},
	{"qstamp":7,	"tstamp":4.318},
	{"qstamp":8,	"tstamp":4.678},
	{"qstamp":9,	"tstamp":5.065},
	{"qstamp":10,	"tstamp":5.458},
	{"qstamp":11,	"tstamp":5.968},
	{"qstamp":12,	"tstamp":6.668},
	{"qstamp":12.5,	"tstamp":6.928},
	{"qstamp":13,	"tstamp":7.188},
	{"qstamp":13.3333,	"tstamp":7.305},
	{"qstamp":13.6667,	"tstamp":7.421},
	{"qstamp":14,	"tstamp":7.538},


Web implementation
===================

The coordination of audio playback and score animation is done in
JavaScript code.  The audio is played back with the HTML 5 audio
interface.  While the audio is playing, the current playback time is
continually polled (at 43 Hz) and checked to see if a new score event
has been reached.  If so, then adjust the CSS class styles based on the
note found at that time to highlight notes red if starting or black if
ending at that time in the score.  See index.html file for JavaScript
implementation.


Future work
============

Some possible future enhancements:

**Scrolling variations**: scroll continuously; scroll before the end of a line;
scroll when at the middle of a line; paginate display.

**Note highlighting**: increase note sizes when playing; put aura around 
playing notes; animate highlighting of active notes (add decay to 
non-highlighted states; show non-active music in gray and active notes in
black.



