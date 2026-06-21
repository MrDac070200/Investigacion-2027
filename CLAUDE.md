# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Spanish-language academic research project titled **"Método de Optimización"** for a 2026 Jornada Científica (Scientific Conference). The research proposes a 5-phase pipeline for compressing and optimizing deep learning models (trained in PyTorch) so they can run on limited hardware such as tablets and portable ultrasound devices, with minimal loss of diagnostic precision.

The domain is medical imaging (dermoscopy / skin lesion classification). Model architectures considered: EfficientNetV2, MobileNetV4, YOLO26.

## Key Documents

- [PPI\PPI 2026 - metodo de optimizacion.docx](PPI/PPI%202026%20-%20metodo%20de%20optimizacion.docx) — Main research paper (Word)
- [PPT Plantilla\Plantilla Jornada Científica (2).pptx](PPT%20Plantilla/Plantilla%20Jornada%20Científica%20(2).pptx) — Presentation template for the conference
- [Metodologia\](Metodologia/) — Five PNG diagrams (FASE 1–5) illustrating the methodology pipeline

## 5-Phase Methodology

**Fase 1 — Baseline Training**
Train an initial model via Transfer Learning with the AdamW optimizer. Establish "ceiling" precision metrics (Accuracy, F1-score, AUC) and "floor" efficiency metrics (inference latency, model size, VRAM usage) tracked in MLflow. Output: `modelo_entrenado.pt`.

**Fase 2 — Pruning / Compression**
Apply neural network reduction techniques (pruning or equivalent strategies) to the trained model. This deliberately sacrifices some metric quality in exchange for a smaller, faster model.

**Fase 3 — Fine-Tuning after Pruning**
Re-train the pruned model to recover lost accuracy. Analyze pruning + fine-tuning metrics, iterate strategies, and select the best-performing configuration. Output: `modelo_fine_tuning.pt`.

**Fase 4 — Quantization**
Convert the optimized model weights from FP32 to INT8 using techniques such as SmoothQuant. Goal: minimize file size and maximize inference speed for deployment on constrained hardware.

**Fase 5 — Evaluation & MLflow Comparison**
Generate a comprehensive MLflow comparison between the baseline model and each optimization iteration (including the final quantized model). Demonstrate the efficiency/accuracy trade-off quantitatively (e.g., 60% latency reduction vs. minimal precision loss).

## Tooling & Technologies

- **PyTorch** — model training and serialization (`.pt` files)
- **MLflow** — experiment tracking across all phases
- **SmoothQuant** — INT8 quantization
- **AdamW** — optimizer for baseline training and fine-tuning
- Transfer Learning from pretrained EfficientNetV2 / MobileNetV4 / YOLO26 backbones
