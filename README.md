# ADHD-MultiTask-FlanT5

[![TechRxiv](https://img.shields.io/badge/TechRxiv-XXXX.XXXXX-b31b1b.svg)](https://techrxiv.org/abs/XXXX.XXXXX)
[![HuggingFace](https://img.shields.io/badge/🤗%20HuggingFace-Model-yellow)](https://huggingface.co/lhwang19/ADHD-MultiTask-FlanT5)
[![Demo](https://img.shields.io/badge/🚀%20Live-Demo-blue)](https://adhd-multitask-flant5.streamlit.app/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

A privacy-preserving, low-resource multi-task NLP framework built on **Flan-T5-Base** (248M parameters) to help ADHD users organize scattered thoughts through automated **classification**, **rewriting**, and **summarization**. Designed for on-device deployment with minimal compute requirements.

---

## 🎯 Quick Links

- **📄 Paper**: [TechRxiv](https://techrxiv.org/abs/XXXX.XXXXX) *(Link will be updated after approval)*
- **🤖 Model**: [HuggingFace Hub](https://huggingface.co/lhwang19/ADHD-MultiTask-FlanT5)
- **🚀 Live Demo**: [Streamlit App](https://adhd-multitask-flant5.streamlit.app/)
- **📧 Contact**: layhwangk@gmail.com

---

## ✨ What This Does

This project demonstrates a **complete end-to-end pipeline**: data collection and annotation, model training, post-processing optimization, and interactive demo deployment. It addresses a critical gap in assistive technology for neurodivergent users. Unlike diagnostic-focused NLP tools, this framework provides **functional assistance** to help ADHD individuals:

- **🏷️ Classify** thoughts into intent-based categories (e.g., Self Reflection, Health, Work, Relationships)
- **✍️ Rewrite** disorganized text into clearer, structured sentences while preserving the user's authentic voice
- **📝 Summarize** lengthy posts into concise 1-2 sentence summaries

The demo is hosted on Streamlit Cloud for easy access.

---

## 🚀 Try It Now

**Visit the [live Streamlit demo](https://adhd-multitask-flant5.streamlit.app/)** to test the model interactively. Simply paste your text and see real-time results.

> **Note**: The model on HuggingFace Hub requires additional post-processing logic (calibrated per-label thresholds and exclusivity rules) to achieve the reported performance. The demo includes these components.

---

## 🔬 Technical Highlights

### Architecture
- **Base Model**: Flan-T5-Base (248M parameters)
- **Multi-task Design**: Shared encoder with task-specific heads
  - Classification: Encoder + Linear head (multi-label)
  - Generation: Full encoder-decoder (rewriting & summarization)

### Training Strategy
To overcome catastrophic forgetting and negative transfer in multi-task learning under resource constraints (16GB T4 GPU), this project developed a **staged training pipeline** that sequentially trains tasks while strategically freezing/unfreezing components. This approach achieves optimal balance between classification accuracy and generation quality.

*See the paper for detailed methodology and ablation studies.*

### Key Design Choices
- ✅ **Group-wise data splitting** by Post_ID to prevent leakage across tasks
- ✅ **Taxonomy-driven post-processing** with calibrated per-label thresholds
- ✅ **LLM-driven synthetic data augmentation** (GPT-4o-mini) for low-resource generation tasks
- ✅ **Focal Loss** + stratified oversampling to handle class imbalance

---

## 📚 Citation

If you use this work in your research, please cite:

```bibtex
@article{koay2025adhd,
  title={Organising ADHD Users' Thoughts: A Low-Resource Multi-Task Framework using Flan-T5},
  author={Koay, Lay Hwang},
  journal={TechRxiv preprint techrxiv:XXXX.XXXXX},
  year={2025}
}
```
*techrxiv link will be updated after approval.*

---

## 🎓 For Researchers

### Dataset
- **Source**: r/ADHD subreddit (2008-2024)
- **Size**: 4,000 examples total
  - Classification: 2,000 (manually annotated)
  - Rewriting: 1,286 (synthetic targets)
  - Summarization: 714 (synthetic targets)
- **Taxonomy**: 9 intent-based labels with exclusivity rules
- **Split**: 70/15/15 (train/val/test) with group-wise splitting by Post_ID

### Training Details
- **Hardware**: Single T4 GPU (16GB VRAM)
- **Batch Size**: 4
- **Optimizer**: AdamW
- **Learning Rates**: 6e-6 (encoder), 1.5e-4 (classifier head), 2e-5 (decoder)
- **Loss Functions**: Focal Loss (classification), Cross-Entropy (generation)
- **Early Stopping**: Micro-F1 for classification, validation loss for generation

### Results
| Task | Metric | Score |
|------|--------|-------|
| **Multi-label Classification** | Micro-F1 | **0.5251** |
| | Macro-F1 | 0.4479 |
| | Exact Match | 0.4233 |
| **Rewriting** | BERTScore (F1) | **0.4953** |
| | BLEU | 0.1093 |
| **Summarization** | BERTScore (F1) | **0.4892** |
| | ROUGE-L | 0.3590 |

*Trained on 4,000 examples from r/ADHD (2008-2024) using a novel staged training strategy.*

See the [full paper](https://techrxiv.org/abs/XXXX.XXXXX) for detailed methodology, ablation studies, error analysis, limitations, and future work.

---

## 🛠️ For Developers & Professionals

### Technical Stack
- **Model**: Flan-T5-Base (Google)
- **Framework**: PyTorch, Transformers (HuggingFace)
- **Deployment**: Streamlit Cloud (demo)

---

## ⚠️ Important Notes

- **Model Usage**: The raw model on HuggingFace requires post-processing (calibrated thresholds and exclusivity rules) to achieve reported performance. Use the [demo](https://adhd-multitask-flant5.streamlit.app/) for the complete pipeline.
- **Code & Data**: Training code and dataset are not publicly released due to privacy and platform policies.

---

## 📝 License

This project is licensed under the Apache License 2.0. The model weights are available under the same license. See [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- **Data Source**: r/ADHD community for publicly shared content
- **Infrastructure**: Google Colab, Kaggle, HuggingFace Hub, Streamlit Cloud

---

## 📧 Contact & Links

- **Email**: layhwangk@gmail.com
- **Paper**: [TechRxiv](https://techrxiv.org/abs/XXXX.XXXXX) *(Link will be updated after approval)*
- **Model**: [HuggingFace](https://huggingface.co/lhwang19/ADHD-MultiTask-FlanT5)
- **Demo**: [Streamlit Cloud](https://adhd-multitask-flant5.streamlit.app/)
