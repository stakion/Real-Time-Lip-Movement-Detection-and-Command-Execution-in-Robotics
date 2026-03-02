# Real-Time-Lip-Movement-Detection-and-Command-Execution-in-Robotics
## Abstract
The main purpose of the project focuses on leveraging modern technology to enable human-robot or human-computer interaction. Specifically, the project utilizes Media Pipe to detect lip movements (comparing information of mean difference lips gap in the actual frame vs the last frame ). This mechanism triggers the Whisper system to convert spoken instructions into text. Subsequently, a large language model (LLM) powered by LangChain and Ollama performing the process of the text to interpret and execute commands within a simulated drone environment in Gazebo on Ubuntu 22.04 LTS

## Objectives:
### General:
To design, implement, and evaluate a multimodal human–robot interaction system that integrates computer vision, automatic speech recognition, and large language models to interpret natural language commands and execute real-time drone control within a simulated robotic environment.

### Specific:
1. To implement a facial landmark-based algorithm that detects lip movement in real time by analyzing the mean difference between upper and lower lip coordinates to trigger speech recording.
2. To incorporate OpenAI Whisper for converting recorded audio signals into structured textual representations suitable for natural language processing.
3. To implement a classification framework using LangChain and locally deployed LLMs (LLaMA via Ollama) that:

  Identifies the user’s command intent (movement, landing, stop, etc.)
  Determines the directional axis of motion (X/Y/Z ±)

4. To deploy large language models locally and evaluate their performance (LLaMA 2 vs LLaMA 3) in terms of inference latency and classification effectiveness under hardware constraints.
5. To design and tune a PID controller capable of executing movement commands in a Gazebo-based drone simulation environment.
6. To evaluate multithreading, multiprocessing, and concurrent futures approaches in order to mitigate latency introduced by speech transcription and LLM inference.
7. To analyze hardware bottlenecks, ASR latency, LLM response time, and environmental biases (lighting, occlusion, noise) affecting real-time multimodal interaction.


## Research Questions
1. How feasible and effective is the integration of computer vision-based lip movement detection, automatic speech recognition (Whisper), and locally deployed large language models for real-time human–robot interaction?

2. What are the primary computational and architectural bottlenecks that affect real-time execution when deploying Whisper and LLaMA models locally in a robotics control loop?

3. To what extent can large language models (via LangChain and Ollama) reliably classify and interpret natural language commands for structured robotic control tasks in simulated environments?


## Related Work
The related work demonstrates advances in automatic speech recognition integration in robotics, LLM-based pipeline orchestration via LangChain, natural language database interfaces, and real-time computer vision using MediaPipe. While prior research explores these technologies independently—particularly in ROS environments, medical information retrieval, chatbot systems, and gesture recognition—none combine lip-based activation, ASR transcription, local LLM reasoning, and PID-based robotic control into a unified multimodal real-time interaction system.


## Pipeline structure
1. Lip Movement Detection
  MediaPipe detects facial landmarks.
  Upper and lower lip Y-coordinates are averaged.
  A mean difference threshold triggers speech recording.

2. Speech Recognition
  Audio is recorded using sounddevice.
  Whisper transcribes speech into text.
  CSV logs are generated for tracking.

3. Natural Language Classification
  LLaMA (via Ollama) classifies commands into:
    Movement
    Position recovery
    Orientation recovery
    Velocity queries
    Takeoff / Landing / Stop
  A second classification determines axis direction (X/Y/Z ±).

4. Drone Control 
  Commands are interpreted and sent to a Gazebo drone simulation.
  A manually tuned PID controller (Kp=1, Ki=0.0001, Kd=0.01) manages movement.
  Position and orientation data are logged and plotted.

