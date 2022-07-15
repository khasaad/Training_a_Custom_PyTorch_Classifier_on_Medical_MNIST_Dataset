# Training a Custom PyTorch Classifier on Medical MNIST Dataset
<p>This project is a solution to one of the projects at <a href="https://www.nvidia.com/fr-fr/">Nvidia</a>.</p>
<p><B>Key words</B>: Classification radio images, PyTorch, CNN, MNIST Medical dataset</p>

<h3>Context of the project</h3>

<p>A start-up has won a call for tenders to produce a POC (Proof Of Concept) for an AI solution capable of classifying radio images into six categories.</p>

<p>My objective as an IA developer is to prove the technical skills of the start-up to carry out this project and to get the medical profession to join the Health Data Hub project.</p>

<p>As the Health Data Hub is being implemented, the company uses the MedNIST dataset. In this project, we will classify images from the MNIST medical dataset. In fact, we are going to train a custom PyTorch classifier on the MNIST Medical dataset.</p>

<p>The dataset available for image classification consists of images stored in corresponding folders. For example, our dataset consists of 6 types of images and they are stored in corresponding folders.</p>

<p>We will use Kaggle's MNIST Medical dataset to train our custom PyTorch image classifier. All images are 64×64 grayscale images.</p>

<p>The MNIST Medical dataset contains 58954 images with dimensions 64×64. All images are in grayscale format and there are 6 classes in total. They are:</p>
<ul>
<li>AbdomenCT – 10000 images</li>
<li>BreastMRI – 8954 images</li>
<li>CXR (Chest X-Ray) – 10000 frames</li>
<li>ChestCT – 10000 images</li>
<li>Hand – 10000 images</li>
<li>HeadCT – 10000 images</li>
</ul>

<h3>Architecture of our CNN model for classification</h3>

<p>In our model, there are 4 CNN blocks, and each block consists of a convolution layer and a max-pooling layer. Each layer should produce the same number of nodes as the next layer.</p>

<p>The Relu activation function is used to remove negative values ​​from the feature map because there cannot be negative values ​​for any pixel value. Stride(2,2) used and the padding is also 1.</p>

<p>After applying the convolution and extracting features from the image, a flatten layer is used to flatten the tensor. The flatten layer converts the tensor to one-dimensional. Then 2 linear added to reduce tensor size and learn features, and a dropout added to avoid overfitting. The final layer should have exit nodes equal to the number of labels used.</p>

<p>Finally, added pooling average and that it is effective when we want to detect weak signals.</p>

<p>In this case, the stride and the size of the kernel are automatically selected to adapt to the needs.</p>

<h3>Model training</h3>

<p>First, we define the training hyperparameters. The learning rate reflects the degree to which the model is updated in batches. In our model, it is equal to 0.001, the training time lasted 17.5 hours (Compute device: CPU). We cannot adjust the learning rate too large, the weights will be adjusted too much and will miss the true minimum loss, or even become unstable.</p>

<p>We have defined 20 epochs to train the model. An epoch corresponds to learning on all the data.</p>

<p>We divide the data into 70% training, 20% validation, and 10% testing.</p>

<p>We use validation data to avoid overtraining in our model. Training and validation data are taken from the same dataset. Therefore, the model should have a similar loss for both.</p>

<p>Next, we cycle through the batches. We exclude the information accumulated in the optimizer, feed the batch by the model and calculate the loss for a batch. We use cross entropy (calculating the difference between two probability distributions), a common metric for classifiers.</p>

<p>This loss is added to a running total for the time, and then we apply Backpropagation. The optimizer then takes a step and updates the weights.</p>

<p>After all the training batches are complete, the same process happens for the validation data, without the backpropagation and optimization steps.</p>

<p>The average loss is calculated and we compare the validation loss against the training loss to test overfitting.</p>

<p>Here we obtain very good results for such a simple model. The final validation loss is 0.003 and the validation accuracy is 99.89%. This means that the model predicts almost everything correctly.</p>

<div class="row">
  <div class="column">
    <img src="https://github.com/khasaad/Training_a_Custom_PyTorch_Classifier_on_Medical_MNIST_Dataset/blob/main/outputs/accuracy.png" alt="Accuracy graph after training the model on the dataset" style="width:100%">
  </div>
  <div class="column">
    <img src="https://github.com/khasaad/Training_a_Custom_PyTorch_Classifier_on_Medical_MNIST_Dataset/blob/main/outputs/loss.png" alt="Model Training Loss Graph" style="width:100%">
  </div>
</div>

<p>The graphs also show minimal fluctuations in the lines. It seems like it's practically possible to get 100% validation accuracy with a bit more training by using a learning rate planner.</p>
