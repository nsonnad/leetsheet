# leetsheet

`leetsheet` is a file format spec for capturing in plain-text all the elements needed to describe the chords, rhythm, and structure of a song. i.e., for creating a lead sheet or chord chart.

`leetsheet` is nothing more than a set of rules for how to describe a song in plain-text. as such it can by itself be used to document entire songs, but using tools like `leetsheet-parser`, you can also turn a `leetsheet` into a data structure that makes it easy to do other things with, like convert to midi or have a computer play your song.

## overview of a leetsheet

a `leetsheet` contains three elements:

1. metadata about the song (referred to as "frontmatter")
2. the song's structure
3. the individual sections that make up the structure

like so:

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

| Bb(8) -(14) |

- chorus

| Eb | Bb | Gm7 | F | F7 |
```
