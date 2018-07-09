
The Caffe-compatible files that you are probably looking for:

    SqueezeNet_v1.0/train_val.prototxt          #model architecture
    SqueezeNet_v1.0/solver.prototxt             #additional training details (learning rate schedule, etc.)
    SqueezeNet_v1.0/squeezenet_v1.0.caffemodel  #pretrained model parameters

If you find SqueezeNet useful in your research, please consider citing the [SqueezeNet paper](http://arxiv.org/abs/1602.07360):

    @article{SqueezeNet,
        Author = {Forrest N. Iandola and Song Han and Matthew W. Moskewicz and Khalid Ashraf and William J. Dally and Kurt Keutzer},
        Title = {SqueezeNet: AlexNet-level accuracy with 50x fewer parameters and $<$0.5MB model size},
        Journal = {arXiv:1602.07360},
        Year = {2016}
    }


Helpful hints:

1. **Getting the SqueezeNet model:** `git clone <this repo>`.
In this repository, we include Caffe-compatible files for the model architecture, the solver configuration, and the pretrained model (4.8MB uncompressed).

2. **Batch size.** We have experimented with batch sizes ranging from 32 to 1024. In this repo, our default batch size is 512. If implemented naively on a single GPU, a batch size this large may result in running out of memory. An effective workaround is to use hierarchical batching (sometimes called "delayed batching"). Caffe supports hierarchical batching by doing `train_val.prototxt>batch_size` training samples concurrently in memory. After `solver.prototxt>iter_size` iterations, the gradients are summed and the model is updated. Mathematically, the batch size is `batch_size * iter_size`. In the included prototxt files, we have set `(batch_size=32, iter_size=16)`, but any combination of batch_size and iter_size that multiply to 512 will produce eqivalent results. In fact, with the same random number generator seed, the model will be fully reproducable if trained multiple times. Finally, note that in Caffe `iter_size` is applied while training on the training set but not while testing on  the test set.

3. **Implementing Fire modules.** In the paper, we describe the `expand` portion of the Fire layer as a collection of 1x1 and 3x3 filters. Caffe does not natively support a convolution layer that has multiple filter sizes. To work around this, we implement `expand1x1` and `expand3x3` layers and concatenate the results together in the channel dimension.

4. **The SqueezeNet team has released a few variants of SqueezeNet**. Each of these include pretrained models, and the non-compressed versions include training protocols, too.

  SqueezeNet v1.0 (in this repo), the base model described in our SqueezeNet paper.

  [Compressed SqueezeNet v1.0](https://github.com/songhan/SqueezeNet_compressed), as described in the SqueezeNet paper.

  [SqueezeNet v1.0 with Residual Connections](https://github.com/songhan/SqueezeNet-Residual), which delivers higher accuracy without increasing the model size.

  [SqueezeNet v1.0 with Dense→Sparse→Dense (DSD) Training](https://github.com/songhan/SqueezeNet-DSD-Training), which delivers higher accuracy without increasing the model size.

  SqueezeNet v1.1 (in this repo), which requires 2.4x less computation than SqueezeNet v1.0 without diminshing accuracy.

5. **Community adoption of SqueezeNet**:

  [SqueezeNet in the *MXNet* framework](https://github.com/haria/SqueezeNet), by Guo Haria

  [SqueezeNet in the *Chainer* framework](https://github.com/ejlb/squeezenet-chainer), by Eddie Bell

  [SqueezeNet in the *Keras* framework](https://github.com/DT42/squeezenet_demo), by [dt42.io](https://dt42.io/)
  
  [SqueezeNet in the *Tensorflow* framework](https://github.com/vonclites/squeezenet), by Domenick Poster

  [SqueezeNet in the *PyTorch* framework](https://github.com/pytorch/vision/blob/master/torchvision/models/squeezenet.py), by Marat Dukhan

  [SqueezeNet in the *CoreML* framework](https://github.com/mdering/CoreMLZoo)

  [Neural Art using SqueezeNet](https://github.com/pavelgonchar/neural-art-mini), by Pavel Gonchar

  [SqueezeNet compression in Ristretto](https://arxiv.org/abs/1605.06402), by Philipp Gysel
  
**If you like SqueezeNet, you might also like SqueezeNext! ([SqueezeNext paper](https://arxiv.org/abs/1803.10615), [SqueezeNext code](https://github.com/amirgholami/SqueezeNext))**
