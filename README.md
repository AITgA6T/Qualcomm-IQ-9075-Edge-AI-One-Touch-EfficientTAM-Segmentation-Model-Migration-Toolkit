# Qualcomm IQ-9075 Edge AI One-Touch EfficientTAM Segmentation Model Migration Toolkit

## Advantages of IQ-9075

1. IQ-9075 can provide up to 200 sparse TOPS of AI computing power and supports GPU and DSP accelerated computing
2. The Qualcomm Neural Processing (SNPE) SDK and the Qualcomm AI Engine Direct (QNN) can optimize the performance of trained neural networks
3. It supports Yocto and Ubuntu for AI development

## Performance Metrics

- **AI Model**: EfficientTAM-Ti (512 × 512) — Video Object Segmentation and Tracking from a single click (QNN, 4 components: image encoder, memory attention, mask decoder, memory encoder)

| Model | Precision | J&F | IoU vs. FP32 | Latency on IQ-9075 (HTP, per frame) |
|---|---|---|---|---|
| Reference | FP32 | 0.9391 | — | — |
| QNN | FP16 | 0.9386 | 0.998 | ~48 ms |

Evaluated on the DAVIS "blackswan" sequence (50 frames) with the DAVIS J&F metric. Latency is the graph time per frame on the HTP backend.

## Hardware

- **Platform**:  [Qualcomm IQ-9075 EVK](https://www.qualcomm.com/developer/hardware/qualcomm-iq-9075-evaluation-kit-evk)
- **Host PC**: Ubuntu x86_64 PC with NVIDIA RTX 30/40 series GPU, connected to the EVK over USB (ADB)

## Software & Toolkit

- **Qualcomm AI Runtime (QAIRT) SDK**：v2.44.0 (conversion) / v2.47.0 (on-device runtime)
- **System:** Yocto (Qualcomm Linux)
- **Host OS:** Ubuntu 22.04

## Background & Solution

### Motivation

- Creating a One-Touch Toolkit to show Qualcomm Edge AI strength on real-time video object tracking with memory-based models

### Solution

- One-touch PyTorch-to-QNN conversion of all four EfficientTAM components with a fixed precision recipe, deployed to the IQ-9075 NPU together
- Click an object on the first frame and track it through the video on the IQ-9075 EVK
- On-device QNN benchmark on IQ-9075 EVK: per-frame latency, J / F / J&F and agreement with the FP32 reference

## Architecture Diagram

The architecture diagram shows the toolkit workflow, corresponding to the colors in the legend on the left

Blue Phase: Convert the PyTorch model into a QNN model, and evaluate the benchmark for the QNN model

Purple Phase: Perform real-time inference and display the results based on the converted QNN model

<img width="1843" height="742" alt="architecture" src="assets/architecture.png" />

## Demo

Live video object tracking with the FP16 QNN model on IQ-9075 EVK

<img width="900" alt="inference" src="assets/demo-inference.jpeg" />

One-touch EfficientTAM conversion with a fixed per-component precision recipe

<img width="900" alt="conversion" src="assets/demo-conversion.jpeg" />

## Contact
If you require any further information, please feel free to contact:

TW: qualcomm.tw@aitgroup.com.tw

CN: qualcomm.cn@aitgroup.com.tw
