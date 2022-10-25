# EarthNet2022

### Context
Forecasting the state of vegetation in response to climate and weather events is a major challenge. Requena and al. (2021) [1] define the land surface forecasting task as a strongly guided video prediction task where the objective is to forecast the vegetation developing at very fine resolution using topography and weather variables to guide the prediction and design a first dataset for this task, the EarthNet2021 dataset. Several papers have addressed this issue, namely [2, 3] on the EarthNet2021 dataset, and [4] focusing instead on Africa (freshly accepted! :D currently under review, the pdf is in the repository, waiting for the arxiv link). See [4] for more details on context and the project.

### EarthNet2022, a new brand dataset
The new dataset  has a better cloud masking, the data are not anymore interpolated and it include new variables (Landsat climatology NDVI and Sentinel - 1 vegetation index), relevant for environnemental science. This also means that the times series (from different sources) are not regular.

The variables are:
* Sentinel 2 (B02 to B12 bands)
* Sentinel1 (VV, VH, mask)
* NDVI Climatology (12 months Landsat 30m/pix)
* SRTM (DEM)
* ESA World Cover
* ERA5 (t2m, pev, slhf, ssr, sp, sshf, e, tp)
* Soil Grids
* Geomorphons
* ALOS, COP 30 (DEMs)

The target is the Normalized Difference Vegetation Index (NDVI), a proxy for vegetation health monitoring calculated from the red and infrared bands.

*Please note:* This new dataset will most likely **not be publicly available** by the end of the project. However, a sample (or few if needed) will be available, as well as the jupyters used to explore the data. 

### Approach - Irregularly sampled time series
**Bring your own method**
The objective to create a model capable of learning the relationship between vegetation states, local factors and weather conditions, at a very fine resolution in order to characterise and forecast the impact of weather extremes from an ecosystem perspective. I will firstly explore the new dataset (understand the variables, maybe select some of them), and write the dataloader. Then I need to develop a model for the data. The main point is that the data are irregularly sampled time series (from different sources). Although several papers have addressed this issue for RNNs, we need to extend the methods to include the spatial dimension of our data. This is the main point of rech



*Note:* I am aware that the papers are rather for temporal series without spatial components, which can represent an insurmountable difficulty in the given time of the project. If this is the case, the fallback plan would be to avoid the problem by interpolating all the data and get a regular time step, and I would orient the project on the explainability of a more basic ConvLSTM model, with more classical had-hoc methods. 

### Work-breakdown structure 
 * Data collection: 0 hours
 * Data understanding and exploration: 15 hours   
understanding the distribution 
 * Framework: 10 hours   
PyTorch lighnight framework (already implemented?)
 * Model for irregularly sampled time series: 50 hours
 * Optimisation: 20 hours   
There is a potentially important grain to be gained through a more rigorous optimization (try different optimiser, use a schudeler) 
 * Building an application: 30 hours   
I don't have any knowledge in web development or application, so it will probably take time and it is difficult to evaluate. The idea would be to develop a (simple) web page with an access to the model and a (sub)set of samples from the test test. Select a sample on the map, and generate its prediction as well as the analyses of the prediction.
 * Final report: 15 hours
 * Presentation: 10 hours
 * Total: 160 hours


### Bibliography
[1] Christian Requena-Mesa, Vitus Benson, Markus Reichstein, Jakob Runge, and Joachim Denzler. Earthnet2021: A large-scale dataset and challenge for earth surface forecasting as a guided video prediction task. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pages 1132–1142, 2021.

[2] Codrut-Andrei Diaconu, Sudipan Saha, Stephan Günnemann, and Xiao Xiang Zhu. Understanding the role of weather data for earth surface forecasting using a convlstm-based model. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pages 1362–1371, 2022.

[3] Klaus-Rudolf William Kladny, Marco Milanta, Oto Mraz, Koen Hufkens, and Benjamin David Stocker. Deep learning for satellite image forecasting of vegetation greenness. bioRxiv, 2022.

[4] Claire Robin, Christian Requena-Mesa, Vitus Benson, Lazaro Alonso, Jeran Poehls, Nuno Carvalhais, and Markus Reichstein. Learning to forecast vegetation greenness at fine resolution over Africa with ConvLSTMs. In *Tackling Climate Change with Machine Learning workshop, NeurIPS 2022*.

