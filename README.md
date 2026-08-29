# 🌙 TrueSleep

An AI-powered smart alarm designed to help users get the amount of sleep they **actually need** by starting the sleep countdown when they fall asleep, rather than when they simply go to bed.

Traditional alarms assume:

```text
Time in Bed = Time Asleep
````

This application instead monitors sleep-related signals, estimates when the user actually falls asleep, and calculates a wake-up time based on:

* Detected sleep onset
* Requested sleep duration
* Optional hard wake deadline
* User sleep patterns
* Upcoming commitments

The system also learns from users over time and generates personalized sleep plans and sleep-trend summaries.

---

## 🎯 Core Idea

Instead of only asking:

> "What time do you want to wake up?"

the application focuses on:

> "How much sleep do you want, and when do you absolutely need to be awake?"

The alarm is calculated using:

```text
Wake Time =
min(
    Detected Sleep Onset + Requested Sleep Duration,
    Hard Wake Deadline
)
```

### Example

```text
Sleep Tracking Started: 10:30 PM
Detected Sleep Onset:   11:05 PM
Requested Sleep:        8 Hours
Hard Wake Deadline:     7:30 AM

Calculated Wake Time:   7:05 AM
Final Alarm:            7:05 AM
```

If the user falls asleep too late to receive their full requested sleep duration:

```text
Detected Sleep Onset:   12:15 AM
Requested Sleep:        8 Hours
Calculated Wake Time:   8:15 AM
Hard Wake Deadline:     7:30 AM

Final Alarm:            7:30 AM
```

The hard wake deadline acts as a safety limit.

---

## 🚀 How It Works

### 1. Create a Sleep Plan

Before going to sleep, the user selects:

* Desired sleep duration
* Optional hard wake deadline
* Upcoming events or commitments
* Pre-sleep habits

Example:

```text
Desired Sleep:      8 Hours
Hard Wake Deadline: 7:30 AM
Tomorrow:           9:00 AM Class
```

The user then starts sleep tracking.

---

### 2. Monitor Sleep-Related Signals

The application uses multimodal sensor data to understand the user's sleep state.

Signals can include:

* Accelerometer movement
* Audio features
* Breathing-pattern features
* Screen activity
* Phone interactions

These signals are processed together rather than relying on a single input.

```text
Accelerometer
      +
Audio
      +
Breathing Patterns
      +
Screen Activity
      ↓
TensorFlow Data Pipeline
      ↓
Sleep-State Classification
```

---

### 3. Detect Sleep State

A TensorFlow model classifies the user's state into categories such as:

```text
Awake
  ↓
Falling Asleep
  ↓
Asleep
```

Once the model detects that the user has transitioned into sleep, the application records the estimated sleep-onset time.

That timestamp becomes the starting point for the requested sleep duration.

---

### 4. Calculate the Alarm

The Flutter application calculates the final wake time using:

```text
Detected Sleep Onset
        +
Requested Sleep Duration
        ↓
Calculated Wake Time
```

If a hard deadline exists:

```text
Calculated Wake Time
        +
Hard Wake Deadline
        ↓
Earliest Valid Wake Time
```

This ensures the user gets as much of their requested sleep duration as possible without missing an important wake-up requirement.

---

## 🧠 7-Day Personalization Period

New users begin with a **7-day baseline period**.

During this period, the application observes the user's sleep-related patterns before heavily personalizing recommendations.

The system can analyze:

* Typical bedtime
* Average time required to fall asleep
* Phone usage before sleeping
* Estimated sleep duration
* Nighttime interruptions
* Wake-up patterns
* Pre-sleep habits
* User-reported sleep quality

```text
Days 1–7
    ↓
Collect Sleep Data
    ↓
Identify Patterns
    ↓
Establish User Baseline
    ↓
Improve Future Predictions
```

The goal is to build a personalized baseline rather than assuming every user has the same sleep behavior.

---

## 🌙 Pre-Sleep Check-In

Before starting a sleep session, users can record habits that may affect their sleep.

Examples include:

* ☕ Caffeine
* 📱 Screen time
* 🏃 Exercise
* 😰 Stress
* 🍽️ Late meals
* 📚 Studying
* 🎮 Gaming
* 💤 Daytime naps

Over time, the application can compare these behaviors against sleep outcomes.

Example:

```text
High Screen Activity
        ↓
Longer Sleep-Onset Time
```

```text
Late Caffeine
        ↓
Reduced Sleep Duration
```

```text
Exercise
        ↓
Improved Reported Sleep Quality
```

These insights are intended to help users understand their habits rather than provide medical conclusions.

---

## 📱 Phone Activity Tracking

Starting a sleep session does not necessarily mean the user immediately goes to sleep.

For example:

```text
10:30 PM → Sleep tracking starts
10:35 PM → User opens phone
10:42 PM → Phone is put down
10:48 PM → User opens phone again
```

The application can track phone and screen activity to avoid incorrectly treating this period as sleep.

If significant phone usage continues, the sleep-detection period can be adjusted or restarted.

```text
Sleep Tracking Starts
        ↓
Phone Activity Detected
        ↓
User Still Awake
        ↓
Continue Monitoring
        ↓
Sleep-Onset Detection
```

---

## 🤖 Machine Learning

The application uses **TensorFlow** to classify sleep states and estimate sleep onset from multimodal sensor data.

Potential model inputs include:

* Accelerometer movement
* Audio features
* Breathing patterns
* Screen activity
* Historical sleep behavior

The model is designed to distinguish between:

* Awake
* Falling asleep
* Asleep

```text
Multimodal Sensor Data
        ↓
TensorFlow Processing
        ↓
Feature Extraction
        ↓
Sleep-State Classification
        ↓
Sleep-Onset Detection
```

---

## 🌅 Morning Sleep Review

After waking up, the user receives a summary of their sleep session.

The morning review can include:

* Requested sleep duration
* Estimated sleep duration
* Detected sleep-onset time
* Time required to fall asleep
* Wake interruptions
* Alarm trigger reason
* Pre-sleep habits
* Comparison with previous nights

### Example

```text
Sleep Goal:             8h 00m
Estimated Sleep:        7h 32m
Time to Fall Asleep:    28 min
Wake Interruptions:     1
Alarm Trigger:          Hard Wake Deadline
```

The system can also explain why the user received less sleep than requested.

Example:

> You slept less than your 8-hour goal because your estimated sleep onset was later than usual and your 7:30 AM wake deadline limited your total sleep time.

---

## 📊 Sleep Pattern Insights

As more sessions are collected, the application can identify patterns in the user's behavior.

Example:

```text
Last 14 Days

Average Sleep Duration:
7h 18m

Average Time to Fall Asleep:
24 min

High Screen-Activity Nights:
Average Sleep-Onset Time = 33 min

Lower Screen-Activity Nights:
Average Sleep-Onset Time = 20 min
```

The goal is to turn sleep data into understandable trends instead of simply showing raw numbers.

---

## 📅 Personalized Sleep Planning

Users can add events or required wake times such as:

* Classes
* Work
* Meetings
* Exams
* Interviews
* Flights
* Appointments
* Personal commitments

The application can combine those requirements with historical sleep data.

```text
Upcoming Event
      +
Required Wake Time
      +
Requested Sleep Duration
      +
Historical Sleep Patterns
      ↓
Google Gemini API
      ↓
Personalized Sleep Plan
```

Example:

```text
Class:                  9:00 AM
Required Wake Time:     7:30 AM
Desired Sleep:          8 Hours
Average Sleep-Onset:    25 Minutes

Recommended Bedtime:    ~11:05 PM
```

---

# 🛠️ Tech Stack

## 📱 Flutter / Dart

The mobile application is built using **Flutter** and **Dart**.

Flutter is used to develop the duration-based smart alarm and support both iOS and Android from a shared codebase.

The mobile application handles:

* Sleep-plan creation
* Requested sleep duration
* Hard wake deadlines
* Sleep-session tracking
* Morning summaries
* Sleep insights
* Alarm logic
* Sensor-data integration

The duration-based alarm calculates wake time from:

```text
Detected Sleep Onset
        +
Requested Sleep Duration
        +
Optional Hard Wake Deadline
        ↓
Final Wake Time
```

---

## 🧠 TensorFlow

**TensorFlow** is used to build the machine learning and data-processing pipeline.

The pipeline processes multimodal sensor data including:

* Accelerometer signals
* Audio signals
* Breathing-pattern features
* Screen-activity signals

The processed data is used to classify:

```text
Awake
Falling Asleep
Asleep
```

The resulting sleep-state predictions allow the system to identify the estimated transition into sleep.

---

## ☁️ Azure Machine Learning

**Azure Machine Learning** is used to train, evaluate, and compare TensorFlow models.

Azure ML supports:

* Model training
* ML pipeline execution
* Model evaluation
* Experiment comparison
* Training configuration
* Model lifecycle management

```text
Processed Sensor Data
        ↓
Azure Machine Learning
        ↓
TensorFlow Training
        ↓
Model Evaluation
        ↓
Performance Comparison
```

---

## 🗃️ Azure Blob Storage

**Azure Blob Storage** is used to store data and machine learning artifacts used by the training pipeline.

This can include:

* Processed sensor datasets
* Training datasets
* Validation datasets
* Model artifacts
* Experiment outputs

Sensitive raw data is minimized where possible, with processed features used instead when appropriate.

---

## 📊 MLflow

**MLflow** is used to track machine learning experiments and compare model performance.

MLflow tracks information such as:

* Training parameters
* Model configurations
* Evaluation metrics
* Experiment results
* Performance between training runs

```text
Experiment 1 ──► Metrics
Experiment 2 ──► Metrics
Experiment 3 ──► Metrics
                    ↓
                  MLflow
                    ↓
             Compare Performance
                    ↓
             Select Best Model
```

This allows different TensorFlow models and configurations to be evaluated consistently.

---

## 📦 Azure ML Model Registry

Trained models are versioned using **Azure ML Model Registry**.

The registry is used to:

* Track model versions
* Store trained models
* Compare model iterations
* Preserve previous versions
* Select deployment candidates

```text
Model v1
Model v2
Model v3
   ↓
Azure ML Model Registry
   ↓
Best-Performing Model
```

---

## 📲 TensorFlow Lite

After evaluation, the best-performing model is exported to **TensorFlow Lite**.

TensorFlow Lite allows sleep-onset inference to run directly on the user's mobile device.

The deployed model can process:

* Audio
* Motion
* Screen activity

```text
Audio
  +
Motion
  +
Screen Activity
  ↓
TensorFlow Lite
  ↓
Sleep-State Prediction
  ↓
Sleep-Onset Detection
```

On-device inference provides:

* Lower latency
* Offline functionality
* Reduced cloud dependency
* Reduced transfer of sensitive sensor data
* Improved privacy

---

## 🔐 Firebase Authentication

**Firebase Authentication** is used to securely manage application accounts.

It supports:

* User registration
* User login
* Authentication sessions
* Account identity management

Authentication ensures that sleep-session information is associated with the correct account.

---

## 🗄️ Cloud Firestore

**Cloud Firestore** is used to store application and sleep-session data.

Stored information can include:

* Sleep-session summaries
* Requested sleep duration
* Detected sleep onset
* Alarm information
* User preferences
* Pre-sleep check-ins
* Historical sleep trends

```text
Sleep Session
      ↓
Sleep-Onset Detection
      ↓
Session Summary
      ↓
Cloud Firestore
```

The architecture prioritizes storing summarized information instead of permanently storing unnecessary raw sensor data.

---

## ✨ Google Gemini API

The **Google Gemini API** is used to generate personalized sleep plans and trend summaries.

Gemini receives structured information such as:

* Historical sleep duration
* Average sleep-onset time
* Hard wake deadlines
* Requested sleep duration
* Pre-sleep habits
* Previous sleep summaries
* Detected trends

```text
Sleep History
      +
Wake Deadline
      +
Requested Sleep Duration
      +
Detected Patterns
      ↓
Google Gemini API
      ↓
Personalized Sleep Plan
      +
Trend Summary
```

The Gemini integration is designed to meet a **sub-200ms p99 latency SLO**, allowing personalized sleep-planning responses to be generated quickly.

Gemini is responsible for interpreting existing sleep information and producing understandable recommendations, while TensorFlow is responsible for sleep-state classification and sleep-onset detection.

---

# 🧪 Machine Learning Pipeline

The complete model-development pipeline follows:

```text
Multimodal Sensor Data
        ↓
Azure Blob Storage
        ↓
TensorFlow Data Processing
        ↓
Azure Machine Learning
        ↓
TensorFlow Model Training
        ↓
MLflow Experiment Tracking
        ↓
Model Performance Comparison
        ↓
Azure ML Model Registry
        ↓
Best-Performing Model
        ↓
TensorFlow Lite Export
        ↓
On-Device Sleep-Onset Inference
```

This separates cloud-based model development from mobile inference.

**Azure Machine Learning**, **Azure Blob Storage**, and **MLflow** support model training and experimentation, while **TensorFlow Lite** performs sleep-state inference directly on the user's device.

---

# 🏗️ High-Level Architecture

```text
                    ┌─────────────────────┐
                    │     Flutter App     │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
          ▼                    ▼                    ▼
   Accelerometer             Audio           Screen Activity
          │                    │                    │
          └────────────────────┼────────────────────┘
                               │
                               ▼
                    TensorFlow Data Pipeline
                               │
                               ▼
                 Awake / Falling Asleep / Asleep
                               │
                               ▼
                    Sleep-Onset Detection
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
          Flutter Alarm Logic         Session Summary
                                             │
                               ┌─────────────┴─────────────┐
                               │                           │
                               ▼                           ▼
                      Cloud Firestore              Google Gemini API
                               │                           │
                               ▼                           ▼
                         Sleep History           Personalized Plans
                                                 & Trend Summaries
```

---

# 🔧 Technologies

| Category            | Technology                                             | Purpose                                                     |
| ------------------- | ------------------------------------------------------ | ----------------------------------------------------------- |
| Mobile              | **Flutter / Dart**                                     | Build the duration-based smart alarm and mobile application |
| Machine Learning    | **TensorFlow**                                         | Process multimodal sensor data and classify sleep states    |
| ML Platform         | **Azure Machine Learning**                             | Train, evaluate, and compare models                         |
| ML Storage          | **Azure Blob Storage**                                 | Store processed datasets and ML artifacts                   |
| Experiment Tracking | **MLflow**                                             | Track experiments and compare model performance             |
| Model Management    | **Azure ML Model Registry**                            | Version and manage trained models                           |
| On-Device ML        | **TensorFlow Lite**                                    | Run sleep-onset inference directly on the device            |
| Authentication      | **Firebase Authentication**                            | Secure user accounts                                        |
| Database            | **Cloud Firestore**                                    | Store sleep-session summaries and user data                 |
| Generative AI       | **Google Gemini API**                                  | Generate personalized sleep plans and trend summaries       |
| Sensor Inputs       | **Audio, Motion, Breathing Patterns, Screen Activity** | Multimodal sleep-state features                             |
| Alarm Logic         | **Flutter + Native Alarm APIs**                        | Schedule duration-based and deadline-aware alarms           |

---

# 🔒 Why Is This Repository Private?

The source code for this project is currently **private and not publicly available**.

The application works with sensitive user information related to sleep behavior, device activity, and personalized machine learning.

This can include:

* Sleep patterns
* Sleep-session information
* Device movement
* Audio-derived features
* Breathing-pattern features
* Screen activity
* User schedules
* Pre-sleep habits
* Authentication information
* User-specific ML data
* Historical sleep trends

The implementation also contains backend and infrastructure logic responsible for securely processing, authenticating, and storing this data.

Because of the privacy and security requirements associated with this information, the implementation is intentionally kept private.

---

# 🛡️ Privacy-First Architecture

Privacy is treated as a core architectural requirement.

The application is designed to:

* Perform TensorFlow Lite inference on-device
* Minimize transfer of sensitive sensor data
* Avoid permanently storing raw microphone recordings
* Store summarized session information when possible
* Protect accounts through Firebase Authentication
* Separate individual user data
* Restrict access to private information
* Reduce unnecessary cloud processing
* Keep alarm functionality independent from cloud availability

Preferred data flow:

```text
Raw Sensor Signals
        ↓
Local Feature Processing
        ↓
TensorFlow Lite
        ↓
Sleep-State Prediction
        ↓
Sleep-Onset Estimate
        ↓
Store Minimal Session Summary
```

Keeping the source code private also reduces exposure of implementation details involving:

* Authentication
* User-data storage
* Sensor processing
* ML pipelines
* Backend configuration
* Privacy controls
* Personalized sleep data

---

# 🔐 Privacy Goals

Long-term privacy goals include:

* On-device ML inference
* Minimal cloud data collection
* No permanent raw audio storage
* Secure authentication
* Per-user authorization
* Data encryption
* Clear user consent
* User-controlled deletion
* Aggregated or anonymized analytics where appropriate

---

# ⚠️ Technical Challenges

## Background Monitoring

Mobile operating systems restrict continuous background execution.

The application must account for:

* iOS background restrictions
* Android background services
* Microphone permissions
* Sensor permissions
* Alarm reliability
* Battery optimization

---

## Sleep Detection Accuracy

Phone-based sleep detection cannot guarantee medically accurate sleep measurements.

The system estimates sleep states from consumer-device signals and should be treated as a behavioral estimation tool rather than a clinical sleep monitor.

---

## Battery Usage

Continuous use of:

* Accelerometer signals
* Audio processing
* Screen-activity monitoring

must be optimized to reduce overnight battery consumption.

---

## Privacy & Security

Sleep patterns, behavioral data, audio-derived signals, and device activity can contain sensitive information.

Privacy and security therefore remain important requirements throughout development.

---

# 🎯 Project Goal

A traditional alarm works like this:

```text
Go to Bed
    ↓
Set Alarm
    ↓
Assume Time in Bed = Time Asleep
    ↓
Wake Up
```

This application instead follows:

```text
Start Sleep Tracking
        ↓
Monitor Multimodal Signals
        ↓
Classify Sleep State
        ↓
Detect Sleep Onset
        ↓
Start Requested Sleep Duration
        ↓
Consider Hard Wake Deadline
        ↓
Schedule Alarm
        ↓
Generate Morning Summary
        ↓
Analyze Sleep Patterns
        ↓
Generate Personalized Sleep Plan
```

The long-term goal is to create a smart alarm that becomes increasingly personalized as it learns how each user actually sleeps.

---

# ⚠️ Disclaimer

This project is intended for sleep planning, personal insights, and behavioral tracking.

Sleep-state predictions and sleep-duration estimates generated from consumer-device sensors and machine learning are **not medical measurements** and are not intended for diagnosis, treatment, or clinical sleep monitoring.

```
