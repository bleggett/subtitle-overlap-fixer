# subtitle-overlap-fixer
Corrects issues with SRT subtitle files that have been converted from more complex WebVTT format subtitles

Stolen from @nimatrueway's Gist (https://gist.github.com/nimatrueway/4589700f49c691e5413c5b2df4d02f4f) and slightly enhanced for my needs.

What it do:
    Removes empty subtitles
    Combines subtitles if the end-time of the previous subtitle overlaps with the start-time of the current subtitle.
    Removes subtitles with very very short duration (<150ms) if they contain what the previous line contains
    Removes first line of a subtitle, if it is the same as the last line of previous subtitle
