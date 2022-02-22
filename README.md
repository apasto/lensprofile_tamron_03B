# Tamron 135mm f/2.5 03B LCP

User-contributed Lens Correction Profile for the Tamron Adaptall 2 135mm ƒ/2.5 03B on Canon APS-C body. More about this vintage prime lens on [pentaxforums.com](https://www.pentaxforums.com/userreviews/tamron-adaptall-2-135mm-f-2-5-03b.html) ([archived link](https://web.archive.org/web/20220222084506/https://www.pentaxforums.com/userreviews/tamron-adaptall-2-135mm-f-2-5-03b.html)), [adaptall-2.com](http://www.adaptall-2.com/lenses/03B.html) ([archived link](https://web.archive.org/web/20220222084644/http://www.adaptall-2.com/lenses/03B.html)).

Notice that this is a rough estimate, its main limiting factor being the small number of covered apertures.
Nevertheless, it seems somewhat effective in reducing chromatic aberrations.
Personal preference applies in judging if it is worth applying or not.

**TO DO: examples, ACR original/corrected, RawTherapee original/corrected**

This LCP was generated using the [Adobe Lens Profile Creator](https://helpx.adobe.com/camera-raw/digital-negative.html#Adobe_Lens_Profile_Creator) ([archived link](https://web.archive.org/web/20220127035413/https://helpx.adobe.com/camera-raw/digital-negative.html)).

This repository and their contributors are not affiliated with Tamron Co., Ltd. or with any of its subsidiary companies. Tamron Co., Ltd. and its subsidiaries neither endorse, control, nor claim any responsibility for the content and accuracy of the files provided in this repository.

This profile can be applied in ACR and in [RawTherapee](https://rawpedia.rawtherapee.com/Lens/Geometry).

## lensfun

lcp-to-lensfun conversion can be carried out with [lensfun-convert-lcp](https://lensfun.github.io/manual/latest/lensfun-convert-lcp.html).

## Calibration configuration

- chart: 19&thinsp;×&thinsp;31 ISO A3 chart, Square Print Dimension 36 Pts.
- focal distance 6&thinsp;m
- lighting was constant throughout the shots (due to the indoor setting), but uneven over the chart area
- the small built-in collapsible lens hood was extended (its effect on vignetting seems negligible, due to its length compared to the focal length - this is reflected in its limited effectiveness in preventing flares)
- body: Canon 60D
- adapters: the Adaptall-2 mount was adapted to EF through 2 adapters in series: first an Adaptall-2 to Pentax ES (M24 screw, see picture 2 [here](https://www.pentaxforums.com/userreviews/adaptall-m42-screw-mount.html) ([archived link](https://web.archive.org/web/20220222092213/https://www.pentaxforums.com/userreviews/adaptall-m42-screw-mount.html)) for an example), then a generic M42 to EF. While this setup conserves infinity focus, different adapter arrangements may influence the optical behaviour.

The following apertures were covered:

- ƒ/2.5
- ƒ/5.6
- ƒ/11.0
- 
on the suggested 3&thinsp;×&thinsp;3 grid.
There is _plenty_ of room for improvement in aperture coverage, especially at the wide-open range, which is more prone to chromatic aberrations (while vignetting and distortion seem to be less significant over the whole aperture range).

## Aperture in EXIF

If using a programmable AF confirm chip (e.g. "EMF", "Dandelion"), note that in order to correctly record the aperture the picture is shot at, the camera is expected to meter at maximum aperture and stop down only when the shutter is released.
Therefore, exposure must be locked at maximum aperture, and only then the aperture ring must be stopped down to the desidered f-stop - then the shutter button is depressed. See this reply: [https://photo.stackexchange.com//How can I work around metering issues with adapted lenses on a Canon DSLR?](https://photo.stackexchange.com/a/22378).
This does not apply to pictures metered and shot while in LiveView.

If no AF chip is employed, or if it is non-programmable (with a preset wrong maximum aperture), or if the image is shot using trough-the-lens (TTL) metering while stopped down, the old-school alternative is to jot down the used F-value.
It can be set afterwards in EXIF, e.g. with this exiv2 command:

**TO DO: set aperture exiv2 one liner**

## EXIF metadata for a manual lens:

This example script sets all some of the relevant EXIF data, for all the files in a directory.
Rembember to set the serial number.

```bash
#!/usr/bin/env bash
find ./ -type f \( -iname \*.CR2 -o -iname \*.jpg -o -iname \*.xmp \) |
xargs -I filename exiv2 -v -k \
-M"del Exif.CanonCs.LensType" \
-M "set Exif.Photo.LensSpecification 135/1 135/1 25/10 320/10" \
-M "set Exif.Photo.LensSerialNumber 000000" \
-M "set Exif.CanonCs.MaxAperture 84" \
-M "set Exif.Canon.LensModel 135mm f/2.5 03B" \
-M "set Exif.Photo.LensModel 135mm f/2.5 03B" \
-M "set Exif.CanonCs.MinAperture 320" \
-M "set Exif.Photo.FocalLength 135/1" \
-M "set Exif.CanonCs.Lens 135 135 1" \
-M "set Xmp.aux.Lens Tamron 135mm f/2.5 03B" \
-M "set Exif.Photo.MaxApertureValue 25/10" \
-M "set Exif.Image.LensInfo 135/1 135/1 25/10 320/10" \
-M "set Exif.Photo.LensMake Tamron" \
"filename"
```




