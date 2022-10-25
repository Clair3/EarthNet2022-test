# EarthNet2022

### Context
Forecasting the state of vegetation in response to climate and weather events is a major challenge. Requena and al. (2021) [1] define the land surface forecasting task as a strongly guided video prediction task where the objective is to forecast the vegetation developing at very fine resolution using topography and weather variables to guide the prediction and design a first dataset for this task, the EarthNet2021 dataset. Several papers have addressed this issue, namely [2, 3] on the EarthNet2021 dataset, and [4] focusing instead on Africa (freshly accepted! :D currently working on the reviews, the pdf is in the repository, waiting for the arxiv link). See [4] for more details on the project.

### EarthNet2022, a new brand dataset
The new dataset  has a better cloud masking, the data are not anymore interpolated and it include new variables (Landsat climatology NDVI and Sentinel - 1 vegetation index), relevant for environnemental science. This also means that the data (from different sources) are irregularly sampled time series.

The variables are:
* Sentinel 2 (B02 to B12 bands) - spatio-temporal data
* Sentinel1 (VV, VH, mask) - spatio-temporal data
* NDVI Climatology (12 months Landsat 30m/pix) - spatio-temporal data
* SRTM (DEM) - static data
* ESA World Cover - static data
* ERA5 (t2m, pev, slhf, ssr, sp, sshf, e, tp) - temporal data
* Soil Grids - static data
* Geomorphons - static data
* ALOS, COP 30 (DEMs) - static data

The target is the Normalized Difference Vegetation Index (NDVI), a proxy for vegetation health monitoring calculated from the red and infrared bands.

*Please note:* This new dataset will most likely **not be publicly available** by the end of the project. However, a sample (or few if needed) will be available, as well as the jupyters used to explore the data. 

### Approach - Irregularly sampled time series
**Bring your own method** 

The objective to create a model capable of learning the relationship between vegetation states, local factors and weather conditions, at a very fine resolution in order to characterise and forecast the impact of weather extremes from an ecosystem perspective. I will firstly explore the new dataset (understand the variables, maybe select some of them), and write the dataloader. 

the data have different dimensions (spatio-temporal, only temporal (for weather), or static (terrain topology), we will use the simplest solution which consists in resizing and concatenating everything to the spatio-temporal dimensions.

Then I need to develop a model for the data. The main point is that the data are irregularly sampled time series (from different sources). Although several papers have addressed this issue for RNNs, we need to extend the methods to include the spatial dimension of our data. this will be our main axis of research. We will compare our results to a ConvLSTM baseline that does not take into account the time-step irregularity. 

A second solution, simpler to implement, consists in directly testing the methods developed for the RNN. During the learning phase, the RNN is used only on a random subset of pixels, and the gradient is computed on these pixels. The idea is that on an image, and even more on a landscape, a large number of pixels are (almost) identical, and it is not necessary to compute the gradient for each of these pixels. In this way, we drastically reduce the learning time required for the use of a RNN on spatio-temporal data. This solution has shown good results with classical RNN, so it is promising for RNN adapted to irregular data. 

Finally, I would like to develop a web application, the tricky part is that I have no knowledge of javascript at the moment, so it could be reduced to a docker, or a simple command line in case of lack of time. But ideally, on the web application, the user will be able to select a sample on a map of Africa, then generate the prediction with some associated analysis. 

### Work-breakdown structure 
 * Data collection: 0 hours
 * Data understanding and exploration: 10 hours   
understanding the distribution 
 * Framework: 10 hours   
PyTorch lighnight framework (already implemented?)
 * Model for irregularly sampled time series: 50 hours
 * Optimisation: 20 hours 
 * Building an application: 40 hours   
I don't have any knowledge in web development or application, so it will probably take time and it is difficult to evaluate. The idea would be to develop a (simple) web page with an access to the model and a (sub)set of samples from the test test. Select a sample on the map, and generate its prediction as well as the analyses of the prediction.
 * Final report: 15 hours
 * Presentation: 10 hours
 * Total: 155 hours


### Bibliography
[1] Christian Requena-Mesa, Vitus Benson, Markus Reichstein, Jakob Runge, and Joachim Denzler. Earthnet2021: A large-scale dataset and challenge for earth surface forecasting as a guided video prediction task. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pages 1132–1142, 2021.

[2] Codrut-Andrei Diaconu, Sudipan Saha, Stephan Günnemann, and Xiao Xiang Zhu. Understanding the role of weather data for earth surface forecasting using a convlstm-based model. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pages 1362–1371, 2022.

[3] Klaus-Rudolf William Kladny, Marco Milanta, Oto Mraz, Koen Hufkens, and Benjamin David Stocker. Deep learning for satellite image forecasting of vegetation greenness. bioRxiv, 2022.

[4] Claire Robin, Christian Requena-Mesa, Vitus Benson, Lazaro Alonso, Jeran Poehls, Nuno Carvalhais, and Markus Reichstein. Learning to forecast vegetation greenness at fine resolution over Africa with ConvLSTMs. In *Tackling Climate Change with Machine Learning workshop, NeurIPS 2022*.

