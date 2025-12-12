# **UMN LIGO/Multi-Messenger Astronomy Machine Learning Notebook**

In this notebook you will:

1. Explore a dataset of gamma-ray bursts (GRBs) from Fermi
2. Build features from light curves (flux vs. time) and spectrograms (flux as a fucntion of time and energy/frequency)
3. Train a neural network to classify GRBs as short or long based on their prompt emission properties

# Useful Background Information

## Astrophysics, Multi-messenger Astronomy, Gamma-ray Bursts, Machine Learning

* Multi-messenger Astornomy Wikipedia: https://en.wikipedia.org/wiki/Multi-messenger_astronomy
* Gamma-ray Bursts (GRBs) Wikipedia: https://en.wikipedia.org/wiki/Gamma-ray_burst 
* Machine learning Wikipedia: https://en.wikipedia.org/wiki/Machine_learning 
* Machine learning tutorial: https://www.geeksforgeeks.org/machine-learning/machine-learning/
* Machine learning and Python tutorial: https://www.w3schools.com/python/python_ml_getting_started.asp

# Gamma-ray Bursts (GRBs)

Gamma-ray bursts (GRBs) are among the most powerful and energetic events observed in the universe. These brief but intense flashes of gamma radiation, lasting from milliseconds to several minutes, originate from distant galaxies and are thought to signal the collapse of massive stars or the merger of compact binary objects such as neutron stars or black holes. GRBs are broadly classified into two categories based on their duration: long GRBs (L-GRBs) and short GRBs (S-GRBs). The $T_{90}$ time is a crucial parameter in the classification of GRBs that quantifies the burst duration. It is defined as the duration during which 90\% of the burst's fluence (total energy) is accumulated. Specifically, the $T_{90}$ time is measured between the moments when 5\% and 95\% of the total fluence is detected. This parameter is instrumental in distinguishing between long and short GRBs. L-GRBs typically have a $T_{90}$ value greater than 2 seconds, indicating that they last longer and are usually associated with the collapse of massive stars into black holes, a process often linked to supernovae. In contrast, S-GRBs have a $T_{90}$ value less than 2 seconds and are thought to arise from the merger of compact objects, such as neutron stars or black holes. 

While the $T_{90}$ classification paradigm has been successful, it faces challenges with certain events that blur these boundaries. For instance, some long-duration GRBs like the kilonova events and some short GRBs associated with massive star collapses challenge the traditional classification scheme. Additionally, the rest-frame duration of GRBs can differ significantly from the observed duration due to cosmological redshift effects, further complicating classification efforts.

The *Fermi Gamma-ray Space Telescope*, launched in 2008, has revolutionized the study of GRBs. Equipped with the Gamma-ray Burst Monitor (GBM) and the Large Area Telescope (LAT), *Fermi* is capable of observing GRBs over a broad range of energies, from a few keV to several GeV. The GBM provides excellent time-resolution data in the form of light curves and spectrograms, enabling researchers to analyze the temporal and spectral properties of GRBs with unprecedented precision. However, the sheer volume of data collected by *Fermi* presents a significant challenge for manual classification of GRBs.

Understanding the distinction between L-GRBs and S-GRBs helps astrophysicists investigate the nature of stellar collapse, compact object mergers, and other high-energy astrophysical processes. It also plays a vital role in the identification of potential gravitational wave sources, particularly for S-GRBs, which are associated with the mergers of neutron stars — a leading source of gravitational waves. Moreover, precise GRB classification contributes to improving our models of cosmic structure formation and the evolution of galaxies, as the progenitors of these bursts are tied to the life cycle of stars and galaxies.

# Your Goal

Your goal is to train a model that can distinguish between long and short GRBs. Start with just the light curve data and then move to both light curve and spectrogram data. This model can demonstrate the potential of machine learning to efficiently categorize GRBs, enabling rapid characterization of their physical origins and contributing to the understanding of these energetic cosmic events.

Obviously a GRB can be classified by simply looking at the value for the $T_{90}$ time, but this project is attempting to classify these GRBs without $T_{90}$ and by only using light curve and spectrogram features.

# [The GRB Dataset in a Google Drive](https://drive.google.com/drive/folders/1CPqBuNXDQRUUQ8syJglJkSHSYcl9_H-a?usp=sharing)

In this study, you will explore the use of *PubSmartWaterfalls* (https://github.com/nmik/PubSmartWaterfalls), a tool designed to generate spectrogram representations of light curves, to create a labeled dataset of GRBs for classification purposes. This project uses a dataset consisting of 1,963 GRB events. Each event includes light curve and spectrogram data, which serve as the primary features for training the classification model. The light curve data consists of time-resolved flux measurements for each GRB, used to track the intensity over time. For each GRB event, we utilized time bins and flux values to model the temporal behavior. The best practice would have the dataset be split into training and testing sets. The training set can contain 80% of the total data (1,570 GRB events), and the testing set can have the remaining 20% (393 events). 
