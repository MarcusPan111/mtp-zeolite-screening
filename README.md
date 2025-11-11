# Dataset Description

To facilitate model training and data management, all structures from *The Atlas of Prospective Zeolite Structures* were systematically encoded.  
The encoding scheme is as follows: each structure is represented by either a three-letter or four-letter code.  
Among them, the three-letter codes correspond to the 200 structures selected for DFT calculations,  
while the four-letter codes represent the remaining hypothetical structures.  
To distinguish them from experimental (IZA) zeolites, a suffix **“1”** is added to all encoded structures.

All encoding information is provided in **hypo_zeolite_structure_encoding_map.csv**.

- **train.csv** – Training dataset containing encoded structures and their features used for model training.  
- **prediction_input.csv** – Input data for model prediction.  
- **predicted_results.csv** – Model prediction results corresponding to the input file.
