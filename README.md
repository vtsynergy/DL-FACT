# DL-FACT
DL-FACT stands for Deep Learning-based Fast and Accurate Computed Tomography. It is a computational deep-learning (DL) framework for fast, accurate CT testing and monitoring of COVID-19. This DL-FACT repository contains a CT Image Enhancement AI submodule and an Analysis AI submodule. Specifically, there is an Enhancement AI submodule that is based on a 2D version of DenseNet and Deconvolution based Network (i.e., 2D-DDnet). The 2D-DDnet Enhancement AI is used to enhance the quality of CT scans, and the Analysis AI is used to automatically analyze CT scans. The Analysis AI contains two further submodules: Segmentation AI and Classification AI. The Segmentation AI is used to segment the lung region from the CT scans, and the Classification AI is used to predict the possibility for COVID-19. Figure 1 shows a high-level overview of DL-FACT. 

Our experimental results show that the diagnostic accuracy is improved from about 86% to 91% by enhancing CT scan images with our Enhancement AI.
Enhancement AI is based on DenseNet and Deconvolution network (DDnet) architecture. The AI generates high-quality enhanced CT images.

**Figure 1： High-Level Overview of DL-FACT (Deep Learning-based Fast and Accurate Computed Tomography)**
![image](https://user-images.githubusercontent.com/31482058/119709957-ab721000-be12-11eb-9bb2-cb20a8b6938a.png)

Figure 2 is a schematic diagram of the test framework we used for the experiment. After preparing the data, we first use the analysis AI to directly perform diagnostic tests on the original data to obtain the diagnostic accuracy. Then use the same analysis AI to perform diagnostic tests on the enhanced image. Comparing the diagnosis results based on different images, it can be found that the accuracy of CT scan classification using enhanced AI has been greatly improved.

**Figure 2: Overall Architecture of DL-FACT Framework, where Analysis AI = Segmentation AI + Classification AI**
![image](https://user-images.githubusercontent.com/31482058/119988932-7cc37900-bf7b-11eb-8ef3-49226e2d331c.png)

Figures 3 and 4 show some results of our testing experiments. Figure 3 are example diagrams of images before and after enhancement. Figure 4 is the ROC curve improvement of analysis after enhancement. 

**Figure 3: A CT Image of a COVID-19 Patient Before Enhancement (Left) and its Counterpart After Enhancement (Right)**
![image](https://user-images.githubusercontent.com/31482058/119993479-6e2b9080-bf80-11eb-8910-397743b80a62.png)

**Figure 4: ROC Curve of Analysis Result of One Testing**
![image](https://user-images.githubusercontent.com/31482058/119710075-cb093880-be12-11eb-95d2-66e8e0d5aa0b.png)

## Hardware requirements

For Enhancement Model:

The code can run without GPU. Running code with GPU could increase training and inference speed. PyTorch requires Nvidia GPUs with compute capability 6.0 or higher, i.e. any GPU from Pascal, Volta, Turing, Ampere series will work. Our code was tested on Nvidia V100, P100, T4 GPUs.

For Segmentation and Classification Model:

One or more Nvidia GPU. (2+GPUS are recommended for advanced features as AutoML). GPU version is only compatible with Nvidia GPUs having compute capability 6.0 or higher. Meaning, any GPU from Pascal, Volta, Turing, Ampere series will work.

## Software requirements

The Enhancement AI depends on Conda (version: conda 4.6.11), Python (version: 3.6.8), PyTorch (version: 1.0.1), Scikit-image (version: 0.13.1), PIL (version: 5.3.0), Matplotlib (version: 3.0.3), Nibabel (version: 3.2.1), and Cuda compilation tools (release 10.1, V10.1.105)

The Analysis AI require Nvidia-docker and Nvidia Clara SDK. If you already have docker installed then user should be in the docker group. Otherwise, sudo access is needed to install the prerequisite. Nvidia Clara SDK requires Nvidia CUDA 11.0.194 and Nvidia Driver release 450 or later.


## How to run
1. Run the [Enhancement AI](https://github.com/vtsynergy/2D-DECT). The enhancement model will generate original CT scans (.nii) and enhanced CT scans.
2. (OPTIONAL) Run the [Analyze AI](https://github.com/vtsynergy/Analyze-AI/tree/251bcf33df61851529e9cbcb1995c3f218f7f759). The segmentation program will automatically copy the imediate result generated by enhancement model and generate segmentaion mask images (.nii), and the classification program will automatically copy the segmentation mask image generated by segmentation models. The classification model will generate the positive and negative possibility score of each CT scan in a table (.csv).

## Data Citation
**LIDC-IDRI**: Armato III, SG; McLennan, G; Bidaut, L; McNitt-Gray, MF; Meyer, CR; Reeves, AP; Zhao, B; Aberle, DR; Henschke, CI; Hoffman, Eric A; Kazerooni, EA; MacMahon, H; van Beek, EJR; Yankelevitz, D; Biancardi, AM; Bland, PH; Brown, MS; Engelmann, RM; Laderach, GE; Max, D; Pais, RC; Qing, DPY; Roberts, RY; Smith, AR; Starkey, A; Batra, P; Caligiuri, P; Farooqi, Ali; Gladish, GW; Jude, CM; Munden, RF; Petkovska, I; Quint, LE; Schwartz, LH; Sundaram, B; Dodd, LE; Fenimore, C; Gur, D; Petrick, N; Freymann, J; Kirby, J; Hughes, B; Casteele, AV; Gupte, S; Sallam, M; Heath, MD; Kuhn, MH; Dharaiya, E; Burns, R; Fryd, DS; Salganicoff, M; Anand, V; Shreter, U; Vastagh, S; Croft, BY; Clarke, LP. (2015). Data From LIDC-IDRI. The Cancer Imaging Archive. http://doi.org/10.7937/K9/TCIA.2015.LO9QL9SX

**BIMCV**: Region, B. M. I. D. o t V., Pertusa, A., & de la Iglesia Vaya, M. (2020, June 9). BIMCV-COVID19+. https://doi.org/10.17605/OSF.IO/NH7G8

**MIDRC**: Tsai, E., Simpson, S., Lungren, M.P., Hershman, M., Roshkovan, L., Colak, E., Erickson, B.J., Shih, G., Stein, A., Kalpathy-Cramer, J., Shen, J., Hafez, M.A.F., John, S., Rajiah, P., Pogatchnik, B.P., Mongan, J.T., Altinmakas, E., Ranschaert, E., Kitamura, F.C., Topff, L., Moy, L., Kanne, J.P., & Wu, C. (2020). Data from the Medical Imaging Data Resource Center - RSNA International COVID Radiology Database Release 1a - Chest CT Covid+ (MIDRC-RICORD-1a).  Data from The Cancer Imaging Archive (2020). DOI: https://doi.org/10.7937/VTW4-X588.
