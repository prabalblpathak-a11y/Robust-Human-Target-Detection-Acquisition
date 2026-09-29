# 🎯 Robust Human Target Detection and Acquisition

> A Deep Learning and Computer Vision based system for robust human detection, multi-object tracking, target acquisition, occlusion handling, person re-identification, and target re-acquisition.

---

## 📌 About the Project

**Robust Human Target Detection and Acquisition** is a B.Tech major project focused on developing a computer-vision-based system capable of detecting multiple humans in a video or live camera feed, tracking them individually, and allowing a particular person to be selected as a target.

The main challenge addressed by this project is not only **detecting a person**, but also **maintaining the identity of the selected person over time**.

Real-world situations such as:

- Multiple people appearing simultaneously
- People crossing each other
- Partial or complete occlusion
- Temporary disappearance from the camera
- Re-entry into the frame
- Similar-looking individuals
- Changes in illumination
- Camera movement

can cause conventional tracking systems to lose or switch the identity of a person.

This project explores the integration of **Human Detection, Multi-Object Tracking (MOT), Target Acquisition, and Person Re-Identification (ReID)** to improve target identity consistency.

---

## 🎯 Project Objectives

The major objectives of the project are:

- Detect humans from live camera and recorded video streams.
- Detect multiple people simultaneously.
- Assign and maintain tracking IDs for detected individuals.
- Allow the user to select a particular person as the target.
- Continuously track the selected target.
- Identify situations in which the target becomes temporarily lost.
- Handle partial and temporary occlusion.
- Explore appearance-based Person Re-Identification.
- Attempt to re-acquire the same target after temporary disappearance.
- Evaluate tracking accuracy, identity consistency and system performance.
- Compare a baseline tracking system with an appearance/ReID-assisted approach.

---

## ❓ Problem Statement

Modern object detection models can accurately locate humans in images and video frames.

However, **human detection alone does not guarantee identity continuity**.

Consider a situation where several people are present:

```text
Person 1       Person 2       Person 3       Person 4
 ID: 1          ID: 2          ID: 3          ID: 4

                   ↓

             Select Person 3

                   ↓

             TARGET ACQUIRED
```

The system can initially track the selected person.

However, problems arise when:

```text
Person 3
   ↓
Moves Behind Another Person
   ↓
OCCLUSION
   ↓
Target Temporarily Disappears
   ↓
Tracking ID May Be Lost
   ↓
Person Reappears
   ↓
System Must Determine:
"Is this the same person?"
```

Maintaining the correct identity through these situations is the central problem explored by this project.

---

## 💡 Proposed Solution

The proposed system follows a modular **tracking-by-detection** approach.

```text
┌──────────────────────┐
│   Camera / Video     │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│   Frame Acquisition  │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│   Human Detection    │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Multi-Object Tracking│
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│   Target Selection   │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│  Target Acquisition  │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Continuous Tracking  │
└──────────┬───────────┘
           ↓
      Target Visible?
        /        \
      YES         NO
       ↓           ↓
    TRACK      TARGET LOST
                   ↓
          Appearance / ReID
                   ↓
           Candidate Search
                   ↓
          Target Re-Acquired
```

---

## 🔄 Target States

The selected target can move through four major states:

```text
ACQUIRED
   ↓
TRACKING
   ↓
LOST
   ↓
RE-ACQUIRED
```

These states help the system distinguish normal tracking from temporary identity loss and successful recovery.

---

## 🧠 Proposed Technologies

The following technologies and methods are currently being evaluated.

### Programming & Computer Vision

- Python
- OpenCV
- NumPy

### Deep Learning

- PyTorch
- YOLO-family Human Detection

### Multi-Object Tracking

Candidate tracking approaches include:

- ByteTrack
- BoT-SORT

### Person Re-Identification

Appearance-based Person Re-Identification techniques will be explored for recovering the selected target after temporary loss.

### Development

- Git
- GitHub
- VS Code

> **Note:** The final detector, tracker, ReID model and configurations will be selected after literature review, implementation, guide approval and experimental evaluation.

---

## 🔬 Research Direction

The project investigates whether adding **appearance/ReID-assisted target re-acquisition** can improve identity consistency compared with a conventional detection-and-tracking pipeline.

### Baseline Approach

```text
Human Detector
      ↓
Multi-Object Tracker
      ↓
Target Tracking
```

### Improved Candidate Approach

```text
Human Detector
      ↓
Multi-Object Tracker
      ↓
Target Acquisition
      ↓
Target Appearance Memory
      ↓
Target Lost
      ↓
Person Re-Identification
      ↓
Appearance + Tracking Information
      ↓
Target Re-Acquisition
```

The performance difference between these configurations will be experimentally evaluated.

---

## 📚 Literature Review Direction

Our literature review currently focuses on four major areas:

### 1. Human Detection in Crowded Environments

Crowded scenes introduce overlapping bounding boxes and partial occlusion, which can result in missed or incorrectly localized pedestrians.

Research areas studied include:

- Crowd-aware pedestrian detection
- Repulsion-based localization
- Adaptive Non-Maximum Suppression

### 2. Multi-Object Tracking

Multi-object tracking associates detected humans across consecutive frames.

Candidate approaches include:

- ByteTrack
- BoT-SORT
- Motion-based association
- Appearance-assisted association

### 3. Person Re-Identification

Person ReID attempts to determine whether a detected person corresponds to a previously observed identity.

Our research considers:

- Appearance embeddings
- Feature similarity
- Robust representation learning
- Re-identification after occlusion

### 4. Occlusion Handling

Occlusion is one of the major challenges addressed by the project.

We study:

- Partial occlusion
- Full temporary occlusion
- Crossing trajectories
- Target disappearance
- Target re-entry
- Appearance variation

---

## 🔎 Research Gap

Existing research provides strong solutions for individual components such as:

- Human detection
- Crowded pedestrian detection
- Multi-object tracking
- Person Re-identification
- Occlusion-aware feature extraction

However, our project focuses on integrating these ideas into an end-to-end workflow where:

1. Multiple humans are detected.
2. Their identities are tracked.
3. One person is explicitly selected as the target.
4. The target's state is monitored.
5. Temporary target loss is detected.
6. Appearance information can assist identity recovery.
7. The target is re-acquired when sufficient evidence indicates the same person has returned.

The project will experimentally investigate whether this integration improves target identity consistency under challenging conditions.

---

## 🧪 Testing Scenarios

The system is planned to be evaluated under multiple controlled scenarios.

### Basic Tests

- Single person
- Multiple people
- Stationary person
- Walking person

### Tracking Tests

- Multiple people walking simultaneously
- People crossing paths
- Different movement speeds
- Target moving between other people

### Occlusion Tests

- Partial occlusion
- Full temporary occlusion
- Target moving behind another person
- Target moving behind an object

### Re-Acquisition Tests

- Target leaves the frame
- Target re-enters the frame
- Similar-looking individuals
- Multiple possible target candidates

### Environmental Tests

Where feasible:

- Low illumination
- Different backgrounds
- Camera movement
- Crowded environments

---

## 📊 Evaluation Metrics

The final evaluation will use suitable metrics depending on the experimental setup and availability of ground-truth annotations.

Possible metrics include:

| Metric | Purpose |
|---|---|
| Precision | Accuracy of positive detections |
| Recall | Ability to detect actual humans |
| FPS | Real-time processing performance |
| ID Switches | Number of incorrect identity changes |
| IDF1 | Identity tracking consistency |
| MOTA | Multi-object tracking accuracy |
| HOTA | Combined detection and association quality |
| Re-Acquisition Success Rate | Successful target recoveries |
| Re-Acquisition Time | Time required to recover a lost target |

> Experimental values will be added only after implementation and testing.

---

## 👥 Team

### 👨‍💻 Prabal Pathak — Team Leader

**Responsibilities**

- System Architecture
- Module Integration
- Target Acquisition
- Project Coordination
- Research & Documentation
- Final Implementation Integration
- Presentation & Viva Coordination

---

### 👨‍💻 Veer Parekh

**Responsibilities**

- Human Detection Module
- Dataset Preparation
- Data Pre-processing
- Detection Model Evaluation
- Detection Testing

---

### 👨‍💻 Anant Parikh

**Responsibilities**

- Multi-Object Tracking
- Tracking Algorithm Integration
- Track ID Management
- Motion Association
- Occlusion Handling

---

### 👨‍💻 Arjun Awasthi

**Responsibilities**

- Person Re-Identification
- Target Re-Acquisition
- Testing
- Performance Evaluation
- Experimental Results & Metrics

---

### 🤝 Shared Responsibilities

All team members will contribute to:

- Literature Review
- Research Papers
- Testing
- Documentation
- Project Report
- Presentations
- Viva Preparation

---

## 🗂️ Repository Structure

```text
robust-human-target-detection-acquisition/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── src/
│   │
│   ├── detection/
│   │   └── Human detection module
│   │
│   ├── tracking/
│   │   └── Multi-object tracking module
│   │
│   ├── acquisition/
│   │   └── Target selection and acquisition
│   │
│   ├── reid/
│   │   └── Person Re-identification
│   │
│   ├── interface/
│   │   └── User interface / visualization
│   │
│   └── evaluation/
│       └── Performance evaluation
│
├── datasets/
│   └── Dataset information / scripts
│
├── tests/
│   └── Module and integration tests
│
├── notebooks/
│   └── Experimental notebooks
│
├── docs/
│   │
│   ├── research-papers/
│   ├── literature-review/
│   ├── synopsis/
│   ├── srs/
│   ├── presentations/
│   └── report/
│
├── results/
│   │
│   ├── screenshots/
│   ├── videos/
│   └── metrics/
│
└── main.py
```

---

## ⚙️ Installation

> Installation instructions will be finalized as implementation dependencies are frozen.

### 1. Clone the Repository

```bash
git clone <repository-url>
cd robust-human-target-detection-acquisition
```

### 2. Create Virtual Environment

```bash
python -m venv .venv
```

### 3. Activate Environment

#### Windows

```bash
.venv\Scripts\activate
```

#### Linux / macOS

```bash
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run

```bash
python main.py
```

---

## 🖥️ Expected System Output

The final interface is expected to display information such as:

```text
┌─────────────────────────────────────────────┐
│              LIVE CAMERA FEED               │
│                                             │
│     [ID 1]        [TARGET - ID 3]           │
│                                             │
│            [ID 2]                           │
│                                             │
├─────────────────────────────────────────────┤
│ Target Status : TRACKING                    │
│ Target ID     : 3                           │
│ Confidence    : --                          │
│ FPS           : --                          │
│ ID Switches   : --                          │
│ Lost Count    : --                          │
│ Re-Acquired   : --                          │
└─────────────────────────────────────────────┘
```

Values shown above are placeholders until experimental implementation is completed.

---

## 📈 Expected Outcomes

The project aims to produce:

- A functional human detection system
- Multi-person tracking with persistent track IDs
- Interactive target selection
- Target acquisition and state management
- Occlusion/loss detection
- Appearance-assisted target re-acquisition
- Real-time visualization
- Performance measurements
- Baseline vs improved-system comparison
- Documented limitations and future scope

---

## 🚧 Current Project Status

**Status:** 🟡 Under Development

Current work includes:

```text
Literature Review          ██████████  Ongoing
Requirement Analysis       ████████░░  Ongoing
System Design              ███████░░░  Ongoing
Detection Implementation   ██░░░░░░░░  Planned / Initial
Tracking Integration       ██░░░░░░░░  Planned / Initial
ReID Integration           ░░░░░░░░░░  Planned
Testing & Evaluation       ░░░░░░░░░░  Planned
Final Integration          ░░░░░░░░░░  Planned
```

> This section will be updated as development progresses.

---

## 🗓️ Development Roadmap

```text
Literature Review
       ↓
Problem & Research Gap
       ↓
Synopsis
       ↓
Software Requirements Specification
       ↓
System Architecture
       ↓
Human Detection
       ↓
Multi-Object Tracking
       ↓
Target Acquisition
       ↓
ReID / Re-Acquisition
       ↓
Integration
       ↓
Testing & Experiments
       ↓
Performance Evaluation
       ↓
Research Paper
       ↓
Final Report
       ↓
Project Demonstration
```

---

## 📄 Project Documentation

Project documentation will be maintained under the `/docs` directory.

Planned documents include:

- Major Project Synopsis
- Software Requirements Specification (SRS)
- Literature Review
- Research Paper Analysis
- System Architecture
- Presentation-I
- Presentation-II
- Presentation-III
- Project Report
- Research Paper-I
- Research Paper-II

---

## 📖 Research Papers Reviewed

The literature study currently includes work related to:

1. **Repulsion Loss: Detecting Pedestrians in a Crowd**
2. **Adaptive NMS: Refining Pedestrian Detection in a Crowd**
3. **NFormer: Robust Person Re-identification with Neighbor Transformer**
4. **Robust Pedestrian Attribute Recognition Using Group Sparsity for Occlusion Videos**
5. **Robust Human Target Detection and Aquisitions**

Additional literature will be added as the project progresses.

---

## 🔮 Future Scope

Depending on experimental results and available resources, future extensions may include:

- Multi-camera tracking
- Cross-camera Person Re-identification
- Edge-device deployment
- Improved occlusion handling
- More advanced appearance modelling
- Real-time analytics dashboard
- Larger benchmark evaluation
- Camera-motion compensation
- Improved crowded-scene tracking
- Automated experiment logging

---

## 🌐 Applications

Potential civilian and research applications include:

- Smart surveillance analytics
- Crowd monitoring
- Safety monitoring
- Human-aware robotics
- Restricted-area monitoring
- Computer Vision research
- Human movement analysis
- Academic experimentation

---

## ⚠️ Ethical Use & Disclaimer

This project is developed strictly for **academic, research, civilian computer-vision and safety-monitoring purposes**.

The term **“target”** in this repository refers to a **user-selected human subject for visual tracking and re-identification within a video stream**.

The project is not intended for autonomous weapon targeting, harmful surveillance, or automated high-stakes decision-making.

Any real-world deployment should consider privacy, consent, data protection and applicable laws.

---

## 🎓 Academic Information

**Project Title:**  
Robust Human Target Detection and Acquisition

**Project Type:**  
Major Project

**Program:**  
B.Tech — Computer Science & Engineering

**Institute:**  
Shri Vaishnav Institute of Information Technology

**University:**  
Shri Vaishnav Vidyapeeth Vishwavidyalaya

**Location:**  
Indore, Madhya Pradesh, India

**Academic Session:**  
2026–27

---

## 📚 References

The repository's final references will be maintained alongside the project report and research documentation.

Initial literature includes research on:

- Crowded pedestrian detection
- Repulsion Loss
- Adaptive NMS
- Multi-Object Tracking
- Person Re-Identification
- Occlusion-aware representation learning

All research papers, algorithms and external implementations used in the project will be appropriately cited.

---

## ⭐ Project Note

This repository represents an **ongoing academic research and development project**.

Models, algorithms, datasets, configurations, performance values and architecture may change based on:

- Literature review
- Guide feedback
- Experimental findings
- Hardware constraints
- Performance evaluation

No experimental performance result should be considered final until it has been reproduced and documented by the project team.

---

### Made for Major Project Research & Development

**Prabal Pathak • Veer Parekh • Anant Parikh • Arjun Awasthi**

Shri Vaishnav Vidyapeeth Vishwavidyalaya, Indore
