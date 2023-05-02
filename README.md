# Hand-drawn Flowchart Recognition
## Team Members:
- Mu Chen, MS-SE (mu.chen@sjsu.edu) [SJSU ID: 014725425]
- Roger Kuo, MS-SE (roger.kuo@sjsu.edu) [SJSU ID: 013784706]
- Hardy Leung, MS-AI (kwok-shing.leung@sjsu.edu) [SJSU ID: 016711877] COORDINATOR
- Jasmine Wang, MS-AI (jasmine.wang@sjsu.edu) [SJSU ID: 002805362]

[Proposal](https://docs.google.com/document/d/1min_aHQF5sf6_ieqOGGpwV4Use2VStQybVCBv5W3MO8/edit?usp=sharing)

[Report](./report/report.pdf)

---

## Abstract
We propose to develop a method to recognize hand-drawn flowcharts to be used in software applications including word processors and presentation softwares. While many softwares provide functionality to recreate flowcharts using functionalities such as drawing circles, blocks, and arrows, they are often primitive and awkward to use. Anecdotal evidence suggests that many people avoid flowcharts due to such difficulty, despite the fact that flowcharts can often help succinctly summarize important concepts such as workflow and relationships. Our goal is to develop a DNN-based model that can take an image of a flowchart, and extract the blocks, text, arrows, and their relative positioning. Thereafter, the flowchart can be recreated in graphical applications.

## Coding and Training
Our approach will be based on either YOLO (v4 and above) or Faster R-CNN with fine-tuning on important flowchart elements such as blocks, circles, diamonds, arrows, and lines. Text elements will also be extracted and copied as-is (and extended to OCR in a future project). The main challenges of the project are: (1) acquiring dataset for training, (2) increasing the accuracy of the object detection, and (3) increasing the accuracy of the semantics we extract from the detected objects. We envision that the project entails a 4-stage process: (a) a preprocessing stage to cleanup the image based primarily on OpenCV, (b) an object detection stage using DNN such as a fine-tuned YOLO on our training dataset, and potentially specialized DNNs to classify elements such as lines beyond what YOLO can do, (c) an analysis stage that reconstruct the semantics of the flowchart, and (d) an assembly stage to save and recreate the flowchart in other formats suitable for further processing. We will provide an end-to-end demo of the whole process on real-world flowcharts.

If possible, we will build our training datasets from existing resources if available, including datasets of individual elements that allow us to classify individual flowchart elements, as well as complete flowchart for testing purposes. If needed, we will also manually create necessary training data to improve the performance.

## Software
Python 3, OpenCV 2, Pytorch 2.0, Matplotlib, YOLO (v4 or above) or Faster R-CNN.

Additional packages:
- Tesseract:
    - via Anaconda ```$ conda install -c conda-forge tesseract```
    - (Optional alternative for MacOS users): ```$ brew install tesseract```
- Other:
    - ```$ pip install pytesseract```
    - ```$ pip install schemdraw```

## Dataset

- [Dataset](https://cmp.felk.cvut.cz/~breslmar/flowcharts_offline/)
- [Dataset Preparation](https://docs.google.com/document/d/1iY2F0LpL9rOEVAxZMaGc8gkD9l-GDl9_IjW8bnVCrqw/edit?usp=sharing)

## Literature Review

- [Symbol detection in online handwritten graphics using Faster R-CNN](https://arxiv.org/pdf/1712.04833.pdf)
- [Arrow R-CNN for handwritten diagram recognition](https://www.researchgate.net/publication/348974392_Arrow_R-CNN_for_handwritten_diagram_recognition)
- [DrawnNet: Offline Hand-Drawn Diagram Recognition Based on Keypoint Prediction of Aggregating Geometric Characteristics](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8947756/pdf/entropy-24-00425.pdf)

---
## Instructions

How to setup and use the program:
1. Install Anaconda
2. Use the provided yaml file to create a conda environment 
    1. ```$ conda env create -f conda-cpu.yml```
    2. You can modify the yaml file to use a different environment name
3. Activate the environment 
    1. ```$ conda activate <insert_env_name>```
5. Install the additional packages listed above in the "Software" section
6. Run the detection script 
    1. ```$ python detection_custom.py```
    2. You can also add and use your own hand-drawn flowchart image to the main directory
    3. ```$ python detection_custom.py <insert_path_to_image>```

How to train a custom dataset:
- You can search through the [source repo](https://github.com/pythonlessons/TensorFlow-2.x-YOLOv3)
- Or look through their [main website](https://pylessons.com/)

---
## Model Evaluation

Enter in the terminal ```$ tensorboard --logdir=log``` and then navigate to http://localhost:6006/
### Training Loss
![Training Loss](./images/train.JPG)

### Validation Loss
![Validation Loss](./images/val.JPG)

### Sample Classification
![Sample Classification](./images/sample.png)
