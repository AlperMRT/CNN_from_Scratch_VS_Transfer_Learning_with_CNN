#%% md
In the first part, I implemented CNN classifier from scratch. I build up the model with different parameters and trained the model with them to compare each of them.
I used epochs=25; learning rates as 0.001, 0.0005, 0.0001; batch sizes as 32, 64; dropouts as 0.3, 0.5, 0.8 . I calculated loss and accuracy for each case and then visualized them to see results better.
For a general comment, most cases have a bit overfitting problem. The difference between training accuracy and validation accuracy is high, it shows that model has low ability to generalize. 
The accuracies are close for each case, but I got the best accuracy while learning rate is 0.0005. Test loss is lower while learning rate is 0.0001. For high learning rate, model optimized faster but it has highest test loss. 
Because of high running times, I tested model with 3 dropout values. Low dropout(0.3) value was ineffective against overfitting. Middle dropout value(0.5) generated the best results. High dropout value(0.8) caused low performance due to excessive dropout usage.
I also plotted confussion matrix for each case. As I seen from them: Class imbalance may have challenged the model. Even at the highest accuracy, some classes were not correctly predicted.
To get better results; more data may be used, data augmentation may be applied, increasing image quality may increase the accuracies, more optimal parameters may be used.

In the second part, I used pretrained vgg16 base model. We had to use the model in two different fine-tuning scenarios. Then, we had to train and test the models with the same data in part 1 and observe the results.
Fine tuning is optimizing weights of a pretrained model to adapt it to a new dataset. In this part, we did this processes:
1) Freezing Layers: The weights of the lower convolutional layers were frozen, allowing only the Fully Connected (FC) layers to be optimized. This preserves the feature extraction capabilities of the pre-trained model.
2) Modifying the Output Layer: The output layer was redefined to match the number of classes in the dataset, and its weights were randomly initialized.
3) Using FC Layers Only or Using Last Two Convolutional Layers + FC Layers: In Using FC only case, all convolutional layers were frozen, and only the FC layers were optimized. In Using Last Two Convolutional Layers + FC Layers case, the last two convolutional layers, along with the FC layers, were optimized.
used epochs as 15, batch_number as 32 and learning rate as 0.0005. I wanted to use higher epochs, but because of high running time and some computer issues, I could not increase epoch number. I also chose batch number and learning rate from part1's best results parameters.

Results with Only FC Layers:
Maximum training accuracy: 86.82%
Maximum validation accuracy: 62.56%
Signs of overfitting were observed towards the final epochs as validation loss increased.
Test accuracy: 61.81%
Test loss: 1.30

Results with Last Two Convolutional Layers + FC Layers:
Maximum training accuracy: 85.07%
Maximum validation accuracy: 63.66%
Validation loss was slightly lower compared to the first model, generated better generalization.
Test accuracy: 61.60%
Test loss: 1.25

Test accuracies are very close, but validation accuracy is slightly better. This may be show that more layers increase model's generalization ability. Also, second model's test loss is slightly less than the first one, so it may be show that second model is more stable.

Comparison with Part1:
In part1, the best test accuracy was 0.34. The lowest test loss was 2.24. So it shows that using transfer learning has huge positive effect on learning. Also test loss is much lower in transfer learning cases. However, even it was not a big problem like in the part1, overfitting is still there. I expected that the transfer learning models could have generalized better.

I used the same data in part1. As in part1, using more data, data augmentation, using more optimal parameters may increase the success of models. 
