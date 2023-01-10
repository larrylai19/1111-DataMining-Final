# 1111-DataMining-Final


## Dataset

[YouTube Videos and Channels Metadata](https://www.kaggle.com/datasets/thedevastator/revealing-insights-from-youtube-video-and-channe)


## Usage

### 1. Create Enviroments

+ Windows

  ```
  python -m venv venv
  venv\Scripts\activate
  pip install -r requirements.txt
  jupyter lab
  ```

### 2. Download Dataset

+ Download dataset from [YouTube Videos and Channels Metadata](https://www.kaggle.com/datasets/thedevastator/revealing-insights-from-youtube-video-and-channe)
+ Put `YouTubeDataset_withChannelElapsed.csv` under source folder

### 3. Open `data-mining.ipynb` On Jupyter


## Processing

### 1. Data Preprocessing

+ #### Unique: Set videoID to index and Drop duplicate data
    + Delete attributes ['index', 'likes/dislikes', 'channelId']

+ #### DropNA: Drop all null and meaningless values
    + Delete by row if attributes' value is -1 in data

+ #### TimeStamp: Transfer time format to timestamp
    + 2012-01-19T18:38:28.000Z -> 1326902400

![dataPreprocessing.png](images/dataPreprocessing.png)

### 2. Calculate Correlation

+ Use min-max scaling to normalization
+ Calculate Pearson correlation coefficient correlations

+ #### Correlation
    ![correlation.png](images/correlation.png)
    
<!-- + #### Correlation Heatmap
    ![correlation_heatmap.png](images/correlation_heatmap.png) -->
    
+ #### Correlation Heatmap With Annotation
    ![correlation_heatmap_annot.png](images/correlation_heatmap_annot.png)

### 3. Scatter Plot Between Two Attributes

<!-- + #### VideoViewCount and SubscriberCount
    ![videoViewCount_subscriberCount_scatter_s=5.png](images/videoViewCount_subscriberCount_scatter_s=5.png) -->

+ #### ChannelViewCount and SubscriberCount
    ![channelViewCount_subscriberCount_scatter_s=5.png](images/channelViewCount_subscriberCount_scatter_s=5.png)
    
<!-- + #### VideoViewCount and SubscriberCount With Correlation
    ![videoViewCount_subscriberCount_scatter_withCorr.png](images/videoViewCount_subscriberCount_scatter_withCorr.png) -->

+ #### ChannelViewCount and SubscriberCount With Correlation
    ![channelViewCount_subscriberCount_scatter_withCorr.png](images/channelViewCount_subscriberCount_scatter_withCorr.png)
    

### 4. Analysis by VideoCategory and Bar Chart

+ Add attribute 'videoCategory' by 'videoCategoryID'
+ Group by VideoCategory

+ #### SubscriberCount
    ![subscriberCount_bar.png](images/subscriberCount_bar.png)

+ #### VideoCount
    ![videoCount_bar.png](images/videoCount_bar.png)
    
+ #### Views/Subscribers
    ![views_subscribers_bar.png](images/views_subscribers_bar.png)
    
+ #### SubscriberCount and VideoViewCount
    ![subscriberCount_videoViewCount_bar_75.png](images/subscriberCount_videoViewCount_bar_75.png)


## Functions

+ ### Draw Heatmap
    ``` Python
    def draw_heatmap(data):
      # Use minmax to normalize (value between 0 ~ 1)
      normalizedDF_minmax = (data - data.min()) / (data.max() - data.min())
      normalizedDF_correlation = normalizedDF_minmax.corr()
      plt.figure(figsize=(30, 24))
      sns.heatmap(normalizedDF_correlation, cmap='RdBu_r', linewidths=0.5, vmin=-1, vmax=1, annot=True)
      plt.show()

    draw_heatmap(data)
    ```
