# 🏋️ AI Gym & Fitness Assistant

An all-in-one AI-powered fitness platform built as a Google Colab notebook, featuring **7 intelligent modules** that cover workout tracking, nutrition planning, habit analysis, and gym recommendations — all powered by modern machine learning and computer vision.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Modules](#modules)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)
- [Project Structure](#project-structure)
- [Requirements](#requirements)

---

## Overview

The AI Gym & Fitness Assistant is a comprehensive fitness intelligence system that combines computer vision, NLP, behavioral AI, and IoT simulation into a single Colab-ready notebook. It is designed to act as a full-stack fitness companion — from detecting your reps in real time to recommending the best gym near you.

---

## Modules

### Module 1 — AI Gym Trainer (Workout Detection)
**Tech: YOLOv8 Pose + NumPy**

Uses the YOLOv8 nano pose model to detect **17 body keypoints** (COCO layout) from video frames. Joint angles are computed from keypoint triplets (e.g., shoulder–elbow–wrist for a bicep curl) to count reps and provide real-time form feedback.

Supported exercises: Bicep Curl, Squat, Push-up, Shoulder Press, Lateral Raise

In notebook mode, realistic keypoint trajectories are simulated to demonstrate the full pipeline without a live camera.

---

### Module 2 — AI Dietician & Calorie Coach
**Tech: NLP + Rule-based AI**

A smart nutrition engine that calculates your BMI, daily calorie target (TDEE), and macronutrient breakdown based on your personal stats and fitness goals. It then assembles a full daily meal plan from an internal food database covering proteins, carbs, vegetables, fruits, and healthy fats.

Key features:
- BMI & TDEE calculation
- Goal-aware macro targeting (muscle gain, fat loss, maintenance)
- Personalized meal plan generation
- Nutrient breakdown per food item

---

### Module 3 — Smart Gym Assistant (IoT Simulation)
**Tech: Simulated IoT + ML**

Simulates a connected cardio machine (e.g., treadmill) generating real-time sensor data: speed, heart rate, and calories burned over a 30-minute session. The data follows realistic physiological curves using sine-wave patterns with Gaussian noise.

Outputs include a session summary, intensity phases, and a visual performance chart.

---

### Module 4 — AI Fitness Habit Tracker (Behavioral AI)
**Tech: scikit-learn Random Forest**

Trains a Random Forest classifier on synthetic behavioral data (sleep, stress, work hours, motivation, workout history) to predict whether a user will complete their workout on a given day. This module powers streak tracking and drop-off risk detection.

Key features:
- 500-user × 60-day behavioral dataset generation
- Workout completion prediction
- Feature importance analysis
- Streak and consistency tracking

---

### Module 5 — Virtual Gym Buddy (AI Chat Companion)
**Tech: Sentiment + Intent NLP**

A conversational fitness companion powered by keyword-based intent classification and a sentiment engine. The Gym Buddy understands topics like motivation, fatigue, diet, injury, and progress — and responds with contextually appropriate, encouraging messages.

---

### Module 6 — Pose-to-Performance Analyzer
**Tech: Motion Scoring**

Aggregates multiple workout metrics — form percentage, angle variance, reps completed, and average heart rate — into a single composite **Performance Score** (0–100). Weighted formula: 40% form + 25% consistency + 20% endurance + 15% effort.

---

### Module 7 — Gym Recommender & Planner
**Tech: Multi-criteria Scoring**

Recommends the best gym from a local database based on user preferences (budget, proximity, amenities like pool, classes, 24-hour access, personal training). Also generates a personalized weekly workout plan tailored to the user's goal and fitness level.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Computer Vision | YOLOv8 Pose (`ultralytics`) |
| Machine Learning | scikit-learn (Random Forest) |
| Data Processing | NumPy, Pandas |
| Visualization | Matplotlib, Seaborn |
| REST API | FastAPI + Uvicorn |
| Public Tunneling | pyngrok (ngrok) |
| Runtime | Python 3, Google Colab |

---

## Getting Started

### 1. Open in Google Colab

Upload `AI_Gym_Fitness_Assistant_7.ipynb` to [Google Colab](https://colab.research.google.com) or open it directly from Google Drive.

### 2. Install Dependencies

Run **Step 1** cell to install all required packages:

```bash
pip install ultralytics
pip install scikit-learn pandas numpy matplotlib seaborn
pip install fastapi uvicorn nest_asyncio
```

### 3. Run the Modules

Execute the cells in order from top to bottom. Each module is self-contained and can also be run independently after the core imports cell (Step 2) has been executed.

### 4. (Optional) Launch the Public REST API

To expose a live API endpoint via ngrok:

1. Sign up free at [ngrok.com](https://ngrok.com) and copy your auth token
2. Paste the token into the `NGROK_TOKEN` variable in the FastAPI cell
3. Run the cell — a public `https://xxxx.ngrok-free.app` URL will be printed
4. Open the URL in any browser to access the API and Swagger docs

---

## API Reference

The FastAPI backend exposes the following endpoints:

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Health check |
| GET | `/docs` | Swagger UI (interactive API docs) |
| POST | `/api/diet/meal-plan` | Generate a personalized meal plan |
| POST | `/api/trainer/analyze` | Analyze a workout session |
| POST | `/api/habit/predict` | Predict workout completion likelihood |
| POST | `/api/gym/recommend` | Get gym recommendations |

### Example: Meal Plan Request

```json
POST /api/diet/meal-plan
{
  "name": "Alex",
  "weight_kg": 75,
  "height_cm": 175,
  "age": 28,
  "gender": "male",
  "goal": "muscle_gain",
  "activity_level": "moderate"
}
```

---

## Project Structure

```
AI_Gym_Fitness_Assistant_7.ipynb
│
├── Step 1 — Install Dependencies
├── Step 2 — Core Imports
│
├── Module 1 — AI Gym Trainer (YOLOv8 Pose Detection)
├── Module 2 — AI Dietician & Calorie Coach
├── Module 3 — Smart Gym Assistant (IoT Simulation)
├── Module 4 — AI Fitness Habit Tracker
├── Module 5 — Virtual Gym Buddy (Chat)
├── Module 6 — Pose-to-Performance Analyzer
├── Module 7 — Gym Recommender & Planner
│
├── Final Dashboard — All Modules Summary
└── (Optional) FastAPI Backend — Public REST API via ngrok
```

---

## Requirements

- Python 3.8+
- Google Colab (recommended) or local Jupyter environment
- Internet connection (for package installation and ngrok tunneling)
- Free [ngrok account](https://ngrok.com) for the optional public API feature

---

## Dashboard

Upon running the Final Dashboard cell, a comprehensive **16×10 summary panel** is generated visualizing the output of all 7 modules:

- Rep count and form accuracy from the AI Trainer
- BMI, calorie target, and meal plan from the Dietician
- Session data and calories burnt from the IoT module
- Habit prediction accuracy from the Habit Tracker
- Gym Buddy interaction sample
- Composite performance score breakdown
- Gym recommendation and weekly plan

---

*Built with Python 3 · YOLOv8 · scikit-learn · FastAPI · Google Colab*
