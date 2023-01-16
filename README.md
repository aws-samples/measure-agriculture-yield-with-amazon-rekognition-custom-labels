## Use computer vision to measure agriculture yield with Amazon Rekognition Custom Labels

In the agriculture sector, the problem of identifying and counting the amount of fruit on trees plays an important role in crop estimation. The concept of renting and leasing a tree is becoming popular, where a tree owner leases the tree every year before the harvest based on the estimated fruit yeild. The common practice of manually counting fruit is a time-consuming and labor-intensive process. It’s one of the hardest but most important tasks in order to obtain better results in your crop management system. This estimation of the amount of fruit and flowers helps farmers make better decisions—not only on only leasing prices, but also on cultivation practices and plant disease prevention.

This is where an automated machine learning (ML) solution for computer vision (CV) can help farmers. Amazon Rekognition Custom Labels is a fully managed computer vision service that allows developers to build custom models to classify and identify objects in images that are specific and unique to your business.

Rekognition Custom Labels doesn’t require you to have any prior computer vision expertise. You can get started by simply uploading tens of images instead of thousands. If the images are already labeled, you can begin training a model in just a few clicks. If not, you can label them directly within the Rekognition Custom Labels console, or use Amazon SageMaker Ground Truth to label them. Rekognition Custom Labels uses transfer learning to automatically inspect the training data, select the right model framework and algorithm, optimize the hyperparameters, and train the model. When you’re satisfied with the model accuracy, you can start hosting the trained model with just one click.

## Solution overview

We create a custom model to detect fruit using the following steps:

 + Label a dataset with images containing fruit using Amazon SageMaker Ground Truth.
 + Create a project in Rekognition Custom Labels.
 + Import your labeled dataset.
 + Train the model.
 + Test the new custom model using the automatically generated API endpoint.

Rekognition Custom Labels lets you manage the ML model training process on the Amazon Rekognition console, which simplifies the end-to-end model development and inference process.


## Prerequisites

To create an agriculture yield measuring model, you first need to prepare a dataset to train the model with. For this solution, our dataset is composed of images of fruit. The following images show some examples.

![Sample Image](/image/ML-2594-image001.png)

You can download the image files from the repository.

For this solution, we only use a handful of images to showcase the fruit yield use case. You can experiment further with more images.

To prepare your dataset, complete the following steps:

 + Create an Amazon Simple Storage Service (Amazon S3) bucket.
 + Create two folders inside this bucket, called raw_data and test_data, to store images for labeling and model testing.
 + Choose Upload to upload the images to their respective folders from the repository.
	
![S3 Upload](/image/ML-2594-image003.png)

**Train your model using this dataset.**

## Test the model
**analyzeImage.py** can be used in this repository to count the amount of fruit in an image

Once your model is ready for use and in the Running state,complete the following steps:

**Step 1 : Start the model**
On your model details page, on the **Use model** tab, choose **Start**.

**Step 2 : Test the model**
When the model is in the Running state, you can use the sample testing script analyzeImage.py in this repository to count the amount of fruit in an image.
![Start the model](/image/ML-2594-image041.png)

  + Download this script from the repository .
  + Edit this file to replace the parameter bucket with your bucket name and model with your Amazon Rekognition model ARN.

We use the parameters photo and min_confidence as input for this Python script.
![Input](/image/ML-2594-image043.png)

You can run this script locally using the AWS Command Line Interface (AWS CLI) or using AWS CloudShell. In our example, we ran the script via the CloudShell console. Note that CloudShell is free to use.

Make sure to install the required dependences using the command pip3 install boto3 PILLOW if not already installed.
![AWS CloudShell](/image/ML-2594-image045.png)


 + Upload the file analyzeImage.py to CloudShell using the Actions menu.

![AWS CloudShell](/image/ML-2594-image047.png)


The following screenshot shows the output, which detected two fruits in the input image. We supplied 15.jpeg as the photo argument and 85 as the min_confidence value.

![Confidence](/image/ML-2594-image049-cropped.png)

The following example shows image 15.jpeg with two bounding boxes.

![Confidence](/image/ML-2594-image051.png)

**Step 3:  Stop the model**
When you’re done, remember to stop model to avoid incurring in unnecessary charges. On your model details page, on the Use model tab, choose Stop.

## Clean up

To avoid incurring unnecessary charges, delete the resources used in this solution when not in use. We need to delete the Amazon Rekognition project and the S3 bucket.
 + Delete the Amazon Rekognition project
 + Delete your S3 bucket.You first need to empty the bucket and then delete it.


	
## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

