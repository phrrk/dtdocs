---
title: editing an image - workflow overview
id: workflow-overview
draft: false
weight: 20
author: "people"
---

This section will guide you through the basics of developing an image in the [darkroom](../../darkroom/_index.md) view.

To begin, open an image in darkroom mode by double clicking an image thumbnail in the [lighttable](../../lighttable/_index.md) view. The darkroom is where the actual adjustments for an image are made, where an arsenal of modules are at hand to help you reach your goal.

Each change made on a module while developing an image is turned into a history stack item. The history is stored in a database and in an XMP sidecar file for that image.

All changes are stored automatically when you switch images or go from one darktable view to another. You can safely leave darkroom mode or quit darktable at any time and come back later to continue your work. For this reason darktable does not need a “save” button and it does not have one.

On the left panel in darkroom mode is the [history stack](../../module-reference/utility-modules/darkroom/history-stack.md), showing changes starting from bottom, and building up with each change made to the image. You can select a point in this history to show how the image looked at that point, for comparison of changes. The stack can be compressed: it will be optimized and redundant changes will be discarded. When you are happy with what you have done, just compress the history stack.

A number of modules are shipped with darktable, arranged into groups. These [module groups](../../module-reference/utility-modules/darkroom/module-groups.md) are accessed via toggle buttons in the right panel, just under the [histogram](../../module-reference/utility-modules/shared/histogram.md). There are also two special module groups named “active” and “favorites”, which only show modules enabled in the history for the current image, and modules selected as a favourite, respectively. Marking a module as a favorite is done in the [more modules](../../module-reference/utility-modules/darkroom/more-modules.md) module at the bottom of the right panel, by clicking a module until a star is displayed in front of the icon.

# choosing a workflow

When processing an image, we apply a sequence of modules, known as the [pixelpipe](../../darkroom/processing-modules-and-pixelpipe/_index.md). 

```
camera                                                       display
  |                                                             ^
  V                                                             |
	
scene-referred  -->   tone map compression     -->  display-referred
   modules          (eg. filmic or basecurve)            modules
```

The _scene-referred_ modules deal with pixel values that are proportional to the amount of light collected by the camera at the scene. At some point in the pixelpipe, the pixel values are compressed down by a tone mapping module into a non-linear dynamic range suitable for display or a monitor or a hardcopy print. This compressed representation is knowm as _display-referred_. 

There are two standard workflows offered in darktable:
* [_scene-referred workflow_](edit-scene-referred.md): Here the emphasis is on doing as much processing as possible in the scene-referred part of the pipeline, and doing the dynamic range compression to display-referred space as late as possible. This is the preferred workflow for darktable. It uses the [_filmic rgb_](../../module-reference/processing-modules/filmic-rgb.md) module to perform the tone mapping compression.
* [_display-referred workflow_](edit-display-referred.md): This is the legacy workflow that was used by default in darktable prior to version 3.0. It performs the tone map compression much earlier in the pixelpipe, and many of the modules operate in display-referred space. It uses the [_base curve_](../../module-reference/processing-modules/base-curve.md) module to perform the tone mapping compression.

**Note:** when changing the preferences between scene-referred and display-referred workflow, the new setting will only apply for newly imported images. If you already imported an image using a different workflow setting, go to the [_history stack_](../../module-reference/utility-modules/darkroom/history-stack.md) in the darkroom view, select "original image", and click "compress history stack". This will discard any edits and reset the workflow for that image.

A third option is to set the workflow presets option to _none_. In this case, the scene-referred workflow module order will be used by default. The [_filmic rgb_](../../module-reference/processing-modules/filmic-rgb.md) and [_exposure_](../../module-reference/processing-modules/exposure.md) modules will not be applied automatically. It is up to the user to arrange for appropriate tone mappings and reorder the modules where required.
