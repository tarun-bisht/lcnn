# Training Low Curvature Neural Networks

This is the reference implementation of the NeurIPS 2022 paper [*Efficient Training of Low-Curvature Neural Networks*](https://openreview.net/forum?id=2B2xIJ299rx) by Suraj Srinivas, Kyle Matoba, Himabindu Lakkaraju, & François Fleuret.

This codebase contains (a) model definitions and regularizers to train LCNNs, and (b) code to evaluate model curvature of trained models.

## Training LCNNs 
To train an LCNN with gradient norm regularization, use:

```
python train_models.py 
      --model-arch=resnet18lcnn 
      --regularizer=curvature_and_gnorm 
      --dataset=cifar100
```

Or to just train a vanilla LCNN, use: 

```
python train_curvature.py 
      --model-arch=resnet18lcnn 
      --regularizer=curvature 
      --dataset=cifar100
```

For other options, e.g. other datasets, architectures, etc, try `python3 train_curvature.py --help`. 

## Estimate Curvature
To estimate the empirical curvature of a model on a dataset using the power method, try 

```
python evaluate.py 
    --model-arch=resnet18lcnn
    --model-filename=<type-model-filename-with-path-here>
    --dataset=cifar100
    --num-power-iter=10
    --data-fraction=0.1
```

Note: for fast computation, we use a small fraction of the dataset specified in `data-fraction`

## Minimal Recipe
To build LCNNs of your own, you can try a minimal recipe we found to work on image datasets:
1. Build models using [ $\beta$-centered softplus](https://github.com/kylematoba/lcnn/blob/main/models/psoftplus.py) 
2. Apply (large) weight decay to $\beta$ 
3. Train models using [gradient norm regularization](https://github.com/kylematoba/lcnn/blob/main/regularized_loss.py#L29)

However, note that we mention this only for convience, and that this recipe is not supported by our theory, indicating that it may break for exotic architectures or domains.

## Research
If you found our work helpful for your research, please do consider citing us:

```
@inproceedings{
srinivas2022efficient,
title={Efficient Training of Low-Curvature Neural Networks},
author={Suraj Srinivas and Kyle Matoba and Himabindu Lakkaraju and Fran{\c{c}}ois Fleuret},
booktitle={Advances in Neural Information Processing Systems},
editor={Alice H. Oh and Alekh Agarwal and Danielle Belgrave and Kyunghyun Cho},
year={2022},
url={https://openreview.net/forum?id=2B2xIJ299rx}
}

```

