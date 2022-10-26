# Reduced order digital twin and latent data assimilation for global wildfire probability prediction

## About The Project


The occurrence of forest fires can impact vegetation in the ecosystem, property, and human health, but also indirectly affect the climate. JULES-INFERNO is a global land surface model, which simulates vegetation, soils, and fire occurrence driven by environmental factors. However, this model incurs substantial computational costs due to the high data dimensionality and the complexity of differential equations. Deep learning-based digital twins have an advantage in handling large amounts of data. They can reduce the computational cost of subsequent predictive models by extracting data features through Reduced Order Modelling (ROM) and then compressing the data to a low-dimensional latent space. This study proposes a JULES-INFERNO-based digital twin fire model using ROM techniques and deep learning prediction networks to improve the efficiency of global wildfire predictions. Compared to JULES-INFERNO, the iterative prediction implemented in the proposed model can use current-year data to predict fires in subsequent years. To avoid the accumulation of errors from the iterative prediction, Latent data Assimilation (LA) is applied to the prediction process. LA periodically adjusts the prediction results to ensure the stability and sustainability of the prediction. The results show that the proposed model can effectively encode the original data and achieve accurate surrogate predictions. Furthermore, the application of LA can also effectively adjust the bias of the prediction results. The proposed digital twin also runs 500 times faster for online predictions than the original JULES-INFERNO model without requiring High-Performance Computing (HPC) clusters.


## Getting Started

### Hardware requirement

*   Programming language: Python (3.5 or higher)
*   Platform: Google Colab Pro
*   GPU: P100
*   Google Drive space: 200GB

### Software requirement

| Package Requirement                        |
|--------------------------------------------|
| os                                         |
| pandas                                     |
| math                                       |
| numpy                                      |
| netCDF4                                    |
| seaborn                                    |
| matplotlib                                 |
| tensorflow                                 |
| keras                                      |
| sklearn                                    |


## Dataset
All data for this project are from the JULES-INFERNO project. URL:
(https://imperiallondon-my.sharepoint.com/:f:/r/personal/mk1812_ic_ac_uk/Documents/Data/JULES-INFERNO?csf=1&web=1&e=3YXM21)


Four climate variables from 1961 to 1990: 
temperature (``LGM/drive/climate/CRU-NCEP-v7-LGM-n96e/tair``), humidity (``LGM/drive/climate/CRU-NCEP-v7-LGM-n96e/qair``), rainfall (``LGM/drive/climate/CRU-NCEP-v7-LGM-n96e/rain``) and lightning (``LGM/drive/lightning``). Additionally, each dataset contaions 360 snapshot, each size of snapshot is 144*192.


Five wildfire (Grid box mean burnt area fraction) datasets from 1961 to 1990: P1(``LGM/output/p1``), P2(``LGM/output/p2``), P2(``LGM/output/p2``), P3(``LGM/output/p1``), P4(``LGM/output/p4``) and P5(``LGM/output/p5``). Each set was driven by the same climatic conditions (1961 to 1990). However, JULES-INFERNO applied different initial internal states to ensure the robustness of its model; the internal state of P_1 was randomized, and the initial internal states of the subsequent experimental results were all the last internal states of the previous one. Therefore, although each result was for 1961-1990, there was variability.  Additionally, each dataset contaions 360 snapshot, each size of snapshot is 112*192.


## Implementation

### Data Prepocessing

`/Data_prepocessing/JULES_Data_preprocessing.ipynb` describes how to extract the specified features from the original data (netCDF4 files) and generate CSV files for storage.

### Climate data Encoding

`/Climate_CAE_construction/` directory stores CAE implementations for 4 climate conditions, including data processing, CAE model building, training and testing codes.

`/Trained_Models/para_mod/` catalogue contains trained CAE models for four climatic conditions respectively.

### Main Models

Files in `/AE_LSTM_LA/` directory contains data processing, ROM, LSTM, LA, performance anaylsis and performance comparison code. There are comparisons between different ROMs, as well as comparisons with and without LA.

The difference lies in ROM. `/AE_LSTM_LA/CAE_LSTM_LA_20.ipynb` compresses the original data into a 20-dimensional latent space by constructing CAE, `/AE_LSTM_LA/CAE_LSTM_LA_100.ipynb` compresses the original data into a 100-dimensional latent space by constructing CAE, `/AE_LSTM_LA/PCA_LSTM_LA_20.ipynb` compresses the original data into a 20-dimensional latent space by constructing PCA, and `/AE_LSTM_LA/PCA_LSTM_LA_100.ipynb` compresses the original data into a 100-dimensional latent space by constructing PCA.

`/Trained_Models/` catalogue contains 2 trained CAE models for fire data, one is to compress the data into 20 dimensions, and the other is to compress it into 100 dimensions. In addition, this directory contains 4 ROM_LSTM trained models: PCA_20_LSTM, PCA_100_LSTM, CAE_20_LSTM, CAE_100_LSTM.


### Output

`/output_figure/` folder holds the output images for this project, includes results' analysis and comparison.


## License

MIT License. More information see `LICENSE`


## Contact

Caili Zhong - zhongcaili17@126.com<br>
Sibo Cheng - sibo.cheng@imperial.ac.uk<br>
Matthewm Kasoar - m.kasoar12@imperial.ac.uk<br>
