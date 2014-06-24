4d-plugin-phash
===============

This plugin is a 4D implementation of the [pHash] (http://www.phash.org/) open source perceptual hash library.
It can compute and compare the perceptual hashes of PNG, BMP and JPEG files.
You can use it, for example, to search similar images of different file types stored in your database.

__Note__: Audio and Video files are not supported.

__Note__: If you create the PNG on Mac OS, make sure the "simple file" option is NOT used. Otherwise the hash value will be zero.

Example
-------
```
$fileA:=Get 4D folder(Current Resources folder)+"2004Cogs.jpg"
$fileB:=Get 4D folder(Current Resources folder)+"2004Cogs.bmp"
$fileC:=Get 4D folder(Current Resources folder)+"2004Cogs.png"

$statusA:=PH Compute DCT ($fileA;$hashA)//3726390674172847513
$statusB:=PH Compute DCT ($fileB;$hashB)//3726390674172847513
$statusC:=PH Compute DCT ($fileC;$hashC)//3726390674172847513

$fileD:=Get 4D folder(Current Resources folder)+"4D-main.jpg"
$statusD:=PH Compute DCT ($fileD;$hashD)//2732728107267830226
$fileE:=Get 4D folder(Current Resources folder)+"4D-main.png"
$statusE:=PH Compute DCT ($fileE;$hashE)//2732728107267830226

$distance1:=PH Compare DCT ($hashA;$hashB)//0
$distance2:=PH Compare DCT ($hashA;$hashD)//26

$sigma:=1
$gamma:=1
$N:=180

$pcc:=0//peak of cross correlation
$pcc1:=PH Compare RADISH ($fileA;$fileB;$sigma;$gamma;$N)//0.9999931960446829526
$pcc2:=PH Compare RADISH ($fileA;$fileC;$sigma;$gamma;$N)//0.9999931960446829526
$pcc3:=PH Compare RADISH ($fileB;$fileC;$sigma;$gamma;$N)//1

$alpha:=2
$lvl:=1

$hamming_distance:=0
$hamming_distance1:=PH Compare MH ($fileA;$fileB;$alpha;$lvl)//0.01215277777777777797
$hamming_distance2:=PH Compare MH ($fileA;$fileC;$alpha;$lvl)//0.01215277777777777797
$hamming_distance3:=PH Compare MH ($fileB;$fileC;$alpha;$lvl)//0
```
