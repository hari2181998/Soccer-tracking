# SoccerNet - Tracking



<p align="center"><img src="Images/GraphicalAbstract-tracking.png" width="640"></p>

The Tracking dataset consists of 12 complete soccer games from the main camera including:
 - 200 clips of 30 seconds with tracking data.
 - one complete halftime annotated with tracking data.
 - the complete videos for the 12 games.

The dataset has 57 30-seconds clips for the train set, 49 clips for the test set.

## How to download SoccerNet-tracking

The challenge organizers provide a [SoccerNet pip package](https://pypi.org/project/SoccerNet/) to easily download the data and the annotations. 

To install the pip package simply run:

<code>pip install SoccerNet</code>

Then, to download the tracking data, enter the following commands:

```python
from SoccerNet.Downloader import SoccerNetDownloader
mySoccerNetDownloader = SoccerNetDownloader(LocalDirectory="path/to/SoccerNet")
mySoccerNetDownloader.downloadDataTask(task="tracking", split=["train","test","challenge"])
```

## Data format

The ground truth and detections are stored in comma-separate csv files with 10 columns. 
These values correspond in order to: frame ID, track ID, top left coordinate of the bounding box, top y coordinate, width, height, confidence score for the detection (always 1. for the ground truth) and the remaining values are set to -1 as they are not used in our dataset, but are needed to comply with the MOT20 requirements.


## Evaluation

We use the [TrackEval](https://github.com/JonathonLuiten/TrackEval) repository to evaluate the performances. To participate the challenge, you should submit the result as a zip file to [EvalAI](https://eval.ai/web/challenges/challenge-page/1539/overview). Please see the READMEs of our baseline methods under the "Benchmarks" directory for instructions on how to prepare the zipped results.

## Visualizations

You can use the [MOT Challenge Evaluation Kit](https://github.com/dendorferpatrick/MOTChallengeEvalKit) to visualize the tracks.

## Tracking methods

The repository is structured in 2 parts - One for detection and one for tracking. We tried to experiment with contrastive learning methods for improving the feature extraction part in detection. 

In tracking, 2 baseline methods have been implemented namely Deepsort and ByteTrack. Refer the soccernet tracking repository to run the mentioned baselines. Two key ideas involving crowded tracklets and cascaded IOU buffers were also tested on top of Bot-Sort method to improve the accuracy of tracking during occluded detections. Refer the tracking folder to test the same.
