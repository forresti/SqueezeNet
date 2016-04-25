

**Our goal with SqueezeNet_v1.1 is to decrease the computational cost without degrading accuracy.**

Compared to v1.0, this version has two main changes:

1. Fewer and smaller filters in conv1 layer.
2. Pooling/downsampling layers are placed "earlier" in the network.

More details:

|     | v1.0 | v1.1 |
| --- | --- | --- |
conv1:          | 96 filters of resolution 7x7   | 64 filters of resolution 3x3
pooling layers: | pool{1,4,8,10}                  | pool{1,3,5,10}



