![version](https://img.shields.io/badge/version-17%2B-3E8B93)
![platform](https://img.shields.io/static/v1?label=platform&message=mac-intel%20|%20mac-arm%20|%20win-64&color=blue)
[![license](https://img.shields.io/github/license/miyako/4d-plugin-phash)](LICENSE)
![downloads](https://img.shields.io/github/downloads/miyako/4d-plugin-phash/total)

# 4d-plugin-phash

Image hash based on [pHash](https://github.com/aetilius/pHash).

#### Supported image formats

* png
* jpeg
* tiff

### Syntax

[miyako.github.io](https://miyako.github.io/2019/09/09/4d-plugin-phash.html)

### Examples

```4d
$fileA:=Get 4D folder(Current resources folder)+"2004Cogs.jpg"
$fileB:=Get 4D folder(Current resources folder)+"2004Cogs.bmp"
$fileC:=Get 4D folder(Current resources folder)+"2004Cogs.png"

$statusA:=PH Compute DCT ($fileA;$hashA)
$statusB:=PH Compute DCT ($fileB;$hashB)
$statusC:=PH Compute DCT ($fileC;$hashC)
  //mac/windows (pHash-1.0.0): 3695991198010760088
  //windows (pHash-0.9.0): 3726390674172847513
  //old plugin (0.9.6 for UNIX/MinGW): 3726390674172847513

$fileD:=Get 4D folder(Current resources folder)+"4D-main.jpg"
$statusD:=PH Compute DCT ($fileD;$hashD)
$fileE:=Get 4D folder(Current resources folder)+"4D-main.png"
$statusE:=PH Compute DCT ($fileE;$hashE)
  //mac/windows (pHash-1.0.0): 10888135207193571144
  //windows (pHash-0.9.0): 2732728107267830226
  //old plugin (0.9.6 for UNIX/MinGW): 2732728107267830226

$distance1:=PH Compare DCT ($hashA;$hashB)
$distance2:=PH Compare DCT ($hashA;$hashD)

$sigma:=1
$gamma:=1
$N:=180

$pcc:=0  //peak of cross correlation
$pcc1:=PH Compare RADISH ($fileA;$fileB;$sigma;$gamma;$N)
$pcc2:=PH Compare RADISH ($fileA;$fileC;$sigma;$gamma;$N)
  //mac/windows (pHash-1.0.0): 0.9999931960447
  //windows (pHash-0.9.0): 0.9999932088701
  //old plugin (0.9.6 for UNIX/MinGW): 0.9999931960446829526
$pcc3:=PH Compare RADISH ($fileB;$fileC;$sigma;$gamma;$N)  //1  

$alpha:=2
$lvl:=1

$hamming_distance:=0
$hamming_distance1:=PH Compare MH ($fileA;$fileB;$alpha;$lvl)
$hamming_distance2:=PH Compare MH ($fileA;$fileC;$alpha;$lvl)
  //mac/windows (pHash-1.0.0): 0.01215277777778
  //windows (pHash-0.9.0): 0.001736111111111 [BUG!]
  //old plugin (0.9.6 for UNIX/MinGW): 0.01215277777777777797
$hamming_distance3:=PH Compare MH ($fileB;$fileC;$alpha;$lvl)  //0
```
