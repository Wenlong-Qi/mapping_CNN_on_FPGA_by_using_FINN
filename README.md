# mapping_CNN_on_FPGA_by_using_FINN

In [ECG_Classification](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/ECG_Classification), 
a 2D CNN model, which is designed to detect heart anomalies in ECG monitoring signals, is introduced in Jupyter notebook shows hwo to train and compile a CNN model with FINN.
The details of training and compiling a CNN model with FINN as well as the verification are introduced in this notebook step by step. 
This notebook can be used as a guide to use FINN, it helps to understand the workflow of each experiment in 
[Master_Thesis](https://github.com/Wenlong-Qi/mapping_CNN_to_FPGA_by_using_FINN/tree/master/Master_Thesis) folder.

[Master_Thesis](https://github.com/Wenlong-Qi/mapping_CNN_to_FPGA_by_using_FINN/tree/master/Master_Thesis) consists of four experiments, 
which are used to generate different stitched IP Core for my master thesis. 
The training and compiling notebooks of each model as well as its corresponding ONNX models and parameters are upload together in this folder.

Although all the models here can be compiled with FINN successfully, it should be noticed that the compile workflow may not work for customized networks.
The document of FINN shows that the current implementation of streamlining is highly network-specific and may not work for your network if its topology is very different than the example network in [FINN](https://github.com/Xilinx/finn) github.
According to my experience, if your networks can not be compiled successfully, just adjusting the operations which are provided by FINN for the transformations in Step streamline and convert_to_HLS_layer. 
Before starting the automatic compiling step, I strongly recommand you to visualize the ONNX models (convert_to_hls.onnx, create_dataflow_partition.onnx and dataflow_parent.onnx) with Netron and check if all HLS layers are converted successfully.
