# [Predicting Solar Flares Using a Long Short-term Memory Network](https://iopscience.iop.org/article/10.3847/1538-4357/ab1b3c)

Hao Liu <sup>1,2</sup>, Chang Liu <sup>1, 3, 4</sup>, Jason T. L. Wang <sup>1, 2</sup>, and Haimin Wang <sup>1, 3, 4</sup>

1. Institute for Space Weather Sciences, New Jersey Institute of Technology
2. Department of Computer Science, New Jersey Institute of Technology
3. Big Bear Solar Observatory, New Jersey Institute of Technology
4. Center for Solar-Terrestrial Research, New Jersey Institute of Technology


# Abstract

We present a long short-term memory (LSTM) network for predicting whether an active region (AR) would produce a ϒ-class flare within the next 24 hours. We consider three ϒ classes, namely ≥M5.0 class, ≥M class, and ≥C class, and build three LSTM models separately, each corresponding to a ϒ class. Each LSTM model is used to make predictions of its corresponding ϒ-class flares. The essence of our approach is to model data samples in an AR as time series and use LSTMs to capture temporal information of the data samples. Each data sample has 40 features including 25 magnetic parameters obtained from the Space-weather HMI Active Region Patches (SHARP) and related data products as well as 15 flare history parameters. We survey the flare events that occurred from 2010 May to 2018 May, using the GOES X-ray flare catalogs provided by the National Centers for Environmental Information (NCEI), and select flares with identified ARs in the NCEI flare catalogs. These flare events are used to build the labels (positive vs. negative) of the data samples. Experimental results show that (i) using only 14-22 most important features including both flare history and magnetic parameters can achieve better performance than using all the 40 features together; (ii) our LSTM network outperforms related machine learning methods in predicting the labels of the data samples. To our knowledge, this is the first time that LSTMs have been used for solar flare prediction. 


# Reference 

Predicting Solar Flares Using a Long Short-term Memory Network. Liu, H., Liu, C., Wang, J. T. L., Wang, H., ApJ., 877:121, 2019. [link](https://iopscience.iop.org/article/10.3847/1538-4357/ab1b3c)


# Usage

1. There are three folders named C, M, M5 containing data samples in >=C, >=M, >=M5.0 class respectively as described in Table 2.

	In each folder, there are 3 csv files named training, validation, testing respectively, which contain data samples (before normalization) as described in Table 2.
In addition, there are 3 csv files named normalized_training, normalized_validation, normalized_testing respectively, which contain data samples (after normalization) as described in Table 2.

	The column headers for a data sample in each csv file are 
		- label, indicating whether the data sample is positive or negative;  
		- flare, representing the class of the flare within the next 24 hours where "N" indicates no flare occurs within the next 24 hours;  
		- timestamp, denoting the observation time of the data sample;  
		- NOAA, denoting the NOAA active region number;
		- HARP, denoting the corresponding HARP number;
		- 40 features where the order of the features is consistent with the order of features described in Figures 5, 6 and 7 for the three different flare classes.


2. The raw data folder contains raw data in raw_data.csv, downloaded directly from JSOC. The raw_data.csv file includes incomplete data samples, which have at least one missing physical feature value. Our program removes these incomplete data samples to get the data samples described in Table 2. The data samples are collected at a cadence of 1 hour.


3. In the folder named Table5_dataset_and_source_code, it contains one folder, named C, containing data samples in the >=C class. In the folder, there are three csv files named normalized_training, normalized_validation, normalized_testing respectively, which contain training, validation and testing data samples (after normalization).

	The difference between these three csv files and those of Table 2 is that these three csv files contain incomplete data samples that have at least one missing physical feature value. After removing these incomplete data samples, one would get the same data samples as described in Table 2. 

	This zip also contains the source code of our program, called LSTMpredict.py, which is used to calculate the performance metric values for the >=C class as described in Table 5. Our program will (i) automatically remove the incomplete data samples in the three csv files; (ii) apply the zero-padding strategy; (iii) select and use the 14 most important features for the >=C class; (iv) perform the cross-validation test as described in the paper.

	The usage is given as follows:
		python3 LSTMpredict.py C
	
	The first argument "LSTMpredict.py" is the Python program file name.
	The second argument "C" denotes that the program will run for the >=C class.

	The output obtained by executing the above command is stored in the file named output in the zip. This output file contains the performance metric values calculated by our program using the optimal threshold that maximizes TSS.

	Our program is run on Python 3.6.8, Keras 2.2.4, and TensorFlow 1.12.0.

