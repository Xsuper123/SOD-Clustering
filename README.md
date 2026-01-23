# Satellite Object Detection (SOD)-Clustering Dataset

## Related Publications
Please cite the original paper when using the dataset:
- P. Hu and W. Zhang, "AI-Driven Collaborative Satellite Object Detection for Space Sustainability," 2025 IEEE International Conference on Wireless for Space and Extreme Environments (WiSEE), Halifax, NS, Canada, 2025, pp. 1-6, [doi: 10.1109/WiSEE57913.2025.11229836](https://ieeexplore.ieee.org/document/11229836). [arXiv link](https://doi.org/10.48550/arXiv.2508.00755)


## Dataset Generation

This dataset is designed to simulate scenarios involving multiple nearby satellites capturing the same scene from slightly offset positions but identical viewing angles. The goal is to study how a multi-view setting influences satellite object detection. We fix the cluster size at three satellites in this dataset.

A satellite cluster consists of three satellites whose camera positions all lie within a given spatial radius:
- Satellite 1: Central satellite  
- Satellite 2 and 3: Secondary satellites

In each image, the central satellite observes at least one object of interest (another satellite in the simulation) at a distance between 0.5 km and 2 km from the camera. We define cluster types based on the spatial radius around the central satellite:

- `close` cluster: both secondary satellites within 0.5 km  
- `mid` cluster: both secondary satellites within 1 km  
- `far` cluster: both secondary satellites within 2 km  

Secondary satellite positions are uniformly sampled within these distance constraints while maintaining identical camera orientations. Each secondary satellite is also positioned to ensure that it observes at least one object of interest within the scene.

## Dataset Structure

The dataset is organized by `cluster size`, with three categories: `close`, `mid`, and `far`, representing the proximity between satellites within a cluster. The dataset is structured as follows:
```
close/
├── images/
└── labels/
mid/
├── images/
└── labels/
far/
├── images/
└── labels/
```
The file naming convention distinguishes between viewpoints within a satellite cluster:

- Filenames in the format `image##.jpg` refer to images captured by the central satellite in the cluster.
- Filenames in the format `image##_s1.jpg` and `image##_s2.jpg` correspond to images captured by secondary satellites.

Each image has a corresponding label file in the `labels/` folder. For every image file, there are two label files:

- `image##.txt`: Contains bounding box annotations for objects of interest  
- `image##_full.txt`: Contains extended metadata for the observing satellite and all visible objects of interest

The `image##_full.txt` files store additional parameters, including satellite position and orbital data, enabling scene-level understanding beyond bounding boxes. A full description of these metadata fields is provided in the following section.


## Metadata Description
### For the observing satellite (per image):
- Latitude, longitude, and altitude  
- Orbital inclination  
- Right Ascension of the Ascending Node (RAAN)

### For each object of interest:
- Object ID  
- Screen position (image coordinates)  
- Bounding box annotation  
- Distance from the observing satellite  
- Geographic coordinates (latitude, longitude, altitude)  
- Orbital parameters (orbital inclination, RAAN)


## Authors
Wenxuan Zhang and Peng Hu

## License
This dataset is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0) https://creativecommons.org/licenses/by/4.0/


