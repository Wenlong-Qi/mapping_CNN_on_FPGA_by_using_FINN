This folder consists of four experiments, which are designed for my master thesis. 

Although 1D Convolution was supported from *FINN v0.6*, but there were still some bugs in 1D maxpool function in initial *FINN v0.6*. 
The developers have solved these problem now, so I update FINN to *COMMITE 8d02532* in my work environment.
Besides I update FINN-base to *COMMITE abaee5d* and pyverilator to *COMMITE 0c3eb93*, these make FINN work well.
It can be easily implemented by using *Dockerfile.finn* in this folder directly instead of the original file. 
If you use new release of FINN, it should be noticed that some configutations or steps may be different from the notebook in this repository, e.g. setting *DATATYPE*.

### 1. Experiment 1

In this experiment, a 2D CNN model based on LeNet is implemented and trained with [Brevitas](https://github.com/Xilinx/brevitas) in train_model notebbook, 
and the dataset is based on [Sign Language Digits Dataset](https://github.com/ardamavi/Sign-Language-Digits-Dataset). 
The model is designed for images at size (32,32) and with 2-bit and 4-bit parameters, the corresponding ONNX models and parameters are saved in save folder. 
You can re-train the model with different bit width but remember to change the save filename and path if needed. 
In compile_with_finn notebook, the workflow of FINN are shown. The steps including tidy-up, pre- and post-processing, streamline, convert to HLS-layer are shown in detail.
After compiling the model, a verification notebook is used to verify and creat test data if needed.
All the notebooks and files are in [Gesture_Recognizer](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/Gesture_Recognizer) folder.

### 2. Experiment 2 

In this experiment, a 1D CNN model is implemented and trained with 2-bit, 3-bit and 4-bit parameters, the dataset is from [MIT BIH Database](https://www.kaggle.com/mondejar/mitbih-database). 
Similar as above, the notebooks and coresponding files are in [ECG_1D](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/ECG_1D) folder.

### 3. Experiment 3

In this experiment, a 1D CNN model with depthwise seperable convolution is designed in [ECG_AF_1D](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/ECG_AF_1D) folder,
and an equivalent 2D CNN model is dsigned in [ECG_AF_2D](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/ECG_AF_2D) folder.
It should be noticed that the pointwise convolution should be converted into VVAU layer while converting to HLS layers, this is an extra step for depthwise seperable convolution compaired with above models.

### 4. Experiment 4

In this experiment, both 1D and 2D CNN models based on mAlexNet are designed for different image sizes of MNIST handwriting number. 
[MNIST](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/MNIST) folder contains all 1D and 2D CNN models with different input sizes and approaches.
For example, notebook train_model_2D is used to train the model with stride=1, notebook train_model_2D_with_stride_1 and train_model_2D_with_stride_2 are used to train the model with stride=3.
The compiling workflow of 1D and 2D CNN model are written in notebook compile_with_finn_multi_model. 
All the ONNX models, corresponding parameters and configurations are in [multi_model_test](https://github.com/Wenlong-Qi/mapping_CNN_on_FPGA_by_using_FINN/tree/master/Master_Thesis/MNIST/multi_model_test) folder.

### 5. Model Summary

Since FINN or Brevitas doesn't support model summary as PyTorch, I construct all the models with PyTorch. 
Then the amount of parameters in each layer in the models can be seen more clearly.



Although all the models here can be compiled with FINN successfully, it should be noticed that the compile workflow may not work for customized networks.
The document of FINN shows that the current implementation of streamlining is highly network-specific and may not work for your network if its topology is very different than the example network in [FINN](https://github.com/Xilinx/finn) github.
According to my experience, if your networks can not be compiled successfully, just adjust the operations which are provided by FINN for the transformation in Step streamline and Convert_to_HLS_layer. 
Before starting the automatic compiling step, I strongly recommand you to visualize the ONNX models (convert_to_hls.onnx, create_dataflow_partition.onnx and dataflow_parent.onnx) with Netron and check if all HLS layers are converted successfully.
