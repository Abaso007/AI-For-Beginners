<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0d1babfdcbeb46525f2db3fbaaa54cd7",
  "translation_date": "2025-10-03T11:25:55+00:00",
  "source_file": "examples/README.md",
  "language_code": "en"
}
-->
# Beginner-Friendly AI Examples

Welcome! This directory contains simple, standalone examples to help you get started with AI and machine learning. Each example is designed to be beginner-friendly with detailed comments and step-by-step explanations.

## 📚 Examples Overview

| Example | Description | Difficulty | Prerequisites |
|---------|-------------|------------|---------------|
| [Hello AI World](../../../examples/01-hello-ai-world.py) | Your first AI program - simple pattern recognition | ⭐ Beginner | Python basics |
| [Simple Neural Network](../../../examples/02-simple-neural-network.py) | Build a neural network from scratch | ⭐⭐ Beginner+ | Python, basic math |
| [Image Classifier](./03-image-classifier.ipynb) | Classify images with a pre-trained model | ⭐⭐ Beginner+ | Python, numpy |
| [Text Sentiment](../../../examples/04-text-sentiment.py) | Analyze text sentiment (positive/negative) | ⭐⭐ Beginner+ | Python |

## 🚀 Getting Started

### Prerequisites

Make sure you have Python installed (3.8 or higher recommended). Install required packages:

```bash
# For Python scripts
pip install numpy

# For Jupyter notebooks (image classifier)
pip install jupyter numpy pillow tensorflow
```

Or use the conda environment from the main curriculum:

```bash
conda env create --name ai4beg --file ../environment.yml
conda activate ai4beg
```

### Running the Examples

**For Python scripts (.py files):**
```bash
python 01-hello-ai-world.py
```

**For Jupyter notebooks (.ipynb files):**
```bash
jupyter notebook 03-image-classifier.ipynb
```

## 📖 Learning Path

We recommend following the examples in order:

1. **Start with "Hello AI World"** - Learn the basics of pattern recognition
2. **Build a Simple Neural Network** - Understand how neural networks work
3. **Try the Image Classifier** - See AI in action with real images
4. **Analyze Text Sentiment** - Explore natural language processing

## 💡 Tips for Beginners

- **Read the code comments carefully** - They explain what each line does
- **Experiment!** - Try changing values and see what happens
- **Don't worry about understanding everything** - Learning takes time
- **Ask questions** - Use the [Discussion board](https://github.com/microsoft/AI-For-Beginners/discussions)

## 🔗 Next Steps

After completing these examples, explore the full curriculum:
- [Introduction to AI](../lessons/1-Intro/README.md)
- [Neural Networks](../lessons/3-NeuralNetworks/README.md)
- [Computer Vision](../lessons/4-ComputerVision/README.md)
- [Natural Language Processing](../lessons/5-NLP/README.md)

## 🤝 Contributing

Found these examples helpful? Help us improve them:
- Report issues or suggest improvements
- Add more examples for beginners
- Improve documentation and comments

---

*Remember: Every expert was once a beginner. Happy learning! 🎓*

---

**Disclaimer**:  
This document has been translated using the AI translation service [Co-op Translator](https://github.com/Azure/co-op-translator). While we aim for accuracy, please note that automated translations may contain errors or inaccuracies. The original document in its native language should be regarded as the authoritative source. For critical information, professional human translation is recommended. We are not responsible for any misunderstandings or misinterpretations resulting from the use of this translation.