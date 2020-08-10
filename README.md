# Eyes of Gaia

A photomosaic of the planet created from images of 10,000 human irises.

More than 8,800 irises have been captured to date.

Learn more at [the Eyes of Gaia project website](https://jamescarlson.me)

## A photographic machine learning project

The project will use ML to match each eye to the surface of the Earth in a specific location, based on the texture and color features found in that eye and in that location.

The Earth is divided into hexes of equal size (using Uber's wonderful H3 library)[https://github.com/uber/h3] from each of which image data is obtained from (Landsat 8, 7, and 5 datasets)[https://developers.google.com/earth-engine/datasets/catalog/landsat] in the Google Earth Engine catalog.  

| Matching this                                                | To this                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src=".\docs\static\images\eye-hex-600x517.png" style="zoom:50%;" /> | <img src=".\docs\static\images\earth-1-hex-600x524.png" alt="eye-hex-768x661" style="zoom:50%;" /> |

## Image processing

The human eye is a challenging subject to capture. Achieving good results during photography requires the use of macro lenses, multiple light sources from different angles of incidence, and the combination of multiple photographs to achieve a reasonable result.

<img src=".\docs\static\images\image-processing.png"/>

This process is currently done manually using a combination of ImageMagick, Adobe Lightroom and Adobe Photoshop, but is the _first candidate for process automation using machine learning._

The project explores a variety of methods for image segmentation to extract the iris from the rest of the photograph of the facial region. So far, [Hough transforms](https://docs.opencv.org/2.4/doc/tutorials/imgproc/imgtrans/hough_circle/hough_circle.html), [Grabcut](https://www.pyimagesearch.com/2020/07/27/opencv-grabcut-foreground-segmentation-and-extraction/), and [Mask-RCNN](https://github.com/matterport/Mask_RCNN) have all been tried in various combinations. A hybrid approach may be necessary.

Major challenges include creating a fine mask edge, to ensure all iris features are included, dealing with partially occluded irises, and combining regions from different photos to remove specular highlights caused by reflections on the surface of the cornea from ambient objects such as eyelashes.

Each original image is approximately 3000x3000px and therefore poses a real challenge for a performant segmentation approach.

## Color Identification

To facilitate the matching process, the project will tag each iris image using a set of colors taken from the [XKCD Color Name Survey](https://xkcd.com/color/rgb/) having applied a method such as [color-thief](https://github.com/lokesh/color-thief) to find the dominant colors. Again, an iris that looks blue to us is mostly gray and white; an iris that is green to us is mostly blue and yellow.

## Training Dataset

A dataset with markup for training is available in the [Eyes of Gaia Dataset](https://github.com/intoempty/eyesofgaia-dataset) repository and includes a subset of the entire 8,800 iris database. 
