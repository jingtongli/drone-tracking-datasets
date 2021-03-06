# Additional dataset info

## Ground truth synchronization parameters
We provide ground truth time shift (beta) and time scaling parameters (alpha) between the camera streams. 

### Time scale (alpha)
|Ref. camera | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- | --- | 
| 0 | 1.0000 |0.4983 |0.5005 |0.4999 |0.5000 |0.8342 |0.4171 |
| 1 | 2.0069 |1.0000 |1.0044 |1.0033 |1.0034 |1.6741 |0.8370 |
| 2 | 1.9981 |0.9956 |1.0000 |0.9989 |0.9989 |1.6667 |0.8334 |
| 3 | 2.0003 |0.9967 |1.0011 |1.0000 |1.0001 |1.6686 |0.8349 |
| 4 | 2.0002 |0.9966 |1.0011 |0.9999 |1.0000 |1.6685 |0.8343 |
| 5 | 1.1988 |0.5973 |0.6000 |0.5993 |0.5993 |1.0000 |0.5000 |
| 6 | 2.3975 |1.1947 |1.2000 |1.1978 |1.1986 |2.0000 |1.0000 |

### Time shift (beta)
|Ref. camera | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- | --- | 
| 0 | 0.00 |1156.29 |1128.78 |1219.88 |889.37 |3018.11 |-1562.26 |
| 1 | -2320.60 |0.00 |-32.64 |59.77 |-270.82 |1082.34 |-2529.59 |
| 2 | -2255.38 |32.50 |0.00 |92.38 |-238.21 |1136.75 |-2502.62 |
| 3 | -2440.13 |-59.56 |-92.46 |0.00 |-330.57 |982.64 |-2587.35 |
| 4 | -1778.91 |269.91 |238.46 |330.57 |0.00 |1534.20 |-2304.50 |
| 5 | -3618.11 |-646.52 |-682.02 |-588.87 |-919.51 |0.00 |-3071.00 |
| 6 | 3745.56 |3022.07 |3003.04 |3099.07 |2762.22 |6142.00 |0.00 |

Such that for each row: frame i in the reference camera corresponds to frame j = alpha * i + j in the other cameras.

The camera ID's correspond to the order of cameras in cameras.txt file.

### WARNING!
Unfortunately, some of the smartphone cameras were recording at a variable frame rate. It is a feature of those smarthpones and cannot be changed. In some cases the fluctuation in FPS was very high, e.g. Mate 7 and Mate 10 in this dataset. If this is a problem, we suggest to extract the timestamps of each frame using ffprobe using the following command:

```
ffprobe -select_streams v:0 -of default=noprint_wrappers=1:nokey=1 -show_entries  packet=pts_time filename.mp4
```

Having the timestamps for each frame, one can use them in their pipeline. For our purposes, we required a fixed frame rate input so we remapped the detected image points using linear interpolation such that they would be 30fps fixed frame rate.

The time mapping parameters in the tables above are also computed with the remapped frame rate of Mate 7 and Mate 10 to 30fps.

If in doubt, please contact us for details.
