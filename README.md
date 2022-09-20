# PicoCTF2022-Forensics
=======================================================================================
### Enhance!
AUTHOR: LT 'SYREAL' JONES

Description:
Download this image file and find the flag.

Viewing the [SVG file](https://www.lifewire.com/svg-file-4120603) doesn't show us much:
![Drawing Flag](/PicoCTF2022-Forensics/docs/assets/images/drawing.flag.svg)

Viewing the contents of the file shows us the following text;

```$ strings drawing.flag.svg```


```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!-- Created with Inkscape (http://www.inkscape.org/) -->
<svg
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:cc="http://creativecommons.org/ns#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
   xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
   width="210mm"
   height="297mm"
   viewBox="0 0 210 297"
   version="1.1"
   id="svg8"
   inkscape:version="0.92.5 (2060ec1f9f, 2020-04-08)"
   sodipodi:docname="drawing.svg">
  <defs
     id="defs2" />
  <sodipodi:namedview
     id="base"
     pagecolor="#ffffff"
     bordercolor="#666666"
     borderopacity="1.0"
     inkscape:pageopacity="0.0"
     inkscape:pageshadow="2"
     inkscape:zoom="0.69833333"
     inkscape:cx="400"
     inkscape:cy="538.41159"
     inkscape:document-units="mm"
     inkscape:current-layer="layer1"
     showgrid="false"
     inkscape:window-width="1872"
     inkscape:window-height="1016"
     inkscape:window-x="48"
     inkscape:window-y="27"
     inkscape:window-maximized="1" />
  <metadata
     id="metadata5">
    <rdf:RDF>
      <cc:Work
         rdf:about="">
        <dc:format>image/svg+xml</dc:format>
        <dc:type
           rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
        <dc:title></dc:title>
      </cc:Work>
    </rdf:RDF>
  </metadata>
  <g
     inkscape:label="Layer 1"
     inkscape:groupmode="layer"
     id="layer1">
    <ellipse
       id="path3713"
       cx="106.2122"
       cy="134.47203"
       rx="102.05357"
       ry="99.029755"
       style="stroke-width:0.26458332" />
    <circle
       style="fill:#ffffff;stroke-width:0.26458332"
       id="path3717"
       cx="107.59055"
       cy="132.30211"
       r="3.3341289" />
    <ellipse
       style="fill:#000000;stroke-width:0.26458332"
       id="path3719"
       cx="107.45217"
       cy="132.10078"
       rx="0.027842503"
       ry="0.031820003" />
    <text
       xml:space="preserve"
       style="font-style:normal;font-weight:normal;font-size:0.00352781px;line-height:1.25;font-family:sans-serif;letter-spacing:0px;word-spacing:0px;fill:#ffffff;fill-opacity:1;stroke:none;stroke-width:0.26458332;"
       x="107.43014"
       y="132.08501"
       id="text3723"><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08501"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3748">p </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08942"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3754">i </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09383"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3756">c </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09824"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3758">o </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10265"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3760">C </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10706"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3762">T </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11147"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3764">F { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ 6 7 8 3 c c 4 6 }</tspan></text>
  </g>
</svg>
```

This image was created using Inkscape.

From looking at the output, you can see the text is contained within the "tspan" tags lying within the "text" tags. By joining them you get the flag:
> picoCTF{3nh4nc3d_6783cc46}

Note that you can also find this by opening the file in browser and using ctrl-A to select all, and then ctrl-F to search. The flag is revealed in the search box. The whitespace in the flag can be removed using CyberChef.

On YouTube, [John Hammond](https://www.youtube.com/watch?v=dbKwngknixo) shows a simple bash script to pull out the flag:
```
#!/bin/bash
wget https://artifacts.picoctf.net/c/138/drawing.flag.svg
cat drawing.flag.svg | grep "</tspan>" | cut -d ">" -f2 | cut -d "<" -f1 | tr -d "\n" | tr -d " "
```

As an aside, if you open the image in Inkscape and zoom in to the tiny circle in the middle of the image, you will eventually see the SVG Text:

![Enhanced image](/PicoCTF2022-Forensics/docs/assets/images/enhance_zoomedin.png)

You can also view the XML in XML Editor:
![Inkscape XML Editor](/PicoCTF2022-Forensics/docs/assets/images/Inkscape XML Editor.png)



=======================================================================================
### File Types

AUTHOR: GEOFFREY NJOGU

Description:
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.
You can download the file from [here](https://artifacts.picoctf.net/c/325/Flag.pdf).

First checking what kind of file it is: 
```
$  file Flag.pdf 
Flag.pdf: shell archive text
$ mv Flag.pdf flag.shar
```
"A shell archive or shar file is a single file that contains one or more other files. Files are extracted from the archive with the standard UNIX Bourne shell"
While the shar format has the advantage of being plain text, it poses a risk due to being executable;[2] for this reason the older and more general tar file format is usually preferred even for transferring text files. GNU provides its own version of shar in the GNU Sharutils collection.
You can extract the files using the sh command: 

```
$ sudo apt install sharutils
$ ls -sh flag.shar
8.0K flag.shar
$ sh flag.shar
x - created lock directory _sh00046.
x - extracting flag (text)
x - removed lock directory _sh00046.
$ ls
flag  flag.shar
$ file flag
flag: current ar archive
$ mv flag flag.ar
$ ls -sh flag.ar
4.0K flag.ar
```
The archiver, also known simply as ar, is a Unix utility that maintains groups of files as a single archive file.
ar - create, modify, and extract from archives
The GNU ar program creates, modifies, and extracts from archives. An archive is a single file holding a collection of other files in a structure that makes it possible to retrieve the original individual files (called members of the archive).
```
$ ar -x flag.ar
$ ls
flag  flag.ar  flag.shar
$ file flag
flag: cpio archive
$ mv flag flag.cpio
$ ls -sh flag.cpio
4.0K flag.cpio
```
cpio is a general file archiver utility and its associated file format.
cpio - copy files to and from archives
GNU cpio is a tool for creating and extracting archives, or copying files from one place to another. It handles a number of cpio formats as well as reading and writing tar files.
```
$ cpio -i --file flag.cpio
2 blocks
$ ls
flag  flag.ar  flag.cpio  flag.shar
$ file flag
flag: bzip2 compressed data, block size = 900k
$ mv flag flag.bz2
$ ls -sh flag.bz2
4.0K flag.bz2
```
bzip2 is a free and open-source file compression program that uses the Burrows–Wheeler algorithm. It only compresses single files and is not a file archiver. 
```
$ bunzip2 flag.bz2
$ ls
flag  flag.ar  flag.cpio  flag.shar
$ file flag
flag: gzip compressed data, was "flag", last modified: Tue Mar 15 06:50:41 2022, from Unix, original size modulo 2^32 326
$ mv flag flag.gz
$ ls -sh flag.gz
4.0K flag.gz
```
gzip is a file format and a software application used for file compression and decompression. 
gzip, gunzip, zcat - compress or expand files

```
$ gunzip flag.gz
$ ls
flag  flag.ar  flag.cpio  flag.shar
$ file flag
flag: lzip compressed data, version: 1
$ mv flag flag.lzip
$ ls -sh flag.lzip
4.0K flag.lzip
```
lzip is a free, command-line tool for the compression of data; it employs the Lempel–Ziv–Markov chain algorithm (LZMA) with a user interface that is familiar to users of usual Unix compression tools, such as gzip and bzip2.
The file that is produced by lzip is usually given .lz as its filename extension, and the data is described by the media type application/lzip.

```
$ sudo apt install lzip
$ lzip -d flag.lzip
$ ls
flag.ar  flag.cpio  flag.lzip.out  flag.shar
$ file flag.lzip.out
flag.lzip.out: LZ4 compressed data (v1.4+)
$ mv flag.lzip.out flag.lz4
$ ls -sh flag.lz4
4.0K flag.lz4
```
LZ4 is a lossless data compression algorithm that is focused on compression and decompression speed. It belongs to the LZ77 family of byte-oriented compression schemes.
unlz4 is equivalent to lz4 -d

```
$ sudo apt install lz4
$ lz4 -d flag.lz4
Decoding file flag 
flag.lz4             : decoded 263 bytes 
$ ls
flag  flag.ar  flag.cpio  flag.lz4  flag.shar
$ file flag
flag: LZMA compressed data, non-streamed, size 253
$ mv flag flag.lzma
$ ls -sh flag.lzma
4.0K flag.lzma
```
The Lempel–Ziv–Markov chain algorithm (LZMA) is an algorithm used to perform lossless data compression.

```
$ xz -d flag.lzma
$ ls
flag  flag.ar  flag.cpio  flag.lz4  flag.shar
$ file flag
flag: lzop compressed data - version 1.040, LZO1X-1, os: Unix
$ mv flag flag.lzop
$ ls -sh flag.lzop
4.0K flag.lzop
```
lzop is a free software file compression tool which implements the LZO algorithm and is licensed under the GPL.
lzop is a file compressor very similar to gzip. lzop favors speed over compression ratio.
```
$ sudo apt install lzop
$ lzop -d flag.lzop
$ ls
flag  flag.ar  flag.cpio  flag.lz4  flag.lzop  flag.shar
$ file flag
flag: lzip compressed data, version: 1
$ mv flag flag.lz
$ ls -sh flag.lz
4.0K flag.lz
```


```
$ lzip -d flag.lz
$ ls
flag  flag.ar  flag.cpio  flag.lz4  flag.lzop  flag.shar
$ file flag
flag: XZ compressed data, checksum CRC64
$ mv flag flag.xz
$ ls -sh flag.xz
4.0K flag.xz
$ unxz flag.xz
$ ls
flag  flag.ar  flag.cpio  flag.lz4  flag.lzop  flag.shar
$ file flag
flag: ASCII text
$ mv flag flag.txt
$ ls -sh flag.txt
4.0K flag.txt
$ cat flag.txt
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f39353063346665657d0a
```
This is hexadecimal and can be decoded in CyberChef, or on the command line using xxd:
```
$ cat flag.txt | xxd -r -p
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee}
```



If you want to use a python script to decode the hexadecimal:
```
#!/usr/bin/env python3
string = "7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f6630725f3062326375723137795f39353063346665657d0a"
byte_array = bytearray.fromhex(string)
print(byte_array.decode())
```
