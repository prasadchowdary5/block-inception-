The LeNet architecture used 5x5 convolutions, AlexNet used 3x3, 5x5, 11x11 convolutions and VGG used some other mix of 3x3, and 5x5 convolutions. But the questions that deep learning scientists were worried about were which combination of convolutions to use in different datasets to get the best results.

For example, if we pick 5x5 convolutions, we end up with a fair number of parameters, there are a lot more multiplications involved, and they need a lot of parameters and are very slow, but on the other hand, it is very expressive. But if we pick 1x1 convolutions, it is much faster and does not need much memory, but maybe it does not work so well. Keeping these questions in mind, a brilliant idea was proposed in the Google LeNet paper — why not just pick them all, and stack them up in various convolutional blocks. It is also called the Inception paper, based on the movie Inception, and its famous dialogue — ‘we need to go deeper’.

Link to Inception paper — https://arxiv.org/abs/1409.4842

Inception Blocks:


Figure 2. The Inception Block (Source: Image from the original paper)
The inception block has it all. It has 1x1 convolutions followed by 3x3 convolutions, it has 1x1 convolutions followed by 5x5 convolutions, it has a 3x3 max pool layer followed by a 1x1 convolutions and it has a single 1x1 convolution. The idea is that if we use all the convolutions and pooling in a block, some of them will be efficient enough to extract some meaningful information from the images. To make sure that the image dimensions are maintained, the 3x3 convolutions have a padding of 1, and the 5x5 layer has a padding of 2 so that the input and the output images have the same size. And finally, they are all stacked together.


Figure 3. The first Inception Block (Source: Image created by author)
The number of filters in each layer in the Inception blocks are designed in such a way that we get the desired number of channels as the output for the next block. For example, in the first inception block, as shown in Figure 3, the total number of channels add up to 256.


Table 1. Inception blocks vs 3x3 and 5x5 Convolutional blocks — to create 256 output channels (Source: Image created by author)
The Inception blocks are designed in such a way that they need fewer parameters and less computational complexity than a single 3x3 or 5x5 convolutional layer, as shown in Table 1. If we were to have 256 channels in the output layer, Inception needs only 16,000 parameters and costs only 128 Mega FLOPS, whereas a 3x3 convolutional layer will need 44,000 parameters and cost 346 Mega FLOPS, and a 5x5 convolutional layer will need 1,22,000 parameters and cost 963 Mega FLOPS. So Inception blocks, essentially get the same job done as single convolutional layers, with much better memory and compute efficiency.

Inception Network Simplified:

 Inception Network Simplified (Source: Image created by author)
If we see Figure 1, then the Inception network can seem pretty intimidating. So to simplify the network Figure 4 is created. Figure 4 is exactly the same as figure 1, but the entire architecture is represented as blocks. Figure 4 shows that the inception network is no different than a normal vanilla network that we already know. The Inception network has 5 stages.
Stage 1 and 2 of the Inception network (Source: Image created by author)
The network starts with an image size of 224x224x3. Then it goes through a 1x1 Conv, 3x3 MaxPool, 1x1 Conv, 3x3 Conv, and a 3x3 MaxPool, and results in an image of size 192x28x28.

This part of the network is very similar to AlexNet, except that the image size in AlexNet is further reduced to 256x12x12.

Stage 3:


Figure 6. Stage 3 of the Inception network (Source: Image created by the author)
As we see in Figure 6, stage 3 has two Inception blocks and in the end a Max Pool layer. But the inception blocks do not have the same channel allocation, as seen in the figure. Block 1 has 256 channels, whereas block 2 has 480 channels. So the input image of 192x28x28 now becomes 480x14x14, after the two inception blocks and the MaxPooling layer.

Stage 4 and 5:

Stage 4 and 5 are very similar to stage 3. Stage 4 has 5 inception blocks followed by a MaxPool, and stage 5 has 2 inception blocks followed by a GlobalAveragePool.

Stage 4

Input image size — 480x14x14

Inception Block 1–512 channels (increased output channel)

Inception Block 2–512 channels

Inception Block 3–512 channels

Inception Block 4–512 channels

Inception Block 5–832 channels (increased output channel)

Output image size after Max Pool — 832x7x7

Stage 5

Input image size — 832x7x7

Inception Block 1–832 channels

Inception Block 2–1024 channels (increased output channel)

Output image size after GlobalAvgPool — 1024x1x1

So this is the Inception or GoogleLeNet architecture that was originally published. But later the architecture has been further improved in various different versions v2, v3, and v4.

Inception V2 — Add batch normalization

Inception V3 — Modified inception block (

replace 5x5 with multiple 3x3 convolutions (Figure 7),

replace 5x5 with 1x7 and 7x1 convolutions (Figure 8),

replace 3x3 with 1x3 and 3x1 convolutions (Figure 9),

have deeper stacks)
