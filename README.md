# Robot Perception – Maze Navigation Using Visual Place Recognition

This project explores visual place recognition–based navigation in a maze environment using classical computer vision techniques. The system simulates a robot navigating through a maze by identifying a target image and guiding navigation decisions based on visual similarity.

## Overview
The goal of this project is to enable a robot to recognize a target location
within a maze using camera input and image matching. The environment is
represented entirely by a dataset of maze images, which serve as the sole source
of visual information for place recognition and navigation.  
A baseline approach is included to provide a reference point for evaluating the
visual place recognition–based navigation strategy. The system extracts visual
features from exploration images, builds a compact representation database, and
performs real-time matching to estimate proximity to a target image. Navigation
decisions are generated based on these visual matches and displayed through an
interactive interface.


## Core Techniques
- **SIFT (Scale-Invariant Feature Transform)** for robust local feature extraction
- **VLAD (Vector of Locally Aggregated Descriptors)** for compact image representation
- **MiniBatch K-Means** for efficient codebook generation
- **BallTree** for fast nearest-neighbor image matching
- **Pygame** for visualization and user interaction

## System Pipeline
1. **Preprocessing**
   - Extract SIFT descriptors from exploration images
   - Generate a VLAD codebook using MiniBatch K-Means
   - Compute VLAD descriptors for all images
   - Build a BallTree for fast similarity search

<img width="362" height="228" alt="Screenshot 2026-01-21 at 7 45 08 PM" src="https://github.com/user-attachments/assets/c524416f-225a-4379-8104-bf47c5a4daa9" />

2. **Autonomous Mode**
   - Match current frame VLAD descriptors against the database
   - Estimate proximity to the target image
   - Execute navigation actions based on a precomputed action map
   - Perform proximity checks to confirm target reach

<img width="243" height="202" alt="Screenshot 2026-01-21 at 7 45 30 PM" src="https://github.com/user-attachments/assets/bf16cfe3-8201-427e-a12e-b2e5a37bd352" /> <img width="242" height="213" alt="Screenshot 2026-01-21 at 7 45 41 PM" src="https://github.com/user-attachments/assets/3f0cac1a-9461-485e-bf31-95c3aafb1a7a" />

3. **Semi-Autonomous Mode**
   - User manually controls navigation via keyboard input
   - System continuously computes VLAD similarity to the target
   - Closest match ID and distance are displayed in real time
   - User manually confirms arrival using a CHECKIN action
     
<img width="409" height="323" alt="Screenshot 2026-01-21 at 7 46 30 PM" src="https://github.com/user-attachments/assets/fcd89947-e708-429c-bdea-0420f4bbd79a" />

## Design Rationale
Fully autonomous navigation was initially attempted but suffered from drift due to sequential action execution. To improve robustness, a hybrid semi-autonomous approach was adopted, combining human control with real-time visual matching assistance. This design balances automation with reliability in visually ambiguous environments.

## Outputs
- VLAD feature database
- Codebook and BallTree index
- Real-time visualization of navigation state
- Video playback of navigation sequences

## Challenges and Observations
- Drift limited the reliability of fully autonomous navigation
- Sparse visual features in certain maze regions required parameter tuning
- MiniBatch K-Means significantly improved scalability for large datasets
- COLMAP-based 3D reconstruction was explored but not successfully integrated
