Myntra Hackathon 2024 : Solution (LOGIC LEGENDS)
GROUP MEMBER - NIKITA KUMARI, VIDISHA JAHANVI
Theme of the Challenge : Engagement on a shopping platform
Refer to PPT : https://github.com/vidishaaaaa/myntra-logic-legend/blob/main/Myntra_PPT%5B1%5D.pdf
Table of Contents
Overview
Objective
Procedure
Data Cllection
Semantic Segmentation
Attribute Recognition
Results
Technologies Used
Overview
Fast fashion has caused a massive increase in the rate at which new trends are set.

A lot of companies make replica of luxury products at an affordable price.

As a result it is getting difficult for the average consumer to select apparels from such a vast variety.

The problem is further elevated by the lack of interaction with the product which exists in traditional shopping, since it is difficult to choose a apparel without trial.

Objective
With the rise of fast fashion, it is difficult to keep track of ever changing trends.

A model that would help the user filter the products based on the latest trends will make the shopping experience a lot smoother and give Myntra an edge over other e-commerce sites.

Our model detects the latest trends in the market to help the user make the right choice. It would serve as each individual’s own personal, low budget stylist.

Trend Prediction
The first step includes collecting images from the popular social media site - Instagram.
An account following some of the most famous fashion influencers of today is created.

Instagram's algorithm ensures that the feed consists of posts in a descending order according to popularity.

Making use of this feature of Instagram, a model - instagram_scraper1.py is created.

The scraper model ( instagram_scraper1.py ) outputs -profile.txt , profiles.csv  and datetime.csv 

This shows us a detailed list of the profile names and the respective time stamps of posts appearing on the feed.

Next, run syntax.txt i.e.
instagram-scraper -f profile.txt -u perc.eptrons -p Myntra2020 --template {datetime}--latest-stamps time.txt in the command line.

This downloads all the images after the particular latest time stamp.

time.txt contains the timestamps after which the images need to be downloaded.

A folder containing all such images is created.

Run the notebook saveimages.py
This provides profile.txt to an open source software used by us, which downloads the images with the required custom time stamp with and saves them in a required directory.

The open source software can be found on this Github repository: https://github.com/arc298/instagram-scraper

This completes the creation of basic dataset required for further steps.

Semantic Segmentation
Due to the time constraints we decided to use COCO_weights to pretrain our Mask-RCNN model and then fine tune it on around 40,000 images from I-Materialist Dataset which is available on kaggle. We used the matterpost implementation of Mask-RCNN. The output of this step is a segmentation mask which is used to isolate the apparel from its surrounding.

Attribute Recognition
An encoder-decoder model is used, the encoder being InceptionV3 model and decoder an LSTM-based model.

The masks are fed to this model. A feature vector is generated which is decoded to get the attributes.

K-Means Clustering is used for colour detection.

The final output of this prototype includes a list of the most trending colours and attributes for the user to choose from.

This model was used to predict attributes on our dataset and an interactive website is created by deploying the model using Flask. The website allows the user to filter the products based on few of these attributes.

Results
A few examples of images obtained using the Mask-RCNN model for semantic segmentation are given below:







A few examples of images obtained after attribute detection using the encoder-decoder model are given below:







Technologies Used
python
OpenCV
Flask
SQL
Jupyter
References
Mask-RCNN original paper : https://arxiv.org/abs/1703.06870 Matterpost implementation : https://github.com/matterport/Mask_RCNN Semantic segmentation model : https://github.com/manas3858/iMat-Fashion/ Starter kernel for imat(Kaggle): https://www.kaggle.com/ramswaroopbhakar14/training-inception-v3-for-fashion-attributes
