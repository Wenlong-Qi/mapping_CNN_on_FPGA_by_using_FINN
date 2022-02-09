This Jupyter notebook shows how to map a 2D CNN model on FPGA by using FINN toolchain.

The work in this notebook is based on *FINN v0.5* and used to detect heart anomalies in ECG monitoring signal. 
In general, 1D CNN model is a good choice to classify digital signal which is time-series data, but 1D Convolution was not supported by *FINN v0.5*, 
so a 2D CNN model is designed to classify the ECG signals instead of 1D CNN.

The details of training and compiling a CNN model with FINN as well as the verification are introduced in this notebook step by step. 
This notebook can be used as a guide to use FINN, it helps to understand the workflow of each experiment in [Master_Thesis](https://github.com/Wenlong-Qi/mapping_CNN_to_FPGA_by_using_FINN/tree/master/Master_Thesis) folder.
