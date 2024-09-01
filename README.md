### Project Title: Wide & Deep Learning-Based Recommendation System

#### Overview

This project implements a Wide & Deep Learning-based recommendation system, following the framework proposed by Heng-Tze Cheng et al. in their paper "Wide & Deep Learning for Recommender Systems." The objective is to leverage the strengths of both memorization and generalization to improve the performance of recommendation systems, especially when dealing with sparse and high-dimensional data. 

#### Theoretical Background

**Wide & Deep Learning Framework**:
The Wide & Deep Learning model is designed to combine the benefits of both linear models (which excel at memorizing frequent feature interactions) and deep neural networks (which generalize well to unseen feature combinations). 

- **Wide Component**: A generalized linear model (GLM) that captures feature interactions using cross-product transformations. This component is effective at memorizing relationships between features that are seen frequently during training.
  
- **Deep Component**: A deep neural network that learns low-dimensional dense embeddings for high-dimensional sparse features. This component is capable of generalizing to new feature interactions that were not explicitly seen during training.

- **Joint Training**: Both components are trained simultaneously, with their outputs combined using a weighted sum of the log odds, which is then passed to a common logistic loss function. This allows the model to optimize both memorization (through the Wide component) and generalization (through the Deep component).

**Pytorch-Widedeep Library**:
The implementation leverages the `pytorch-widedeep` library, which is designed for building multimodal deep learning models that can handle various data types, including tabular data, text, and images. The library is particularly well-suited for building wide and deep models.

Key features of the library include:
- **Modular Design**: Separate model components for different data types (e.g., `deeptabular`, `deeptext`, `deepimage`).
- **Deeptabular Models**: Three models for tabular data: `TabMLP`, `TabResNet`, and `TabTransformer`.
- **Support for Text and Image Data**: Integration of text and image data through `deeptext` and `deepimage` components.

#### Dataset

The dataset used in this project includes the following columns:
- **Categorical Features**: `Book-Title`, `Book-Author`, `Publisher`, `Year-Of-Publication`, `City`, `Country`.
- **Continuous Feature**: `Age`.
- **Target Feature**: `Book-Rating`.

**Feature Engineering**:
- **Wide Columns**: `Book-Title`, `Book-Author`, `Publisher`, `Year-Of-Publication`, `City`, `Age`.
- **Crossed Columns**: `("Book-Title", "Book-Author")`, `("City", "Book-Author")`.
- **Embedded Columns**: `Publisher`, `Book-Title`, `Book-Rating`, `Book-Author`, `Year-Of-Publication`, `City`, `Country`.

#### Model Architecture

The architecture chosen for this implementation is the `TabMLP` model, which is part of the `deeptabular` component in the `pytorch-widedeep` library. The model consists of:
1. **Embeddings** for categorical features, which are then concatenated with the continuous features.
2. **Multi-Layer Perceptron (MLP)** to process the combined feature vector.
3. **Output Layer** for predicting the target feature, `Book-Rating`.

#### Implementation Steps

1. **Data Preprocessing**:
   - Categorical features are converted into embeddings.
   - Continuous features are normalized.
   - Crossed features are created by combining specific categorical features.

2. **Model Setup**:
   - The wide component is configured with the wide columns and crossed columns.
   - The deep component is configured with the embedded categorical features and continuous features.
   - The model is initialized using the `TabMLP` architecture from the `pytorch-widedeep` library.

3. **Training**:
   - The model is trained using a standard backpropagation algorithm, with the logistic loss function optimized for both the wide and deep components.

4. **Evaluation**:
   - The model's performance is evaluated using metrics like accuracy, precision, recall, and F1-score.
   - The results are compared against baseline models to demonstrate the effectiveness of the Wide & Deep Learning approach.

#### Results

The model significantly improves the recommendation accuracy by effectively balancing memorization and generalization. This results in better predictions, especially for less frequent user-item interactions.

#### Conclusion

This project successfully implements a Wide & Deep Learning-based recommendation system, demonstrating the practical benefits of combining wide linear models with deep neural networks. The use of the `pytorch-widedeep` library facilitates the creation of a modular and extensible model, which can be adapted to various types of recommendation tasks.

#### Future Work

Future enhancements could include:
- Integrating additional data types (e.g., text and images) using the `deeptext` and `deepimage` components.
- Experimenting with different architectures such as `TabResNet` and `TabTransformer` for the deep component.
- Deploying the model in a production environment and testing its performance on live data.

---

**Author**: Anbu Valluvan  
**License**: MIT License  
**Date**: April 2024

---
