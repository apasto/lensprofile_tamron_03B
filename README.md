# Lens Correction Profile for Tamron 135mm f/2.5 03B

User-contributed Lens Correction Profile for the Tamron Adaptall 2 135mm ƒ/2.5 03B on Canon APS-C body. More about this vintage prime lens on [pentaxforums.com](https://www.pentaxforums.com/userreviews/tamron-adaptall-2-135mm-f-2-5-03b.html) ([archived link](https://web.archive.org/web/20220222084506/https://www.pentaxforums.com/userreviews/tamron-adaptall-2-135mm-f-2-5-03b.html)), [adaptall-2.com](http://www.adaptall-2.com/lenses/03B.html) ([archived link](https://web.archive.org/web/20220222084644/http://www.adaptall-2.com/lenses/03B.html)).

Notice that this is a rough estimate, its main limiting factor being the small number of covered apertures.
Nevertheless, it seems somewhat effective in reducing chromatic aberrations.
Usefulness: debatable. Personal preference applies in judging if it is worth applying or not.

**TO DO: examples, ACR original/corrected, RawTherapee original/corrected**

This LCP was generated using the [Adobe Lens Profile Creator](https://helpx.adobe.com/camera-raw/digital-negative.html#Adobe_Lens_Profile_Creator) ([archived link](https://web.archive.org/web/20220127035413/https://helpx.adobe.com/camera-raw/digital-negative.html)).

This repository and their contributors are not affiliated with Tamron Co., Ltd. or with any of its subsidiary companies. Tamron Co., Ltd. and its subsidiaries neither endorse, control, nor claim any responsibility for the content and accuracy of the files provided in this repository.

This profile can be applied in ACR and in [RawTherapee](https://rawpedia.rawtherapee.com/Lens/Geometry).

## Converting to [lensfun](https://lensfun.github.io/) format

lcp-to-lensfun conversion can be carried out with [lensfun-convert-lcp](https://lensfun.github.io/manual/latest/lensfun-convert-lcp.html).

## Calibration configuration

- chart: 19&thinsp;×&thinsp;31 ISO A3 chart, Square Print Dimension 36 Pts
- focal distance 6&thinsp;m
- lighting was constant throughout the shots (due to the indoor setting), but uneven over the chart area
- the small built-in collapsible lens hood was extended (its effect on vignetting seems negligible, due to its length compared to the focal length - this is reflected in its limited effectiveness in preventing flares)
- body: Canon 60D
- adapters: the Adaptall-2 mount was adapted to EF through 2 adapters in series: first an Adaptall-2 to Pentax ES (M24 screw, see picture 2 [here](https://www.pentaxforums.com/userreviews/adaptall-m42-screw-mount.html) ([archived link](https://web.archive.org/web/20220222092213/https://www.pentaxforums.com/userreviews/adaptall-m42-screw-mount.html)) for an example), then a generic M42 to EF. While this setup conserves infinity focus, different adapter arrangements may influence the optical behaviour.

The following apertures were covered:

- ƒ/2.5
- ƒ/5.6
- ƒ/11.0

on the suggested 3&thinsp;×&thinsp;3 grid.
There is _plenty_ of room for improvement in aperture coverage, especially at the wide-open range, which is more prone to chromatic aberrations (while vignetting and distortion seem to be less significant over the whole aperture range).

## Collateral: setting aperture metadata in EXIF

If using a programmable AF confirm chip (e.g. "EMF", "Dandelion"), note that in order to correctly record the aperture the picture is shot at, the camera is expected to meter at maximum aperture and stop down only when the shutter is released.
Therefore, exposure must be locked at maximum aperture, and only then the aperture ring must be stopped down to the desidered f-stop - then the shutter button is depressed. See this reply: [photo.stackexchange.com / How can I work around metering issues with adapted lenses on a Canon DSLR?](https://photo.stackexchange.com/a/22378).

This does not apply to pictures metered and shot while in LiveView.

If no AF chip is employed, if it is non-programmable (with a preset wrong maximum aperture), or if the image is shot using trough-the-lens (TTL) metering while stopped down, the old-school alternative is to jot down the used F-value.
It can be set afterwards in EXIF, e.g. for ƒ/8 using [exiv2](https://exiv2.org/index.html):

`exiv2 -v -k -M "set Exif.Photo.FNumber 80/10" filename`

### F-number aperture to APEX ApertureValue

The field `Exif.Photo.ApertureValue` may be also set by the camera. That field is set in the "APEX system" format (see [this question](https://photo.stackexchange.com/q/19143) and [this Wikipedia entry](https://en.wikipedia.org/wiki/APEX_system).
To avoid conflicting properties, we can either delete that key-value pair or set it accordingly.

The formula for converting a F-number into an APEX value is:

![APEX aperture formula](https://render.githubusercontent.com/render/math?math=A_v%20=%20\log_2A_f^2)

To set that with exiv2:

`exiv2 -v -k -M "set Exif.Photo.ApertureValue ${aperture_apex}" filename`

To delete the ApertureValue field instead (expecting any software to read the F-number from FNumber, if ApertureValue is missing)

`exiv2 -v -k -M "del Exif.Photo.ApertureValue" filename`

## EXIF metadata for a manual lens:

This example script sets all some of the relevant EXIF data, for all the files in a directory (matching .CR2, .jpg, and .xmp, other extension may apply).
The lens serial number can be optionally set in `Exif.Photo.LensSerialNumber`.
Refer to exiv2 documentation (be aware that documentation on CanonCs key-value pairs seems scarce).

```bash
#!/usr/bin/env bash
find ./ -type f \( -iname \*.CR2 -o -iname \*.jpg -o -iname \*.xmp \) |
xargs -I filename exiv2 -v -k \
-M"del Exif.CanonCs.LensType" \
-M "set Exif.Photo.LensSpecification 135/1 135/1 25/10 320/10" \
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
