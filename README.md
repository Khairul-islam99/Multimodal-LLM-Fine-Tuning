# 🤖 Bini-Math: Multimodal LLM Fine-Tuning

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Unsloth](https://img.shields.io/badge/Unsloth-Fast_Fine--Tuning-orange)
![HuggingFace](https://img.shields.io/badge/Hugging%20Face-Transformers-yellow)
![License](https://img.shields.io/badge/License-MIT-green)

**Bini-Math** is a project focused on fine-tuning a Vision-Language Model (Qwen-VL based) on the **GSM8K** dataset to enhance its mathematical reasoning and multimodal capabilities. The project utilizes **Unsloth** for efficient, memory-saving fine-tuning and includes a **Gradio** web interface for interactive inference.

---

## 🚀 Overview

This repository contains a complete pipeline for:
1.  **Data Preprocessing:** Converting the GSM8K math dataset into a conversational format usable by VLMs.
2.  **Efficient Fine-Tuning:** Using LoRA (Low-Rank Adaptation) and Unsloth to fine-tune the `BINI-Qwen3-VL` model on a T4 GPU (Google Colab).
3.  **Inference:** A user-friendly web UI to chat with the model about text and images.

## 🛠️ Tech Stack

* **Model:** `khairul5/BINI-Qwen3-VL-MyMirror` (Qwen-VL Architecture)
* **Fine-Tuning:** [Unsloth](https://github.com/unslothai/unsloth) (2x faster, 70% less memory)
* **Dataset:** [GSM8K](https://huggingface.co/datasets/gsm8k) (Grade School Math)
* **Training Library:** Hugging Face `trl` (SFTTrainer) & `peft`
* **Interface:** Gradio

## 📂 Data Preparation

The project loads the `gsm8k` dataset and converts it into a chat format compatible with Qwen-VL.

**Format Structure:**
```json
{
  "messages": [
    { "role": "user", "content": [{ "type": "text", "text": "Question..." }] },
    { "role": "assistant", "content": [{ "type": "text", "text": "Answer..." }] }
  ]
}
```
## 🧠 Training Configuration

The model is fine-tuned using **LoRA** with the following hyperparameters:

| Parameter | Value |
| :--- | :--- |
| **LoRA Rank (r)** | 16 |
| **LoRA Alpha** | 16 |
| **Batch Size** | 2 (per device) |
| **Gradient Accumulation** | 4 |
| **Learning Rate** | 2e-4 |
| **Optimizer** | AdamW 8-bit |
| **Quantization** | 4-bit |

## 📊 Performance

During training on the dataset (~7.5k examples), the model demonstrated significant convergence:

* **Starting Loss:** ~0.32
* **Final Training Loss:** ~0.08
* **Evaluation Loss:** ~0.89

## 🏃 Usage

### 1. Run the Notebook
Execute the `Multimodal LLM Fine-Tuning` notebook. It handles the entire lifecycle from data loading to saving the adapters.

### 2. Launch the Web UI
The project includes a **Gradio** interface to chat with the model.

```python
# Code snippet to launch UI
demo.launch(share=True)
```
📜 License
This project is open-source and available under the MIT License.
