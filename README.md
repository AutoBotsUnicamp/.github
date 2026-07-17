# 🤖 Autobot: 2D Autonomous Navigation with ESP32 and ROS 2

Welcome to the central repository for **Autobot**, an autonomous mobile track robot featuring a decoupled, hybrid architecture.

This project was developed as the final capstone project for the Computer Engineering degree at UNICAMP (School of Electrical and Computer Engineering - FEEC), under the title: *"Navegação Autônoma 2D com ESP32: Projeto e Implementação em um Robô Móvel"*.

🎥 **[Watch the robot in action on YouTube!](https://youtu.be/cynhL9kDgR4)**

## 👥 The Team
* Thiago Maximo Pavão
* Vinícius Carvalho Pimpim
* Vinícius Esperança Mantovani

---

## 🏗️ System Overview

Autobot utilizes a hybrid architecture that successfully decouples the robot's hardware from the host computer. By utilizing an ESP32 microcontroller as a real-time Wi-Fi bridge, the robot operates untethered while offloading computationally heavy tasks (like SLAM and path planning) to a remote host machine.

Through a comparative analysis of SLAM algorithms, this project demonstrated that fusing encoder and IMU data via an Extended Kalman Filter (EKF) effectively corrects rotational drift, resulting in a highly robust map for autonomous navigation.

### Hardware Components
* **Microcontroller:** ESP32
* **LiDAR:** YDLiDAR X3
* **IMU:** MPU-6050
* **Actuation:** Tracked chassis with DC motors and wheel encoders

---

## 📂 Repository Structure

The system is divided into two primary sub-projects. Please visit their respective repositories for detailed installation and usage instructions:

### 1. 🧠 [autobot_controller](https://github.com/AutoBotsUnicamp/autobot_controller) (ESP32 Firmware)
The low-level embedded firmware, developed over the ESP-IDF framework using FreeRTOS.
* **Hardware Control:** Manages real-time motor control and sensor telemetry.
* **Network Bridge:** Hosts TCP/UDP servers to stream LiDAR data, IMU readings, and odometry over Wi-Fi, while receiving velocity commands.

### 2. 🗺️ [autobot_ws](https://github.com/AutoBotsUnicamp/autobot_ws) (ROS 2 Workspace)
The high-level processing stack, designed for ROS 2 Jazzy on Ubuntu 24.04.
* **Sensor Fusion:** Uses `robot_localization` (EKF) to fuse encoder odometry and IMU data.
* **Mapping:** Utilizes `slam_toolbox` to generate 2D maps of the environment.
* **Navigation:** Leverages the `Nav2` stack for autonomous trajectory planning and execution.

---

## 🚀 Getting Started

If you are setting up the project from scratch:
1. Clone the firmware repository and flash your ESP32.
2. Clone the ROS 2 workspace onto your host machine, install the dependencies, and build using `colcon`.
3. Connect your host machine to the same network as the ESP32 and launch the base drivers to begin mapping or navigating!
