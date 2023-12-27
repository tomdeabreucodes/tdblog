+++
title = 'PyJig: A Digital Jigsaw Puzzle Factory'
date = 2023-12-23T00:24:02Z
tags = ['Python', 'SVG', 'Package']
draft = true
+++

## Introduction
Creating a puzzle programmatically is an interesting challenge I faced, which formed part of a wider project to create an online jigsaw puzzle app (WIP). I initially underestimated the approach required to achieve this, especially in a way that both looked satisfying, had reasonable levels of variation and would be flexible enough to work with different sizes of puzzle and number of pieces - as a result, I would like to share my solution alongside some of my thoughts and learnings on the topic. Before we dive in, I would like to acknowledge an [excellent tool implemented in JavaScript](https://github.com/Draradech/jigsaw/tree/master), I did not use this as a source of inspiration for a number of reasons:
- I did not particularly understand the source code/approach (and was eager to learn and apply rather than lift and shift)
- It did not take a piece by piece approach
- It was in JS and I needed it in Python

However, If you are simply looking for an overall template which can create a puzzle of any size, or the above justifications do not apply to you, this is an excellent resource.

## Cut
The design of a puzzle cut is typically fed into a CNC, laser cutting machine which will trace the design with high precision leaving you with the individual pieces, and to 'cut' the puzzle up digitally, we will use a similar principle. Although rather than approaching the design as a whole, as you would for a physical puzzle, I instead generated an SVG made up of cut paths for every individual piece.

## Design
The design of the actual cut involved learning about SVG curves and how to connect them together in a way that looked satisfying and could be procedurally generated. Overall the piece design I went with was similar to the conventional puzzle shape with either a notch or a gap on each of the interior piece sides, but with a more exaggerated curve to achieve a more unique look. I added randomness to introduce heterogeneity by determining whether each side of the piece was a notch or a gap. While there is randomness, the pieces are not truly unique. This is a trait which is valued by puzzle enthusiasts, as uniqueness of each piece makes it easier to avoid 'false fits', which is where two pieces may seem to slot together perfectly, but are in fact not a match. Adding randomness (i.e. a jitter variable) into the curve values themselves would help achieve this and make the motif more interesting, and is a worthwhile future enhancement to this project (similar to Drardech's implementation linked in the intro).

## Masking
To perform the digital cut itself, a binary mask is used to tag pixels inside the svg path as visible and everything else not.

## Cut
This masked version of each piece is then output as an individual vector or image file to represent the individual piece.

## Use cases
- Create a digital puzzle set
- Create blank template for a puzzle of any custom sized

## Limitations
While the bitmap version of the exports are economical, the SVG version contains the parts of the underlying image hidden by the mask, taking up an unnecessary amount of space. A potential improvement to my implementation would be to crop the underlying image to a slightly larger area than the puzzle piece, meaning that minimal excess image data is stored.

A limtation of using the bitmap version is the resolution of the pixels. The pieces are made up of curves which may cause unnatural or jagged looking edges once converted. Where possible it would be advisable to use SVGs to retain the perfec curves.