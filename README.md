# Secured-Home-Automation-with-Voice-Recognition
A Raspberry Pi–based home automation prototype that identifies the speaker using a Machine Learning model and can be extended to trigger IoT appliances (demo uses LED/relay-style control).
​

# Project overview
This project implements a voice-controlled smart home automation workflow with a focus on security through speaker identification (so only recognized speakers can activate actions).
​
The speaker recognition pipeline uses MFCC feature extraction and a Gaussian Mixture Model (GMM) classifier, trained from recorded voice samples.
​

# Features
Speaker identification using Gaussian Mixture Model (GMM).
​

Feature extraction with MFCC + delta features for audio-based modeling.
​

CLI menu to record training samples, train models, record test audio, and run inference.
​

Designed for Raspberry Pi deployment and IoT integration (relay/LED mentioned as target appliance demo).
​

# Hardware and software
# Hardware (prototype setup)
Raspberry Pi 4 Model B (8GB) and SD card storage.
​

Microphone + sound card (as listed in the project).
​

Relay module + LED (or other appliance load via relay).
​

# Software / environment
Raspberry Pi OS (Linux) and Python.
​

Python libraries used in code: pyaudio, numpy, scikit-learn, scipy, python_speech_features, pickle.
​

# Dataset
The project reports initial testing on the TensorFlow Speech Commands dataset and later a custom dataset recorded from 40 students with variations (near/far mic, slow/fast pace).
​
MFCC (Mel-Frequency Cepstral Coefficients) features are used for training and recognition.
​

# Repository structure (expected)
The script uses the following folders/files (create them if missing):
​

./trainingset/ – stores training WAV files recorded via the script.
​

./testingset/ – stores testing WAV files recorded via the script.
​

./trainedmodels/ – stores trained .gmm model files (pickled).
​

trainingset_addition.txt – list of training WAV filenames appended during recording.
​

testingset_addition.txt – list of test WAV filenames written during test recording.
​

# How it works
Record voice samples for each user (training audio).
​

Extract MFCC + delta features from each sample and train a GMM per speaker.
​

Record a test clip and compute log-likelihood against all trained speaker models to predict the best match (or label as unknown under a threshold).
​

# Setup and run
1) Create folders
bash
mkdir -p trainingset testingset trainedmodels
2) Install dependencies
Install required Python packages (exact versions are not pinned in the shared code):
​

bash
pip install numpy scipy scikit-learn pyaudio python_speech_features
3) Run the program
bash
python3 raspFinal.py
4) Menu options
The script provides an interactive menu:
​

Record audio for training

Train model

Record audio for testing

Test model

During recording, it prints available input devices and prompts for the device index.
​

# Results (from pdf)
The report includes evaluation using datasets with “80 variations” and “60 variations” per the described recording setup and trial tables.
​
Performance is reported using an accuracy formula: (Number of Correct Output / Number of Trials) × 100.
​

# Limitations
Accuracy depends strongly on environment conditions and voice variations (accent, distance, pace).
​

IoT devices/network may be susceptible to cyber attacks if deployed without proper security hardening.
​

Internet dependency and device compatibility can be practical constraints in real deployments.
​

# Future work
Expand from LED/relay demo to controlling more real appliances (AC, lighting, etc.).
​

Improve robustness with a larger custom dataset and better handling of noise/accent variation.
​

Add alerting/notification (e.g., message when the device is activated).
​
