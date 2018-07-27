## SUNCG Dataset

[SUNCG website](http://suncg.cs.princeton.edu/)  
[SUNCG toolbox](https://github.com/shurans/SUNCGtoolbox)  
[2017, CVPR, Semantic Scene Completion from a Single Depth Image](https://arxiv.org/pdf/1611.08974v1.pdf)

* SUNCG is an ongoing effort to establish a richly-annotated, large-scale dataset of 3D scenes. The dataset contains over 45K different scenes with manually created realistic room and furniture layouts. All of the scenes are semantically annotated at the object level.

**Toolbox Usage**

- Viewing the scene (requires compiling with GPU)
```
cd data_root/house/<sceneid>/
gaps/bin/x86_64/scnview house.json -v 
```
if meet the error: `Segmentation fault (core dumped)`, run `export LD_PRELOAD=/lib/x86_64-linux-gnu/libpthread.so.0` before the comment.

* Camera Controls

Left click: Orbit view  
Right click: Pan view  
Mouse wheel: Zoom view  
Double click on an object to change the viewer's rotation center  
Other function keys  

"b": show back faces  
"h": show bounding boxes  
"c": show cameras  
"e": show edges  
"a": show axes  
"Esc": exit program  
"Space": print out current camera  
