# Sratch_NeuralNet![](vertopal_0d0000b520c3414ea2c48e1a64f1534c/media/image1.png){width="1.9680544619422573in"
height="1.8736111111111111in"}

Assignment I

> Deep Learning for Computer Vision(CS776) Indian Institute of
> Technology,Kanpur, INDIA-208 016
>
> Piyush Gangle (21111046)\
> piyushg21\@iitk.ac.in

February 3, 2022

**Contents**

+-------+------------------+------------------+------------------+---+
| **1** | > **CNN          | **2**            |                  |   |
|       | > architecture   |                  |                  |   |
|       | > used**         |                  |                  |   |
+=======+==================+==================+==================+===+
| **2** | 1.1              | > Notations used | . . . . . . . .  | 2 |
|       |                  |                  | . . . . . . . .  |   |
|       |                  |                  | . . . . . . . .  |   |
|       |                  |                  | . . . . . . . .  |   |
|       |                  |                  | . . . .          |   |
+-------+------------------+------------------+------------------+---+
|       | > **Math used to | **3**            |                  |   |
|       | > design Neural  |                  |                  |   |
|       | > network**      |                  |                  |   |
+-------+------------------+------------------+------------------+---+
| **3** | 2.1              | > Forward        | 3                |   |
|       |                  | > Propagation .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . .        |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 2.2              | > Softmax . . .  | 3                |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . .            |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 2.3              | > Cost function  | 3                |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . .            |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 2.4              | Backpropagation  | > . . . . . . .  | 3 |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
+-------+------------------+------------------+------------------+---+
|       | 2.5              | > Updating       | 3                |   |
|       |                  | > Parameters . . |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . .          |                  |   |
+-------+------------------+------------------+------------------+---+
|       | > *              | **4**            |                  |   |
|       | *Backpropagation |                  |                  |   |
|       | > equation       |                  |                  |   |
|       | > derivation**   |                  |                  |   |
+-------+------------------+------------------+------------------+---+
| **4** | 3.1              | Cost function    | > . . . . . . .  | 4 |
|       |                  | derivation       | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . .          |   |
+-------+------------------+------------------+------------------+---+
|       | 3.2              | > Carrying out   | 5                |   |
|       |                  | > calculation    |                  |   |
|       |                  | > further . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . .          |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 3.3              | > Derivation of  | 6                |   |
|       |                  | > ReLU . . . . . |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > .              |                  |   |
+-------+------------------+------------------+------------------+---+
|       | > **Tuning       | **6**            |                  |   |
|       | > parameters**   |                  |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 4.1              | > Unaugmented    | 6                |   |
|       |                  | > data-set . . . |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > . . . . . . .  |                  |   |
|       |                  | > .              |                  |   |
+-------+------------------+------------------+------------------+---+
|       | 4.2              | Augmented        | > . . . . . . .  | 6 |
|       |                  | data-set         | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . .      |   |
+-------+------------------+------------------+------------------+---+
|       | 4.3              | Observation :    | > . . . . . . .  | 6 |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . . . . . . .  |   |
|       |                  |                  | > . .            |   |
+-------+------------------+------------------+------------------+---+

1

**1** **CNN architecture used**

Neural network used has input layer with 512 neurons, single hidden
layer is used having 64 neurons and output layer 10 neurons.ReLU
activation funtion is used for hidden layers and Softmax activation
function is used for output layers.

![](vertopal_0d0000b520c3414ea2c48e1a64f1534c/media/image2.png){width="6.25in"
height="3.8625in"}

Figure 1: Diagrammatic representation of Neural network

**1.1** **Notations used**

> 1\. m: total number of obrservations = 50000
>
> 2\. *n*0: number of neurons in input layer = 512
>
> 3\. *n*1: number of neurons in hidden layer = 64
>
> 4\. *n*2: number of neurons in output layer = 10
>
> 5\. Shape of *W*1 : (*n*1*, n*0) = 64 *×* 512
>
> 6\. Shape of *W*2 : (*n*2*, n*1) = 10 *×* 64
>
> 7\. Shape of *B*1 : (*n*1*,* 1) = 64 *×* 1
>
> 8\. Shape of *B*2 : (*n*2*,* 1) = 10 *×* 1

2

+-------+-----------------------------+-----------------------------+
| **3** | **3** **Backpropagation     |                             |
|       | equation derivation**       |                             |
+=======+=============================+=============================+
|       | > • Loss = *−*�*n           | > *dw*2for multi class      |
|       | > i*=*k*\[*yk∗              | > classifcation in our case |
|       | > log*(*ak*)\]• *ai* =      | > we have 10 *∂loss*        |
|       | > *ezi* �*n i*=*kezk*• Our  |                             |
|       | > purpose is to fnd *dZ*2 = |                             |
+-------+-----------------------------+-----------------------------+
|       | > difrent classes. to       |                             |
|       | > fnd*∂lossdw*2, we need to |                             |
|       | > fnd *∂ai∂zj*but           |                             |
|       | > *∂ai∂zj*will be diferent  |                             |
|       | > for 2 cases.              |                             |
+-------+-----------------------------+-----------------------------+
|       | > 1\. Case 1 : *i* = *q*    | > �*k*=*iezk*               |
|       | > *ezi* *−→∂ai* *∂*\        | >                           |
|       | > *ezj*+� *∂zj*=*∂zj*\[     | > �*n k*=1*ezk*             |
|       | > *k*=*j*\[*ezk*\]\]        |                             |
|       | > (*ezj*+� *∂zj*\[*ezj* +�  |                             |
|       | > *∂* *∂*                   |                             |
|       | > *k*=*j*\                  |                             |
|       | [*ezk*\])*∂zj*(*ezi*)*−ezi* |                             |
|       | > *k*=*jezk*\] *−→*         |                             |
|       | > (*ezj*+�*k*=*jezk*)2      |                             |
|       | > *−→∂ai* (� 0*−eziezj∂zj*= |                             |
|       | > *k*=*iezk*) *ezi* *ezj*\  |                             |
|       | > *−→ −*(�*k*=*iezk*)       |                             |
|       | > *×*(�*k*=*iezk*)\         |                             |
|       | > *−→*= *−ai.aj*\           |                             |
|       | > 2. Case 2 : *i* = *q*\    |                             |
|       | > *ezi*\                    |                             |
|       | > *−→∂ai* *∂* *ezi*+�       |                             |
|       | > *∂zi*=*∂zi*\[             |                             |
|       | > *k*=*i*\[*ezk*\]\]        |                             |
|       | > (*ezi*+� *∂zi*\[*ezi*+�   |                             |
|       | > *∂* *∂*                   |                             |
|       | > *k*=*i*\                  |                             |
|       | [*ezk*\])*∂zj*(*ezi*)*−ezi* |                             |
|       | > *k*=*iezk*\] *−→*         |                             |
|       | > (*ezi*+�*k*=*jezk*)2      |                             |
|       | > (*ezj*+�*k*=*j*\[*ezk*\]  |                             |
|       | )(*ezi*)*−*(*ezi*)(*ezi*+0) |                             |
|       | > *−→* (*ezi*+�*k*=*iezk*)2 |                             |
|       | > *ezi* �*k*=*iezk* *−→∂ai* |                             |
|       | > � � *∂zi*= *k*=*iezk*)    |                             |
|       | > *k*=*iezk*) We know that  |                             |
|       | > : *ai* = *ezi* �*n        |                             |
|       | > k*=1*ezk* &(1 *− ai*) =   |                             |
|       | > *−→*= *ai*(1 *− ai*)      |                             |
+-------+-----------------------------+-----------------------------+

+---------+--------------------------------+-------+---+
| **3.1** | > =*⇒* Thus,                   | *∂ai* | = |
+=========+================================+=======+===+
|         |                                | *∂zj* |   |
+---------+--------------------------------+-------+---+
|         | > **Cost function derivation** |       |   |
+---------+--------------------------------+-------+---+

> �-a*i.aj,* if(i *̸*= *j*) a*i.*(1 *− ai*)*,* *if*(*i* = *j*)

*−→[∂L]{.ul}* � *[∂]{.ul}*\
*∂zi*=*∂zi*\[*−yilog*(*ai*) *−* *k*=*iyk.log*(*ak*)\]\
*−→~~−~~[yi]{.ul}* *∂zi−* � *[yk ∂ak]{.ul}*\
*ai. ~~∂a~~[i]{.ul}* *k*=*i ak∂zi−→~~−~~[yi]{.ul}ai.ai*(1 *− ai*) + �
*[yk]{.ul}* *k*=*i ak.ak.ai−→ −yi* + *yi.ai* + *ai*�*k*=*iyk*\
*−→ −yi* + *ai*\[*yi*�*k*=*iyk*\]

4

*−→ −yi* + *ai*\[*yi*�*n k*=1*yk*\
*−→ we − know − that*�*n k*=1*yk*= 1\
*−→ Hence*\
= *−yi* + *ai*(1)

= *ai − yi*\
=*⇒ thus* :*[∂L]{.ul}∂z*3= *a*3 *− y*\
=*⇒ thus* : *dZ*3 =*[∂Cost]{.ul}∂W*3= *A*3 *− Y*

**3.2** **Carrying out calculation further**

Calulation for*[∂Cost]{.ul}dW*2& *~~∂Cost~~*\
*−→* as we know that

> *da*3*∗ ~~da~~*[3]{.ul}*−→* *dz*3= *~~∂L~~∂z*3= *dZ*3
>
> *−→[∂Z]{.ul}*[3]{.ul}*∂a*2= *~~partial~~∂a*2(*W*3*.a*2 + *B*3) = *a*2
>
> *−→[∂a]{.ul}*[2]{.ul}*∂Z*2= *f ′*2(*Z*2)
>
> *−→[∂Z]{.ul}*[2]{.ul} *[∂]{.ul}* *∂W*2=*∂W*2(*W*2*.a*1 + *B*2) = *a*1
>
> *−→dZ*2 =*[∂Cost]{.ul}∂Z*2= (*W*3)*T.dZ*3 *∗ f ′*2(*Z*2)

=*[⇒]{.ul}*Hence ,\
*∂W*2= *~~∂L~~∂a*3*× ~~∂a~~*[3]{.ul}*∂Z*3*× ~~∂Z~~*[3]{.ul}*∂a*2*×
~~∂a~~*[2]{.ul}*∂Z*2*× ~~∂Z~~*[2]{.ul}

= *dZ*3*.W*3*.f′*2(*Z*2)*.a*1

> *[∂Cost]{.ul}*\
> *∂W*2= ~~1~~*m*\[(*W*3)*T.dZ*3 *∗ f ′*2(*Z*2)\](*A*1)*T*

= [1]{.ul}

=*⇒* Similarly for Bias

> *[∂Cost]{.ul}*\
> *∂B*2= ~~1~~*mSum*(*dZ*2*,* 1)

5

> **3.3** **Derivation of ReLU**
>
> we have used ReLU activation function in hidden layer so it is
> neccesary to calculate derivative of it.

*f*(*z*) =

*f′*(*z*) =

+---------+--------------------------+
| **4**   | > **Tuning parameters**  |
+=========+==========================+
| **4.1** | **Unaugmented data-set** |
+---------+--------------------------+

> 1\. Epochs : 20000
>
> 2\. Learning rate : 0.7
>
> 3\. Training dataset accuracy : 42.35%
>
> 4\. Test dataset accuracy : 41.42%
>
> **4.2** **Augmented data-set**
>
> 1\. Epochs : 10000
>
> 2\. Learning rate : 0.7
>
> 3\. Training dataset accuracy : 41.51%
>
> 4\. Test dataset accuracy : 40.38%
>
> **4.3** **Observation :**

+---+--------+------------+
| � | > *x,* | > *x \>* 0 |
+===+========+============+
|   | > 0*,* | > *x ≤* 0  |
+---+--------+------------+
| � | > 1*,* | > *x \>* 0 |
+---+--------+------------+
|   | > 0*,* | > *x ≤* 0  |
+---+--------+------------+

> On un-augmented data-set we got 42.35% training accuracy but on
> augmented data-set we got 41.51% training accuracy. We observed that
> there is slightly degradation in performance on augmented data-set.On
> augmented data-set we had performed image cutout,crop,rotate which
> makes it difficult to identify image thus we got less performance.
>
> **References**
>
> \[1\] Neural network : https://www.youtube.com/watch?v=vtx1iwmOx10
>
> \[2\] Neural network : https://youtu.be/f-nW8cSa*Ec*

\[3\] Neural network : https://youtu.be/URJ9pP1aURo

\[4\] Image Rotation :
https://gautamnagrawal.medium.com/rotating-image-by-any-angle-shear
transformation-using-only-numpy-d28d16eb5076

6

\[5\] https://www.cs.toronto.edu/ kriz/cifar.html

\[6\]
https://github.com/deep-diver/CIFAR10-img-classification-tensorflow

\[7\]
https://towardsdatascience.com/cifar-10-image-classification-in-tensorflow-5b501f7dc77c

\[8\]
https://towardsdatascience.com/backpropagation-from-scratch-how-neural-networks-really
work-36ee4af202bf

\[9\]
https://machinelearningmastery.com/implement-backpropagation-algorithm-scratch-python/

\[10\]
https://www.kaggle.com/wwsalmon/simple-mnist-nn-from-scratch-numpy-no-tf-keras

7
