![version](https://img.shields.io/badge/version-17%2B-3E8B93)
![platform](https://img.shields.io/static/v1?label=platform&message=mac-intel%20|%20mac-arm%20|%20win-64&color=blue)
[![license](https://img.shields.io/github/license/miyako/4d-plugin-phash)](LICENSE)
![downloads](https://img.shields.io/github/downloads/miyako/4d-plugin-phash/total)

# 4d-plugin-phash

Image perceptual hashing based on [pHash](https://github.com/aetilius/pHash).

Compute perceptual hashes of images and compare them to measure similarity. Supports DCT-based hashes, MH (Marginal Histogram) hashes, and RADISH cross-correlation.

## Supported image formats

* PNG
* JPEG
* TIFF

## Commands

### PH Compute DCT

Computes a DCT-based perceptual hash of an image file.

```4d
status := PH Compute DCT ( file ; hash )
```

| Parameter | Type | Description |
|---|---|---|
| file | Text | Path to the image file |
| hash | Text | Output: the computed hash as a decimal string |
| status | Longint | 0 on success, non-zero on error |

### PH Compare DCT

Compares two DCT hashes and returns the Hamming distance.

```4d
distance := PH Compare DCT ( hashA ; hashB )
```

| Parameter | Type | Description |
|---|---|---|
| hashA | Text | First DCT hash (decimal string from `PH Compute DCT`) |
| hashB | Text | Second DCT hash (decimal string from `PH Compute DCT`) |
| distance | Longint | Hamming distance between the two hashes (0 = identical) |

### PH Compare MH

Computes MH hashes for two image files and returns the Hamming distance.

```4d
distance := PH Compare MH ( fileA ; fileB ; alpha ; lvl )
```

| Parameter | Type | Description |
|---|---|---|
| fileA | Text | Path to the first image file |
| fileB | Text | Path to the second image file |
| alpha | Real | Scale factor for the MH algorithm (typically 2) |
| lvl | Real | Decomposition level (typically 1) |
| distance | Real | Normalized Hamming distance (0.0 = identical) |

### PH Compare RADISH

Computes RADISH digests for two image files and returns the peak cross-correlation.

```4d
pcc := PH Compare RADISH ( fileA ; fileB ; sigma ; gamma ; N )
```

| Parameter | Type | Description |
|---|---|---|
| fileA | Text | Path to the first image file |
| fileB | Text | Path to the second image file |
| sigma | Real | Standard deviation for the Gaussian filter (typically 1) |
| gamma | Real | Gamma correction factor (typically 1) |
| N | Longint | Number of bins for the digest (typically 180) |
| pcc | Real | Peak cross-correlation (1.0 = identical) |

## Examples

```4d
$fileA:=Get 4D folder(Current resources folder)+"2004Cogs.jpg"
$fileB:=Get 4D folder(Current resources folder)+"2004Cogs.bmp"
$fileC:=Get 4D folder(Current resources folder)+"2004Cogs.png"

$statusA:=PH Compute DCT ($fileA;$hashA)
$statusB:=PH Compute DCT ($fileB;$hashB)
$statusC:=PH Compute DCT ($fileC;$hashC)
  //mac/windows (pHash-1.0.0): 3695991198010760088

$fileD:=Get 4D folder(Current resources folder)+"4D-main.jpg"
$statusD:=PH Compute DCT ($fileD;$hashD)
$fileE:=Get 4D folder(Current resources folder)+"4D-main.png"
$statusE:=PH Compute DCT ($fileE;$hashE)
  //mac/windows (pHash-1.0.0): 10888135207193571144

$distance1:=PH Compare DCT ($hashA;$hashB)
$distance2:=PH Compare DCT ($hashA;$hashD)

$sigma:=1
$gamma:=1
$N:=180

$pcc:=0  //peak of cross correlation
$pcc1:=PH Compare RADISH ($fileA;$fileB;$sigma;$gamma;$N)
$pcc2:=PH Compare RADISH ($fileA;$fileC;$sigma;$gamma;$N)
  //mac/windows (pHash-1.0.0): 0.9999931960447
$pcc3:=PH Compare RADISH ($fileB;$fileC;$sigma;$gamma;$N)  //1

$alpha:=2
$lvl:=1

$hamming_distance:=0
$hamming_distance1:=PH Compare MH ($fileA;$fileB;$alpha;$lvl)
$hamming_distance2:=PH Compare MH ($fileA;$fileC;$alpha;$lvl)
  //mac/windows (pHash-1.0.0): 0.01215277777778
$hamming_distance3:=PH Compare MH ($fileB;$fileC;$alpha;$lvl)  //0
```

## Releases

[Releases](https://github.com/miyako/4d-plugin-phash/releases)
