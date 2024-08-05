# High-Low_Magnification_Single_Cell_Mapping
A set of functions designed to help map single cells in high throughput imaging at multiple magnifications

Functions used to map low magnification in-situ genotyping images to high magnification phenotyping images in the paper:
Pooled tagging and hydrophobic targeting of endogenous proteins for unbiased mapping of unfolded protein responses
https://www.biorxiv.org/content/10.1101/2023.07.13.548611v1

The functions perform the following steps:
1.	A dataframe connecting tile number to tile center coordinates is made by extracting tile center stage coordinates from nd2 file metadata.
2.	From coordinates, tiles are arranged in a matrix that contains tile position. Every element in the matrix contains tile number in its respective position. Value of ‘-1’ indicated no tile image exists for this coordinate (occurs since tiles cover a circular well and stored in a square matrix).
3.	Final matrix form must ensure the tile boundaries align correctly. Due to microscope setting, the tile matrix may need to be flipped or transposed such that correct boundaries align.
4.	Five fiducial cells are manually selected at random, four from the edges for the well, and one from the center (repeated for every well). The coordinates (tile number, x in tile, y in tile) of the cells must be found at both the lower and higher magnification images.
5.	Given the coordinates of the fiducial cells, the five mapping parameters for a given well are calculated using sequential least square programming minimization function, scipy package. The five mapping parameters are use to create an affine transformation that includes x-translation, y-translation, angle of rotation, x-scaling, and y-scaling.
6.	Once mapping parameters are optimized, the affine transformation is performed for every cell in the well.

![Workflow diagram of mapping functions](image_url)
