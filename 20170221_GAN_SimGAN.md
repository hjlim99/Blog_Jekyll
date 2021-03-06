SimGANs - a game changer in unsupervised learning, self driving cars, and more

> 출처 : https://getpocket.com/a/read/1595343739
> 코드 : https://github.com/wayaai/SimGAN

Apple’s Learning from Simulated and Unsupervised Images through Adversarial Training (S+U Learning) lays down the blueprint for training state-of-the-art neural nets from only synthetic and unlabelled data.
In this post we will see why this has huge potential, and apply it to an interesting problem: autonomous driving. We will refer to an implementation of SimGAN: https://github.com/wayaai/SimGAN,
> 애플이 제시한 S+U Learning기법은 새로운 학습 기법으로써 호응을 얻고 있다. 본 포스트를 통해서 잠재 가능성과, autonomous driving의 활용에 대하여 살펴 본다.

The core idea behind Apple’s S+U learning is that labelled data is often scarce and expensive. However, synthetic labelled data can be generated using powerful engines like Unity or with other methods.
> 기본아이디어는 labeled 된 데이터는 구하기 어려우니 synthetic labelled를 학습에 이용하자는 것이다.

The problem is that the gap between the synthetic and real datasets leads to a network trained on synthetic data not generalizing well enough to the real world. What S+U learning suggests is that with a real (and not necessarily labelled) dataset this gap can be bridged.
> 문제는 synthetic 데이터와 real데이터간의 `갭(Gap)`으로 인하여 학습시 synthetic데이터가 Real데이터로 잘 일반화(Generalizing)된다는 것이다. S+U Learning이 제시 하는 방법을 통해서 이러한 갭을 줄일수 있다.

A generator can learn to refine synthetic data (such that it’s closer to the real dataset’s distribution while maintaining the synthetic data’s annotations (i.e. it’s labels remain valid) through adversarial training.
> G는 adversarial training을 통해서 Refine synthetic 데이터를 가지고 학습할 수 있다.
> * Refine synthetic : closer to the real dataset’s distribution while maintaining the synthetic data’s annotations (i.e. it’s labels remain valid)

The following links will provide relevant code snippets for the concepts being explained. The refiner (generator) refines the synthetic data such that:
> Refiner(generator)는 synthetic data를 정제 한다.

1. 정제된 데이터와 synthetic데이터간의 차이점을 self-regularization loss term을 통해서 최소화 함으로써 Anotation을 유지 한다.Annotations are preserved by minimizing the difference between the refined and synthetic data with a self-regularization loss term.
2. synthetic 데이터가 Real 데이터가 된다. (기본 GAN컨셉) The synthetic data looks real (standard concept of GANs).

```
def refiner_network(input_image_tensor):
    """
    The refiner network, Rθ, is a residual network (ResNet). It modifies the synthetic image on a pixel level, rather
    than holistically modifying the image content, preserving the global structure and annotations.
    :param input_image_tensor: Input tensor that corresponds to a synthetic image.
    :return: Output tensor that corresponds to a refined synthetic image.
    """
    def resnet_block(input_features, nb_features=64, nb_kernel_rows=3, nb_kernel_cols=3):
        """
        A ResNet block with two `nb_kernel_rows` x `nb_kernel_cols` convolutional layers,
        each with `nb_features` feature maps.
        See Figure 6 in https://arxiv.org/pdf/1612.07828v1.pdf.
        :param input_features: Input tensor to ResNet block.
        :return: Output tensor from ResNet block.
        """
        y = layers.Convolution2D(nb_features, nb_kernel_rows, nb_kernel_cols, border_mode='same')(input_features)
        y = layers.Activation('relu')(y)
        y = layers.Convolution2D(nb_features, nb_kernel_rows, nb_kernel_cols, border_mode='same')(y)

        y = layers.merge([input_features, y], mode='sum')
        return layers.Activation('relu')(y)

    # an input image of size w × h is convolved with 3 × 3 filters that output 64 feature maps
    x = layers.Convolution2D(64, 3, 3, border_mode='same', activation='relu')(input_image_tensor)

    # the output is passed through 4 ResNet blocks
    for _ in range(4):
        x = resnet_block(x)

    # the output of the last ResNet block is passed to a 1 × 1 convolutional layer producing 1 feature map
    # corresponding to the refined synthetic image
    return layers.Convolution2D(1, 1, 1, border_mode='same', activation='tanh')(x)
```

The refiner takes as input a synthetic data sample, and outputs a refined sample of the same dimension(s).
> refiner는 입력값으로 synthetic 데이터 샘플을 취하고, 아웃풋으로 Refined 샘풀을 생성한다.

The discriminator takes as input a data sample and classifies it as refined or real.
> discriminator는 입력으로 데이터 샘플을 취하고, 아웃풋으로 Refined인지 Real인지 분류값을 생성한다.

The GAN architecture and training procedure is standard, but S+U Learning suggests two simple and intuitive methods for improving the quality of generated data that applies to GANs in general.
> GAN의 구조 및 학습 절차는 정해져(Standard)있다. 하지만, S+U Learning은 생성데이터의 질 향상을 위하여 2가지 다른 방법을 제안하고 있다.
1. In current GAN architectures, discriminators are only trained on data generated by the most current generator. This leads to it forgetting features of previously generated data, and means the generator can reintroduce features to trick the discriminator. Generated data is generated data and should always be classified by the discriminator as such. A history buffer of previously generated data can be used so that the discriminator is trained on data from the current generator, along with data from past generators.
2. In current GAN architectures, discriminators classify data as real/generated by analyzing the input data globally. This means the generator can get away with introducing some local artifacts in the generated data to trick the discriminator. Since any local patch of data should look real, the discriminator should instead break the data into local patches and classify each patch as real/generated, averaging these local adversarial losses for a more balanced global adversarial loss.


## 적용 예

https://itunes.apple.com/us/app/dash-train-self-driving-cars/id1146683979?ls=1&mt=8
https://youtu.be/iCjNBGDeQJ4

Imagine you’re comma.ai, and you have a large amount of real unlabelled driving data collected by [Dash](https://itunes.apple.com/us/app/dash-train-self-driving-cars/id1146683979?ls=1&mt=8)[^1].

While your current method of labelling data is awesome, it’s not quite cutting it, and you only have a small subset of labelled data.

Using a SimGAN, you could train a refiner network to refine synthetic data from Grand Theft Auto such that it looks like it came from the distribution of your real dataset and it’s annotations are preserved. Now you can train your production models on this nearly unlimited refined labelled dataset, and use your smaller real labelled dataset as validation/test.

I haven’t taken any of the self driving car courses out there, but I’ve seen that they use GTA and simulated environments to train their models. With a technique like this, their software could be closer to real world ready.

There seem to be many possible applications of SimGANs in the real world and autonomous driving is just an interesting one I chose to use as an example.

---
[^1]: 아이폰 App.
