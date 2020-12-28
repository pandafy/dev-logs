---
title: Polishing ShrutiVaani
published: true
---

The libraries that we were using for syllabification was ignoring spaces
between words. This was making the audio speech to be monotonous. It sounded
like it was pronouncing every individual syllable rather than a word.

I went into the source of the library and added a few cases to respect spaces
between different words. After making this change, it was grouping syllables of
the word. But, it was not there yet.

I then tuned the speed of the audio playback and padding between different
syllables. After playing with these parameters for some time, we reached a
point where it was giving a hint of the word. We were happy with the outcome at
this point.

The other thing which bothered us in ShrutiVaani was the audio corpus. The
audio corpus was big but it was not exhaustive. We tried recording sound for
some syllables ourselves, and it worked with them so much better than with the
existing audio corpus. I delegated the work of recording audio to a teammate
and she did a better job at it than me.

-----------------

### In other news

We had a meeting scheduled with our mentor today for demonstrating our project.
Luckily, the final evaluation of the project was postponed from December 29,
2020 to January 5, 2021. We now have more time to polish it more before the
final evaluation.
