# PyTorch Machine Learning Models Created by [Claude Code](https://claude.ai/code)

The README.md file (this file) was also created by [Claude Code](https://claude.ai/code) (tweaked a little by the author of course).

## Model [1]: Food-101 Classification with PyTorch CNN
A deep learning project implementing a ResNet-based Convolutional Neural Network for classifying food images from the Food-101 dataset. This project demonstrates state-of-the-art computer vision techniques using PyTorch.

**🤖 The initial code in the notebook and the README.md file were generated by [Claude Code](https://claude.ai/code) using a simple prompt provided by the author who also checked the code, split it into multiple cells, made a few minor tweaks and tested the code.**

## Overview

This project implements a custom ResNet-inspired CNN architecture to classify images across 101 different food categories using the Food-101 dataset. The model achieves robust performance through modern deep learning techniques including batch normalization, dropout regularization, and adaptive pooling.

## Dataset

- **Dataset**: Food-101 (101 food categories)
- **Training samples**: 60,600 (80% of original training set)
- **Validation samples**: 15,150 (20% of original training set)
- **Test samples**: 25,250
- **Image size**: 224×224 pixels
- **Data augmentation**: Random horizontal flip, rotation, and ImageNet normalization

## Model Architecture

The `ResNetCNN` model is a custom implementation inspired by ResNet architecture with the following key components:

### Architecture Rationale

- **Initial Conv Layer**: 7×7 kernel with stride 2 for efficient feature extraction from 224×224 input images
- **Batch Normalization**: Applied after each convolution for training stability and faster convergence
- **Residual-inspired Blocks**: Four progressive layers (64→128→256→512 channels) with 2 blocks each
- **Adaptive Global Average Pooling**: Reduces spatial dimensions to 1×1 regardless of input size
- **Dropout**: 50% dropout before final classification layer to prevent overfitting
- **Final FC Layer**: Maps 512 features to 101 food categories

### Model Specifications

- **Total parameters**: 4,785,765
- **Architecture depth**: 4 main layers with progressive channel doubling
- **Activation**: ReLU throughout the network
- **Pooling**: MaxPool after initial conv, AdaptiveAvgPool before classifier

## Training Configuration

- **Optimizer**: Adam (lr=0.001, weight_decay=1e-4)
- **Loss function**: CrossEntropyLoss
- **Scheduler**: StepLR (step_size=10, gamma=0.1)
- **Batch size**: 32
- **Epochs**: 20
- **Device**: Apple Silicon MPS GPU (with CUDA/CPU fallback)

## Performance Metrics

The model training includes comprehensive tracking of:

- **Accuracy**: Classification accuracy on training/validation/test sets
- **Precision**: Weighted average precision across all classes
- **Recall**: Weighted average recall across all classes
- **Loss**: CrossEntropy loss monitoring
- **Training speed**: Real-time performance monitoring (samples/second)

### Results Summary

**Final Test Results:**
- **Test Loss**: 1.6568
- **Test Accuracy**: 56.51%
- **Test Precision**: 55.93%
- **Test Recall**: 56.51%
- **Test evaluation time**: 49.95s
- **Test inference speed**: 506.4 samples/s
- **Total training time**: 47.11 minutes

*Note: Complete training results and performance metrics are tracked during the 20-epoch training process with detailed per-epoch reporting.*

## Features

- **Multi-GPU Support**: Automatic detection of Apple Silicon MPS, NVIDIA CUDA, or CPU
- **Comprehensive Metrics**: Real-time tracking of accuracy, precision, recall, and timing
- **Model Persistence**: Automatic saving of best model based on validation loss
- **Data Visualization**: Built-in plotting for training metrics and timing analysis
- **Performance Monitoring**: Detailed timing analysis for training optimization

## File Structure

```
claude_code_pytorch/
├── claude_code_food101_classification.ipynb  # Main training notebook
├── README.md                                 # This file
├── best_model.pth                           # Saved best model weights
├── training_metrics.png                     # Training performance plots
├── timing_analysis.png                      # Training timing analysis
└── data/                                    # Food-101 dataset (auto-downloaded)
```

## Usage

1. **Environment Setup**: Ensure PyTorch, torchvision, matplotlib, scikit-learn, and numpy are installed
2. **Run Training**: Execute the Jupyter notebook `claude_code_food101_classification.ipynb`
3. **Dataset Download**: Food-101 dataset will be automatically downloaded on first run
4. **Model Training**: 20-epoch training with automatic best model saving
5. **Results**: View training metrics plots and final test evaluation

**The code has been tested on both MacBook Pro /w Apple M4 and Ubuntu 24.04 /w Nvidia GPU**

## Technical Highlights

- **Efficient Data Loading**: Multi-worker DataLoader with optimized batch processing
- **Memory Optimization**: Gradient accumulation and efficient tensor operations
- **Real-time Monitoring**: Batch-level progress tracking with ETA estimation
- **Robust Validation**: Separate validation pipeline with comprehensive metrics
- **Reproducible Results**: Systematic experiment tracking and model persistence

## Requirements

- Python 3.7+ (the Python version used by the author to test the code was **3.11.13**)
- PyTorch 1.9+ (the PyTorch version used by the author to test the code was **2.7.1**)
- torchvision
- matplotlib
- scikit-learn
- numpy

---

*This implementation demonstrates modern deep learning best practices for image classification tasks, combining architectural innovations with robust training methodology.*

## Model [2]: BERT Text Classifier for IMDb Movie Reviews

A comprehensive implementation of a BERT-based text classifier for sentiment analysis using PyTorch and the Transformers library. This project demonstrates state-of-the-art natural language processing techniques for binary sentiment classification.

**🤖 The initial code in the notebook was generated by [Claude Code](https://claude.ai/code) using a simple prompt provided by the author who also checked the code, made minor tweaks and tested the code**

## Overview

The bert_imdb_classifier.ipynb notebook implements a fine-tuned BERT model for sentiment analysis on movie reviews from the IMDb dataset. The model achieves excellent performance through transfer learning, leveraging the pre-trained `bert-base-uncased` model with a custom classification head.

## Dataset

- **Dataset**: IMDb Movie Reviews (50,000 total samples)
- **Training samples**: 35,000 (70% of dataset)
- **Validation samples**: 7,500 (15% of dataset)  
- **Test samples**: 7,500 (15% of dataset)
- **Classes**: Binary (Positive/Negative sentiment)
- **Text preprocessing**: BERT tokenization with 512 max sequence length

## Model Architecture

The `BERTTextClassifier` model combines pre-trained BERT with a custom classification head:

### Architecture Components

- **Base Model**: Pre-trained BERT (`bert-base-uncased`) for contextual embeddings
- **Pooling**: Uses [CLS] token representation from BERT's pooler output
- **Dropout**: 30% dropout for regularization
- **Classification Head**: Linear layer mapping 768 BERT features to 2 classes

### Model Specifications

- **Total parameters**: 109,483,778
- **Trainable parameters**: All parameters fine-tuned
- **Input length**: 512 tokens maximum
- **Tokenizer**: BERT WordPiece tokenization

## Training Configuration

- **Optimizer**: AdamW (lr=2e-5, weight_decay=default)
- **Loss function**: CrossEntropyLoss
- **Scheduler**: Linear warmup with decay
- **Batch size**: 16
- **Epochs**: 4
- **Device**: NVIDIA CUDA GPU (with CPU fallback)

## Performance Metrics

The model training includes comprehensive tracking of:

- **Accuracy**: Classification accuracy on training/validation/test sets
- **Precision**: Weighted average precision across both classes
- **Recall**: Weighted average recall across both classes
- **F1-Score**: Weighted F1-score for balanced evaluation
- **Loss**: CrossEntropy loss monitoring with gradient clipping

### Results Summary

**Final Test Results:**
- **Test Loss**: 0.2101
- **Test Accuracy**: 93.95%
- **Test Precision**: 93.95%
- **Test Recall**: 93.95%
- **Test F1-Score**: 93.95%
- **Best Validation Accuracy**: 94.79%
- **Total training time**: 139.53 minutes (~2.3 hours)

*Note: Complete training results with per-epoch metrics are included in the notebook with full outputs.*

## Features

- **Pre-trained BERT**: Leverages powerful language understanding from BERT-base
- **Comprehensive Metrics**: Real-time tracking of accuracy, precision, recall, and F1-score
- **Model Persistence**: Automatic saving of best model based on validation accuracy
- **Training Visualization**: Built-in plotting for loss, accuracy, learning rate, and timing
- **Example Predictions**: Interactive sentiment prediction with confidence scores
- **Confusion Matrix**: Detailed performance analysis visualization

## File Structure

```
claude_code_pytorch/
├── bert_imdb_classifier.ipynb           # Main training notebook
├── README.md                            # This file
├── best_bert_model.pth                  # Saved BERT model weights
├── bert_training_metrics.png            # BERT training performance plots
├── bert_confusion_matrix.png            # BERT model performance heatmap
└── imdb_data.csv                        # Cached IMDb dataset
```

## Usage

1. **Environment Setup**: Ensure required packages are installed (see Requirements)
2. **Run Training**: Execute the Jupyter notebook `bert_imdb_classifier.ipynb`
3. **Dataset Download**: IMDb dataset will be automatically downloaded on first run
4. **Model Training**: 4-epoch fine-tuning with automatic best model saving
5. **Results**: View training metrics plots and final test evaluation

**The code has been tested and includes complete cell outputs demonstrating successful execution.**

## Technical Highlights

- **Transfer Learning**: Fine-tuning pre-trained BERT for domain-specific sentiment analysis
- **Efficient Tokenization**: BERT WordPiece tokenization with attention masks
- **Gradient Clipping**: Prevents exploding gradients during fine-tuning
- **Learning Rate Scheduling**: Linear warmup and decay for optimal convergence
- **Robust Evaluation**: Separate validation pipeline with detailed classification metrics

## Requirements

- Python 3.7+ (the Python version used for the full run was **3.11.13**)
- torch - PyTorch deep learning framework (the PyTorch version used for the full run was **2.7.1**)
- torchvision - Computer vision utilities for PyTorch  
- transformers - Hugging Face transformers library for BERT
- datasets - Hugging Face datasets library for IMDb data loading
- scikit-learn - Machine learning metrics and evaluation tools
- matplotlib - Plotting and visualization
- seaborn - Statistical data visualization
- pandas - Data manipulation and analysis
- numpy - Numerical computing

---

*This implementation demonstrates modern NLP best practices for text classification tasks, combining pre-trained language models with robust fine-tuning methodology.*