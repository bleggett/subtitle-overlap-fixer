# subtitle-overlap-fixer
Corrects issues with SRT subtitle files that have been converted from more complex WebVTT format subtitles

Stolen from @nimatrueway's Gist (https://gist.github.com/nimatrueway/4589700f49c691e5413c5b2df4d02f4f) and slightly enhanced for my needs.

### Problem
Converting WebVTT subtitles to SRT subtitles via ffmpeg like so: `ffmpeg -i yourvttsub.vtt outputsrt.srt` _mostly_ works,
but since WebVTT supports many more timing and layout options than SRT, and `ffmpeg`'s WebVTT implementation [does not comply with the spec](https://trac.ffmpeg.org/ticket/4048), you can end up with a SRT that has a ton of incorrect overlapping timings and lines.

This tiny program attemps to fix those issues.

What it do:
- Removes empty subtitles
- Combines subtitles if the end-time of the previous subtitle overlaps with the start-time of the current subtitle.
- Removes subtitles with very very short duration (<150ms) if they contain what the previous line contains
- Removes first line of a subtitle, if it is the same as the last line of previous subtitle


### Installation/Usage
1. You need a recent version of `go`
2. Clone repo, `cd` to repo folder, run `go build`
3. This will create an executable named `subtitle-overlap-fixer`
4. Run that executable on the SRT file that `ffmpeg` spit out (via `ffmpeg -i test.vtt test.srt`)
    `subtitle-overlap-fixer test.srt`
5. This will back up the original `.srt` with a `.bak` extension, and generate a cleaned SRT file

NOTE: No warranty, express or implied. This works for my specific use-case perfectly, and I couldn't find a better way to solve it.
