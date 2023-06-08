# S6-Assignment Part 2



1. I have used 4 blocks for the CNN architecture with total ~17K parameters.
   1. First block captures edges and gradients upto receptive field of 7 pixels. With number of channels output = 16 and padding = 1 followed by Relu activation, batch normalization and dropout total 3 times. Finally maxpool is used at the end.
   2. Next block captures parts of objects upto 26 pixel of receptive field. Here also number of channel output = 16 but no padding followed by Relu activation, batch normalization and dropout total 3 times. Finally maxpool is used at the end.
   3. Next block captures the whole object and here the receptive field = 30 so the whole image is being seen in the last convolution. Here number of channel output = 32 without padding followed by Relu activation, batch normalization and dropout.
   4. Lastly, the block has 1x1 convolution to filter the channels into 10 outputs and then using GAP we average all the remaining image get the final 10 outputs.
2.  I have also used data transforms or image augmentation like randomcrop applied 10% of time and then resized to original size, random rotation, and then converted to tensor and normalized using mean and standard deviation of dataset.
3. LR = 0.01 is used and total 15 epochs are run to get final validation accuracy of 99.51%
