+++
title = 'Create Your Own Digital Puzzle Set or Template with Python'
date = 2023-12-23T00:24:02Z
draft = true
+++

## Introduction
Creating a puzzle programmatically is an interesting challenge I faced, which formed part of a wider project to create an online jigsaw puzzle app. I initially underestimated the approach required to achieve this, especially in a way that both looked satisfying, had reasonable levels of variation and would be flexible enough to work with different sizes of puzzle and number of pieces.

## Motif
The design of a puzzle cut is called a motif, and to 'cut' the puzzle up digitally, we will use a similar principle. Although rather than approaching the design as a whole, as you would for a physical puzzle, I instead created a motif made up of cut lines for every individual piece. Cuts in this case are SVG paths which carve out the boundary for the puzzle piece.

## Design
The design of the actual cut involved learning about SVG curves and how to connect them together in a way that looked satisfying and could be procedurally generated. Overall the piece design I went with was similar to the conventional puzzle shape with either a notch or a gap on each of the interior piece sides, but with a more exaggerated curve which made it a bit more unique. I added randomness to introduce randomness of whether each side of the piece was a notch or a gap. While there is randomness, the pieces are not truly unique. This is a trait which is valued by puzzle enthusiasts, as uniqueness of each piece makes it easier to avoid 'false fits', which is where two pieces may seem to slot together perfectly, but are in fact not a match. Adding randomness (i.e. a jitter variable) into the curve values themselves would help achieve this and make the motif more interesting, and is a worthwhile future enhancement to this project.

## Mask
To perform the digital cut itself, a binary mask is used to tag pixels inside the svg path as visible and everything else not.

## Cut
This masked version of each piece is then output as an individual vector or image file to represent the individual piece.

## Use cases
- Create a digital puzzle set
- Create blank template for a puzzle of any custom sized

## Limitations
While the bitmap version of the exports are economical, the SVG version contains the parts of the underlying image hidden by the mask, taking up an unnecessary amount of space. A potential improvement to my implementation would be to crop the underlying image to a slightly larger area than the puzzle piece, meaning that minimal excess image data is stored.

A limtation of using the bitmap version is the resolution of the pixels. The pieces are made up of curves which may cause unnatural or jagged looking edges once converted. Where possible it would be advisable to use SVGs to retain the perfec curves.