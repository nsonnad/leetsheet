# leetsheet

`leetsheet` is a file format spec for capturing in plain-text all the elements needed to describe the chords, rhythm, and structure of a song. i.e., for creating a lead sheet or chord chart.

`leetsheet` is nothing more than a set of rules for how to describe a song in plain-text. as such it can by itself be used to document entire songs, but using tools like `leetsheet-parser`, you can also turn a `leetsheet` into a data structure that makes it easy to do other things with, like convert to midi or have a computer play your song.

## overview of a leetsheet

a `leetsheet` contains three elements:

1. metadata about the song (referred to as "frontmatter")
2. the song's structure
3. the individual sections that make up the structure

here's an example:

```md
---
title: "Purple Rain"
artist: "Prince"
tempo: 80
time: "4/4"
---

## structure

- [ intro, 1 ]
- [ verse, 2 ]
- [ prechorus, 1 ]
- [ chorus, 1 ]
- [ verse, 2 ]
- [ prechorus, 1 ]
- [ chorus, 1 ]

## sections

- intro

| Bb | Gm7 | F | Eb |

- verse

| Bb | Gm7 | F | Eb |

- prechorus

| Bb(8) - |

- chorus

| Eb | Bb | Gm7 | F | F7 |
```

1. `frontmatter` contains top-level facts about the song
2. `structure` contains an array of `[ section, repetitions ]` that describes the order in which to play the sections of the song, and how many time to repeat them. the song is played from top to bottom, through the structure
3. `sections` contains any number of user-defined, uniquely named sections containting `progressions`, i.e. chord progressions

## progressions

`progressions` are the most intricate part of `leetsheet`, but aim to be a simple way of declaring the rhythmic and harmonic elements of a song. (note that `leetsheet` is not interested in having a way to represent melodies or lyrics; in my mind the best tool for this job by far is good old sheet music.)

a `progression` is built like this:

- each area within `| |` equals one measure of musical time, where the number of beats is defined by `time` as declared in the frontmatter
- a chord's quality is written using any of the number of conventions supported by [tonal.js](https://github.com/tonaljs/tonal/blob/main/packages/chord-type/data.ts). a `-` in place of a chord represents a rest

### rhythm and subdivision

a chord can be described to span multiple measures using square brackets, like
  so: `| Bb7[3] |`, which says to repeat `Bb7` for three measures

by using parenthesis, you can specify the duration (note value) of a given
  chord. for example:

  `| Em7(2) Am7(4) Dm7(8) G7(8) | Cmaj7(1) |`

  defines a measure that contains a half note of `Em7`, a quarter note of `Am7`,
  and two eighth notes each of `Dm7` then `G7`, and finally a resolving whole
  note of `Cmaj7`. (putting no number next to the chord is the same as `(1)`)

the following durations are available (taken from [midiwriterjs](https://grimmdude.com/MidiWriterJS/docs/)):

```
1 : whole
2 : half
d2 : dotted half
dd2 : double dotted half
4 : quarter
4t : quarter triplet
d4 : dotted quarter
dd4 : double dotted quarter
8 : eighth
8t : eighth triplet
d8 : dotted eighth
dd8 : double dotted eighth
16 : sixteenth
16t : sixteenth triplet
32 : thirty-second
64 : sixty-fourth
Tn : where n is an explicit number of ticks (T128 = 1 beat)
```

## conclusion and examples

that's it! using just the specifications described here, you can represent virtually any song's chord progressions and overall structure. `leetsheet` is useful as a songwriting tool, as well, making it easy to rearrange a song's structure, quickly add an additional verse, add a variation to the end of a section, and so on.

if you want to see some `leetsheet`s in action, check out the [examples]()
