# EVA5-Assignments

The EVA is one of the most exhaustive and updated Deep Vision Program in the world! It is spread over three semester-style phases, each restricted by a qualifying exam.
This repo constitute the assignment of the first phase of the program which revolves around object recognition, detection and segmentation applications using the pytorch framework. 

Let's start with the description of each task, its challenges and solution provided by me in terms of the neural network, techniques used and optimization performed.

### S1 Assignment :

    Task: Elucidate your understaning about basic fundamentals of image namely channels, kernels alongwith Convolution operations, loss backpropagation and how network learns 
    during training.
    
    Solution: A thorough description has beem written in the assignment01.md file about fundamental concepts of DNN and operations like convolution and Backprop.
    
### S2 Assignment :

    Task: Quiz on convolution operation using different kernel sizes, fundamental concepts of receptive fields, calculation of kernel parameters, adkustment of different layers 
    like dense layers and max pooling to make an efficient neural network
    
    Solution: One of the important takeaway from the assigment was a 3x3, convolution followed by Max Pooling has better quality but requires more processing and more
    RAM whereas the 3x3 operation with stride of 2 has poor quality but requires less RAM and less processing. Be
    
### S3 Assignment :

    Task: Quiz on data augmentation strategy like "CutOut" , Numpy and  tensor operations , Gradient in simple mathematical operations, , benefits of 1x1 kernel, non-linearity 
    in neural network.
    
    Solution: Data Augmentation strategy like "Cutout" can improve the accuracy of network as they cause the network to become invariant and learn from other features of image .
    1x1 Convolution requires less computation for reducing the number of channels, uses existing channels to create complex
    channels(instead of re-convolution), requires less number of parameters, it also reduces the burden of channel selection on 3x3. Non linearity like relu or sigmoid make the 
    function differentiable, make loss is non constant and the plays an important role in making neural network " Universal Function Approximator".
    
### S4 Assignment :
    
    Task: Make a network that has: 
          1. 6 Convolution Layers with following kernels(10, 10, 20, 20, 30, 30)
          2. No use of Fully Connected Layers
          3. Use MNIST Dataset
          4. Use Maximum 2 max-pool layers 
          5. The network should have less than 10k Parameters. 
          Achieve >99.4% accuracy under 20 epochs. 
          
    Solution: I started extending the depth of the network by changing the number of channels in small increments like 1 => 8 => 16 => 32 which performed better and achieved the validation
    accuracy of 99.4%.

    I wanted to check how further we can reduce the parameters. I started with around 6k parameters and the accuracy touched 99.3% but didn't go beyond that. Then I used multiple techniques like adding 
    Batch Normalization and learning rate scheduler but finally with 9k parameters i was able to achieve 99.5% accuracy. I also rewrote the network in a sequential manner which 
    is easy to experiment with.
    
    There are 8 convolution layers with Batch Normalization and Relu after every layer except the last layer. Initially I have started with the channel size size of 4 and increased it uniformly till number of channel reach 20. I have an understanding that the memory assigned for 20 channels is equal to next 2**n channels(i.e. 32) but since the solution requires us to work under a parameter restriction so we went ahead with the given archietecture.
    
    
### S5 Assignment :
    Task: The problem has 10 steps with initial model having 6.3 Million Parameters with best test accuracy being 99.24. The tenth step/final model is expected to have:
    a).Use MNIST Dataset
    b). No use of Fully Connected Layers
    c). Use Batch Nomralization, lighter model, Regularization techniques, Global Average Pooling, Image Augmentation Techniques.
    Achieve >99.5% Test accuracy under 10 epochs.
    
    
    Solution: First Step(EVA_A5F1):
              Target:
              Setting up a skeleton
              Setting a basic Architecture with GAP to remove the final layer
              Result: 
              Total Parameters - 19,734
              Best Performance - 98.75%
              Analysis: I have to use batch norm to increase contrast, Performance is way below the goal of 99.4
              
              Second Step(EVA_A5F2):
              Target:
              Using Batchnorm to improve the performance
              Result:
              Total Parameters - 19,942
              Best Performance - 99.12%
              Analysis: There is some over fitting in the model. We should add dropout to improve that. I have to reduce the no of parameters below 10k
              
              Third Step(EVA_A5F3): 
              Target:
              Reduce the no of parameters below 10k
              Add dropout to reduce over fitting
              Adding 1x1 kernels for reducing the no of channles
              Result:
              Total Parameters - 7,216
              Best Performance - 99.32%
              Analysis: I have fixed overfitting using the dropout. The performance is still below the target 99.4%. 
              Upon observing the data we believe introducing rotation transform can improve the performance. I have reduced the number of parameters below 10k
              
              
              Fourth Step(EVA_A5F4): 
              Target:
              Add rotation transform
              Result:
              Total Parameters - 7,216
              Best Performance - 99.42%
              Analysis: Applying random rotation did improve the performance. Using LR scheduler might improve the performance further
              
             
### S6 Assignment :     
    => refer A6 for code
    Task: The goal of the assignment was to take the best code of the 5th assignment and make it train for 25 epochs with 5 different types of regularization techniques given as:

          1. with L1 Regularization + Batch Normalization
          2. with L2 Regularization + Batch Normalization
          3. with L1 Regularization + L2 Regularization + Batch Normalization
          4. with Ghost Batch Normalization
          5. with L1 Regularization + L2 Regularization + Ghost Batch Normalization
          
          Another goal was to show 25 misclassified images for the GBN model in to a single image.
          
          Solution: Following observations were made: 
                    1. The first model i.e. with L1 + BN performed well compared to other models but was inferior in terms of validation loss to GBN model.
                    2. The implementation of models using L2 gave poor results which might be due to inadequate tuning of parameter 'Lambda'.
                    3. GBN did perform better than BN owing to split of batched data and calculation of mean and std. deviation thereof.
          I also modularized the code by converting different functionalities of code into scripts.
          
### S7 Assignment :
    => refer EVA5 S7 for code
    Task: Design a network that:
    a). Use Cifar 10 Dataset
    b). Use Convolution and Transition blocks involving 3 max-pool layers in total.
    c). Total Receptive field must be more than 44
    d). One of the layers must be "Depthwise Separable Convolution"
    e). One of the layers must use "Dialated Convolution"
    f). Use Global Average pooling
    Achieve 80% Accuracy with total Parameters less than 1 Million.
    
    Solution:
    I achieved 83.74% accuracy in 33 Epochs with total number of parameters = 854,862.
    
    FIrst, i used Random Crop and Random Horizontal Flip data augmentation techniques right off the bat to make the network robust to differences in image.
    Depthwise separable convolution layers was followed by 1x1 convolution to maintain output uniformity in dimension. Dialated kernels and maxpool were used
    at appropriate layers tweaking different archietectures. 
    
    Different types of colvolution operation and their specific usage is elucidated in the model. Thorough understanding of convolution operations like:
    1. Dialated Convolution
    2. Transpose Convolution
    3. Depthwise separable Convolution
    4. Grouped Convolution 
    is required to make best use of these operation for an efficient network.
       
### S8 Assignment :
    => refer EVA5 S8 for code
    Task: The assignment consists of:-
          a. Use Cifar 10 Dataset
          b. Implement Resnet18 model
          c. Use the regularization, training, testing and dataloader scripts from the previous submission to run the model.
          Achieve >85% test accuracy - No limit on the number of epochs.
          
    Solution: The ResNet18 model was extracted from kuangkuangliu/pytorch-cifar. Random Crop and Random Horizontal Flip data augmentation techniques were used. The model 
    was trained for about 30 epochs to achieve the required test accuracy.
    
    This assignement gave me a chance to research about the working and archietecture of ResNet 18. It consists of a basic block and an optional bottleneck block
    Resnet 18 uses only basic blocks with 64, 128, 256 and 512 channels. Another salient feature of ResNet that makes it a truly exceptional network is use of 
    skip connections. There are two main use of skip connections:
                      a. Preserve Gradient - Helps to overcome the issue of vanishing gradient for initial layers.
                      b. In a plethora of tasks (such as semantic segmentation, optical flow estimation , etc.) there is some information that was captured in the initial layers
                         we would like to allow the later layers to also learn from them.                       
    
    
    
### S9 Assignment :
    => refer EVA5 S9 for code
    Task: The assignment consists of:-
          a. Implement Albumentation (Data Augmentation) techniques like Horizontal Flip, Cutout , Random Crop - Individually different for training and testing.
          b. Implement Gradcam to the predictions.
          c. Use the Resnet18 code, regularization, training, testing and dataloader scripts from the previous submission to run the model.
          Achieve >87% test accuracy - No limit on the number of epochs.
    
    Solution: The albumentation library is a well documented and easy to implement library for implementation of albumentation transforms. Tranforms namely - Horizontal flip,
    Cutout, Normalize, Randomcrop, ToTensorV2 were used for training dataset, while Normalize and ToTensorV2 were used for testing dataset.
    
    For gradcam implementation, several sources were taken into reference to tailor fit the final code as per the requirements. For reference, check grad_cam.py in S9. 
    Gradient-weighted Class Activation Mapping (GradCAM) uses the gradients of any target concept (say logits for 'dog' or even a caption),
    flowing into the final convolutionallayer to produce a coarse localization map highlighting the important regions in the image for predicting the concept. 

    We take the final convolutional feature map, and then we weight every channel in that feature with the gradient of the class with respect to the channel. 
    It tells us how intensely the input image activates different channels by how important each channel is with regard to the class. It does not require any re-training 
    or change in the existing architecture.
    
    The model was trained for about 65 epochs to achieve the required test accuracy.
    
 
### S10 Assignment :
     => refer EVA5 S10 for code
     Task: The assignment consists of:-
           a. Implement LR finder to find the best LR
           b. Implement ReduceLROnPleatue
           c. Show training and testing accuracy curves
           d. Use the Resnet18 code, regularization, Albumentation,training, testing and dataloader scripts from the previous submission to run the model.
           Achieve >88% test accuracy under 50 epochs.
           
      Solution: The LR finder code was extracted from davidtvs/pytorch-lr-finder. SGD was used as optimizer with Cross-Entropy loss as criterion. Range test is done 
      by setting end_lr, num_iter, step_mode. Upon plotting the LR finder plot the best LR is suggested based on the steepest gradient.
      
      ReduceLROnPleatue is imported from torch.optim.lr_scheduler. It functions as a regularizer by preventing pleatuing of the training. The learning rate is changed 
      by a pre-determined value to adjust to the direction of global minima. The most common technique is to start with a larger learning rate in the begining and then 
      reducing as soon as the model starts to pleatue. This technique does helps in squeezing out better accuracy in the later part of training.
      
      The model was trained for 50 epochs to achieve 89.87% test accuracy.


### S11 Assignment :              
    => refer EVA5 S11 for code 
    Task: The assignment consists of:-
          a. Write a code which uses this new ResNet Architecture for Cifar10:
             PrepLayer - Conv 3x3 s1, p1) >> BN >> RELU [64k]
             Layer1 -
             X = Conv 3x3 (s1, p1) >> MaxPool2D >> BN >> RELU [128k]
             R1 = ResBlock( (Conv-BN-ReLU-Conv-BN-ReLU))(X) [128k] 
             Add(X, R1)
             Layer 2 -
             Conv 3x3 [256k]
             MaxPooling2D
             BN
             ReLU
             Layer 3 -
             X = Conv 3x3 (s1, p1) >> MaxPool2D >> BN >> RELU [512k]
             R2 = ResBlock( (Conv-BN-ReLU-Conv-BN-ReLU))(X) [512k]
             Add(X, R2)
             MaxPooling with Kernel Size 4
             FC Layer 
             SoftMax
          b. Use One Cycle Policy such that:
             Total Epochs = 24
             Max at Epoch = 5
             LRMIN = To be calculated 
             LRMAX = To be calculated
             NO Annihilation   
          
          c. Use this transform - RandomCrop 32, 32 (after padding of 4) >> FlipLR >> Followed by CutOut(8, 8)
          
          d. Use the LR Finder, Resnet18 code, regularization, Albumentation,training, testing and dataloader scripts from the previous submission to run the model.
          Achieve 90% test accuracy - Batch SIze = 512.
    
    Solution: The model was written as Net class importing from nn.Module. The __init__ function defines the different layers used in the model namely convolution, maxpool2d, 
    Batch Normalization, flatten and linear. (refer model.py in EVA S11)
    The Forward function was thus written in the Net class with defines the archietecture - how each layer is arranged followed by relu and regularization like dropout.
    The network also involves addition of layers much like skip connection in ResNet. Finally the model outputs the softmax probabilities for the input data.
    The model was successfully written and implemented. 
    
    OnecycleLR is imported from torch.optim.The hyperparameters include optimizer, max_lr, epochs, steps_per_epoch ,pct_start.
    OnecycleLR is a superconvergence strategy devised by leslie smith. With superconvergence, neural networks can be trained an order of magnitude faster 
    than with standard training methods. One of the key elements in super-convergence is training with one learning rate cycle and a large maximum learning rate. 
    A primary insight that allows super-convergence training is that large learning rates regularize the training, hence requiring a reduction of all other 
    forms of regularization in order to preserve the optimal balance.

    Leslie smith recommends doing one cycle of learning rate of 2 steps of equal length. We choose the maximum learning rate using a range test. 
    We use a lower learning rate as 1/5th or 1/10th of the maximum learning rate. We go from a lower learning rate to a higher learning rate in step 1 
    and back to a lower learning rate in step 2. 
    
    The superconvergence technique of OnecycleLR worked perfectly fine and gave superfast accuracy results which were expected during the start of training. 
    
    The model was trained for 25 epochs to achieve 88.07% test accuracy.

     
    
### S12 Assignment :
    => refer EVA5 S12a and S12b for code 
    Task: This assignment consists of:
          12.A: Assignment on Tiny Imagenet Dataset :
                a. Split the dataset 70-30  
                b. Train ResNet 18 on the dataset
                Achieve >50% Test accuracy in 50 epochs.
          12.B: Assignment on clustering, data Collection and annotation:
                a. Download/collect minimum 50 images each of people wearing Hardhat, vest, mask and boots.
                b. Annotate bounding boxes around hardhat, vest, mask and boots.
                c. Find out the best total number of cluster using k-means algorithm. 
    
    Solution 12.A: Quite importantly the first task of problem was to preprocess the data and make a 70%-30% split. The dataset was first unzipped. It initally contained 90% 
    data in the train directory and rest 10% data in the val directory. The validation data along with its labels were then first cleared from the val directory. Then, the
    complete data along with labels was distributed in new train and test directory with the required split.
    
    It was initally difficult to achieve the required accuracy as the number of classes are 200 with not much data for each individual class. Few changes were introduced namely:
    a. Data Augmentation using Albumentaion: Transforms used are : RandomCrop, PadIfNeeded, RGBShift, Rotate
    b. Batch Size= 256
    c. Both L1 and L2 decay were used.
    d. Use of OnecycleLR to achieve faster convergence.
    The required accuracy was achieved in 35 epochs.
    
    Solution 12.B: For annotation of the collected data, the annotation tool used was VIA - VGG Image Annotator by Oxford. The Json File obtained was retreived. 
    Ratio of height and width of bounding box to the image height and width wre respectively calculated. The logarithm of these ratio were calculated. The array of the 
    ratio was then used as data for calculating the best total number of cluster(which denotes the number of different anchor boxes). Upon implementation of k-means clustering
    the number of cluster was obtained to be 3 and subsequent graph was plotted.(refer S12b)
    
### S13 Assignment :    
    => refer EVA5 S13a and S13b for code  
    Task: This assignment consists of:
          13.A: Assignment on OpenCV Yolo :
                a. Take an image of yourself holding an object which is one of the class in COCO Dataset.
          13.B: Assignment on YoloV3 :
          a. Train custom data which was annotated in the last assignment using YoloV3
          b. Download a very small (~10-30sec) video from youtube which shows your classes. 
          c. Use ffmpeg to extract frames from the video.
          d. Infer on these images using YoloV3 and generate detection outputs and save them in output folder.
          e. Use ffmpeg  to convert the files in your output folder to video
          
    Solution 13.A: The assignment was fairly simple. The OpenCV code was taken from the article by Sergio Canu on "Yolo Object Detectiob using OpenCV with Python". 
    I posed in front of camera with a fork in my right hand(One of the classes of COCO dataset). It was a good photography session and after few poor clicks, i finally 
    got a good click with good lightning and a tolerable face. The model easily predicted the fork in my hand. Job done.
    
    Solution 13.B: The Reference code for YOLOV3 was taken from theschoolofai/YoloV3. The weights for YoloV3 were downloaded and stored in designated folder.
    Changes in the config file were done namely:
    a. Changes in filters according to number of classes.
    b. Changes in the number of classes to be detected(4 in Our case)
    c. Since we were working with limited samples so we changed burn_in to 100, max_batches to 500, steps to 4000,4500
    
    Data folder was prepared which has following files: 
    a. images
    b. labels
    c. custom.data (data file - containes paths)
    d. custom.names (class names)
    e. custom.txt (list of name/path of the images we want our network to be trained on)
    
    First the model was train on SmallCOCO dataset for 3 epochs and then trained on Custom Data for 5 epochs using the above mentioned custom config file.
    Using the ffmpeg  frames from the a construction video were extracted and store in video_frames folder.
    The inference was made on the video frames using detect.py script and the detection threshold was kept low ~0.1. The model could detect the hardhat, boots, mask, and vest 
    in frames with a good accuracy. The detected frame output was then stored in output folder.
    The frames were converted into MP4 video format and the video was uploaded on the youtube.
    Have a look: https://youtu.be/nPgygJrF1J0
    
### S14 Assignment :
    => refer EVA5 S14 for code
    Task: This assignment consists of:
          a. Take the dataset of hardhat, boots, mask and vest prepared in previous assignment and run:
             1. MIdas and get depth images.
             2. PlaneRCNN and get planer images.
             
          b. Make a new dataset containing depth maps from midas, surface planes from planeRCNN and bounding box from YoloV3.
    
    Solution: MIDAS Depth Map: Monocular Depth Estimation We have used the MIDAS model to generate a depth map. The MIDAS technique was published in the research paper titled 
    “Towards Robust Monocular Depth Estimation: Mixing Datasets for Zero-shot Cross-dataset Transfer” Here we do Monocular depth estimation from a single rgb image. The output of 
    the algorithm is a single image file with a depth map differentiated by the intensity of the different areas of the map. This type of data can be used for multiple 
    applications including Augmented Reality, Robotics, Autonomous Systems and Self- Driving Cars.
             
    PlaneRCNN Surface Planes: We have used PlaneRCNN algorithm to make surface planes along with depth maps for an image. Here we only use surface planes and drop the depth maps. 
    PlaneRCNN was published in the research paper “PlaneRCNN: 3D Plane Detection and Reconstruction from a Single Image” by NVIDIA Research. This algorithm detects and 
    reconstructs piecewise plane surfaces using a variant of MaskRCNN. As input, we need just a single RGB image. For every single input, it provides 9 output files including 
    DEPTH Maps, 3Dplanes, and planer regions. Different regions are annotated using different colored masks.
    
    Bounding Boxes: The dataset has 4 classes and it was annotated using an annotator tool that provides us with coordinates of bounding boxes along with their dimensions. Folder 
    consists of i). classes.txt => Contains names of the four classes ii). custom.names iii). custom. data => Number of classes and path of files containing names of train, 
    validation images and path to custom.name file iv) test.shapes v) test.txt => Description of files to be used for testing. vi) train.shapes vii)train.txt viii) images(Folder) 
    => Contains images for bounding box ix) labels(Folder) => Contains txt file for every image - has coordinates related to bounding box (x, y, h, w)
    
    
    
    
    
    
    
    
    
    
    
