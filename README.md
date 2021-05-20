# DL-FACT
Macro-repository for CT Image Enhancement and Analysis Submodules. It is a deep learning-based COVID-19 testing framework, which is composed of post-CT Enhancement AI to enhance the quality of CT scans, segmentation AI to segment lung region from CT scans, and CT Classification AI to predict the possibility for COVID-19. 
Enhancement AI is based on DenseNet and Deconvolution network (DDnet) architecture. The AI generates high-resolution enhanced CT images.
Segmentation AI is based on a 3D version of AHNet. Classification AI uses 3D DenseNet-121 architecture.
Our early results show good improvement in the accuracy of classification of CT scans enhanced using DDnet.

Figure 1, overall architecture of DL-FACT testing framework.
![image](https://user-images.githubusercontent.com/31482058/115868687-d7146b80-a40a-11eb-9368-d1e16bc94828.png)

Figure 2, lung CT image example before enhancement (left), lung CT image example after enhancment (right).
![image](https://user-images.githubusercontent.com/31482058/110122848-271d6d00-7d8e-11eb-80d7-b8641edfa9d3.png)

Figure 3, ROC curve of classification result of one testing. 
![image](https://user-images.githubusercontent.com/31482058/110995674-befbf780-8348-11eb-8f7a-85fd3d438cd7.png)

## Hardware requirements

For Enhancement Model:

The code can run without GPU. Running code with GPU could increase training and inference speed. PyTorch requires Nvidia GPUs with compute capability 6.0 or higher, i.e. any GPU from Pascal, Volta, Turing, Ampere series will work. Our code was tested on Nvidia V100, P100, T4 GPUs.

For Segmentation and Classification Model:

One or more Nvidia GPU. (2+GPUS are recommended for advanced features as AutoML). GPU version is only compatible with Nvidia GPUs having compute capability 6.0 or higher. Meaning, any GPU from Pascal, Volta, Turing, Ampere series will work.

## Software requirements

The Enhancement AI depends on Conda (version: conda 4.6.11), Python (version: 3.6.8), PyTorch (version: 1.0.1), Scikit-image (version: 0.13.1), PIL (version: 5.3.0), Matplotlib (version: 3.0.3), Nibabel (version: 3.2.1), and Cuda compilation tools (release 10.1, V10.1.105)

The Analysis AI require Nvidia-docker and Nvidia Clara SDK. If you already have docker installed then user should be in the docker group. Otherwise, sudo access is needed to install the prerequisite. Nvidia Clara SDK requires Nvidia CUDA 11.0.194 and Nvidia Driver release 450 or later.


## How to run
1. Run the [enhancement model](https://github.com/vtsynergy/2D-DECT). The enhancement model will generate pre-enhanced (original) CT scans (.nii) and post-enhanced CT scans.
2. (optional) Run the [Analyze AI](https://github.com/vtsynergy/Analyze-AI/tree/251bcf33df61851529e9cbcb1995c3f218f7f759). The segmentation program will automatically copy the imediate result generated by enhancement model and generate segmentaion mask images (.nii), and the classification program will automatically copy the segmentation mask image generated by segmentation models. The classification model will generate the positive and negative possibility score of each CT scan in a table (.csv).

## Data Citation
**LIDC-IDRI**: Armato III, SG; McLennan, G; Bidaut, L; McNitt-Gray, MF; Meyer, CR; Reeves, AP; Zhao, B; Aberle, DR; Henschke, CI; Hoffman, Eric A; Kazerooni, EA; MacMahon, H; van Beek, EJR; Yankelevitz, D; Biancardi, AM; Bland, PH; Brown, MS; Engelmann, RM; Laderach, GE; Max, D; Pais, RC; Qing, DPY; Roberts, RY; Smith, AR; Starkey, A; Batra, P; Caligiuri, P; Farooqi, Ali; Gladish, GW; Jude, CM; Munden, RF; Petkovska, I; Quint, LE; Schwartz, LH; Sundaram, B; Dodd, LE; Fenimore, C; Gur, D; Petrick, N; Freymann, J; Kirby, J; Hughes, B; Casteele, AV; Gupte, S; Sallam, M; Heath, MD; Kuhn, MH; Dharaiya, E; Burns, R; Fryd, DS; Salganicoff, M; Anand, V; Shreter, U; Vastagh, S; Croft, BY; Clarke, LP. (2015). Data From LIDC-IDRI. The Cancer Imaging Archive. http://doi.org/10.7937/K9/TCIA.2015.LO9QL9SX

**BIMCV**: Region, B. M. I. D. o t V., Pertusa, A., & de la Iglesia Vaya, M. (2020, June 9). BIMCV-COVID19+. https://doi.org/10.17605/OSF.IO/NH7G8

**MIDRC**: Tsai, E., Simpson, S., Lungren, M.P., Hershman, M., Roshkovan, L., Colak, E., Erickson, B.J., Shih, G., Stein, A., Kalpathy-Cramer, J., Shen, J., Hafez, M.A.F., John, S., Rajiah, P., Pogatchnik, B.P., Mongan, J.T., Altinmakas, E., Ranschaert, E., Kitamura, F.C., Topff, L., Moy, L., Kanne, J.P., & Wu, C. (2020). Data from the Medical Imaging Data Resource Center - RSNA International COVID Radiology Database Release 1a - Chest CT Covid+ (MIDRC-RICORD-1a).  Data from The Cancer Imaging Archive (2020). DOI: https://doi.org/10.7937/VTW4-X588.
