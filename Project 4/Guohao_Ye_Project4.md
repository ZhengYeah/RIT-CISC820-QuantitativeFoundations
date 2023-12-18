## Eigenface Extraction

Q1: How do the (leading) eigenfaces look like as an image? How does the importance of the eigenfaces decrease?

The leading eigenfaces look like human faces in this dataset. As the ranking of the eigenfaces decrease, they contribute less to human-face features.

We show several examples of the eigenfaces:

![Picture3](C:\Users\17911\Desktop\RIT-CISC-820-Quantitative-Foundation-Assignments\Project 4\Picture3.png)

## Face Reconstruction with PCA

Eigenfaces can be used to compress the original face image. As the number of eigenfaces used increasing, the reconstruction quality gets better. 

We show the results of using the first $n$ eigenfaces to reconstruct the first image (/s1/1.pgm):

![Picture2](C:\Users\17911\Desktop\RIT-CISC-820-Quantitative-Foundation-Assignments\Project 4\Picture2.png)

Q2: How many eigenfaces are required to recover an original face with reasonable errors?

**This dataset requires about at least 200 eigenfaces.** We calculated the $L_2$ distance between the first reconstructed face image and its original, the results are shown bellow. 

<img src="C:\Users\17911\Desktop\RIT-CISC-820-Quantitative-Foundation-Assignments\Project 4\Picture6.png" alt="Picture6" style="zoom: 25%;" />

We can see that when using more than 250 eigenfaces, the $L_2$ distance is almost zero.

## Face Classification

We use eigenfaces to perform the face classification task. The key idea is that we assume human-face image can be represented by a linear combination of the eigenfaces. Then each class can be linearly represented by the eigenfaces. The coefficient matrix $W$ can be obtained by solving the linear system. The following figure shows the intuition.

![Picture4](C:\Users\17911\Desktop\RIT-CISC-820-Quantitative-Foundation-Assignments\Project 4\Picture4.png)

For this task, we use $200$ eigenfaces, so $W$ is a $35\times 200$ matrix. Applying $W$ to a transformed test image will produce the scores for the $35$ classes. The maxima's according class is the predicted class.

**The test accuracy on the 35 classes (70 images) is 98%**, which means it can correctly classify almost all the faces.

## Face Recognition

To recognize an image is whether human face or not, we observe the classification scores of it using the trained model in the above task. If the maximum score of an input image is below a threshold, we think it a non-face image.

The average score of the testing image (total 120) in this task is $0.5317$. So we heuristically choose $0.5$ as the threshold.

<img src="C:\Users\17911\Desktop\RIT-CISC-820-Quantitative-Foundation-Assignments\Project 4\Picture9.png" alt="Picture9" style="zoom: 15%;" />

**In practice, this method performs not good.** The above figure shows three examples. For the middle Butt face, it gives almost the same score as the first att-face. Other images we do not include here even have much higher scores.

## Classification with ResNet

Besides the above method. We design a ResNet neural network to perform image classification. We split images from all classes into training and test sets by 8:2. For the training set, we use 10% samples for validation. So the training, validation, and test set have 288, 32, and 80 samples respectively.

The following left figure shows the training and validation accuracy w.r.t the iteration; the right figure shows the confusion matrix (matching matrix of the prediction and the truth) of the test set.

<img src="C:\Users\17911\Desktop\resnet.png" alt="resnet" style="zoom: 25%;" />

Our ResNet model achieves 98.75% accuracy on test set. From the right figure we can see that only one image is mis-classified.
