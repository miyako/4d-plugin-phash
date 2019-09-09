4d-plugin-phash
===============

Image hash based on [pHash](http://www.phash.org/).

### Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
||<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|

### Version

<img src="https://user-images.githubusercontent.com/1725068/41266195-ddf767b2-6e30-11e8-9d6b-2adf6a9f57a5.png" width="32" height="32" />

![preemption xx](https://user-images.githubusercontent.com/1725068/41327179-4e839948-6efd-11e8-982b-a670d511e04f.png)

#### Releases

[2.2](https://github.com/miyako/4d-plugin-phash/releases/tag/2.2)

#### Supported image formats

* png
* jpeg
* tiff

### Syntax

[miyako.github.io](https://miyako.github.io/2019/09/09/4d-plugin-phash.html)

### Examples

```
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
