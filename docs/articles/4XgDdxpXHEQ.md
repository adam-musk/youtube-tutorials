---
layout: "../../layouts/BlogPost.astro"
title: "Vision Transformers: Embedding Images with Self-Attention"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "4XgDdxpXHEQ"
channel: ""
index: 21
---

# Vision Transformers: Embedding Images with Self-Attention

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/4XgDdxpXHEQ" frameborder="0" allowfullscreen></iframe>


## Introduction to Vision Transformers

Vision Transformers (ViTs) represent a significant advancement in the field of computer vision. Inspired by the success of Transformers in Natural Language Processing (NLP), ViTs adapt the self-attention mechanism to process images directly. This chapter will guide you through the fundamental concepts of Vision Transformers, exploring their architecture, functionality, and advantages, particularly in comparison to earlier models. We will delve into the practical aspects by conceptually building a Vision Transformer from scratch, mirroring the approach taken in the transcript this chapter is based upon.

Vision Transformers enable the transformation of images into rich, informative embeddings.

> **Embedding:** In machine learning, an embedding is a lower-dimensional vector representation of an object, such as an image or word, that captures its essential features and relationships to other objects.

These embeddings are crucial because they allow vision models to be seamlessly integrated with language models, creating powerful multimodal systems known as Vision Language Models (VLMs). VLMs empower language models to "see" and interpret visual information, enabling them to answer questions about images, generate image descriptions, and perform more complex vision-language tasks.

## How Vision Transformers Work: An Overview

Traditional Transformer models, primarily used in NLP, process sequential data like text by breaking it down into tokens (words or sub-word units). Vision Transformers adapt this approach by treating images as a sequence of patches.

> **Token:** In the context of Transformers, a token is the basic unit of input that the model processes. In NLP, tokens are typically words or sub-word units. In Vision Transformers, tokens are image patches.

Here’s a simplified breakdown of how Vision Transformers process visual data:

*   **Image Patching:**  An input image is divided into smaller, non-overlapping patches. Imagine a puzzle where each piece is an image patch. Each patch is considered analogous to a token in NLP.
*   **Patch Embedding:** Each image patch is then linearly transformed into an embedding vector. This embedding captures the visual information contained within the patch.
*   **Position Embeddings:** To retain spatial information, position embeddings are added to the patch embeddings. This step informs the model about the location of each patch within the original image, as Transformers, by nature, are permutation invariant and do not inherently understand order.

    > **Position Embedding:** A vector added to the input embeddings in Transformer models to provide information about the position of each token in the sequence. This is essential because the self-attention mechanism is order-agnostic.
*   **Self-Attention Mechanism:** The core of the Vision Transformer is the self-attention mechanism. This allows each image patch embedding to interact with and attend to all other patch embeddings in the image. Through self-attention, the model learns the relationships between different parts of the image, making each patch "context-aware."
*   **CLS Token:**  A special classification token, often referred to as `[CLS]` token (though not explicitly mentioned in the transcript as such in ViTs, the concept is analogous), is prepended to the sequence of patch embeddings. This token is designed to aggregate information from all patches through self-attention layers. It acts as a global representation of the entire image.
*   **Transformer Encoder Layers:** The sequence of patch embeddings (including position embeddings and the CLS token) is then passed through multiple layers of a Transformer encoder. Each encoder layer typically consists of:
    *   **Multi-Head Self-Attention:** Multiple parallel self-attention mechanisms operating in parallel to capture diverse relationships.
    *   **Feed-Forward Network (Multi-Layer Perceptron - MLP):** Processes the output of the self-attention layer.
*   **Output Representation:** After passing through the encoder layers, the CLS token's output embedding is often used as the final, high-level representation of the entire image. This embedding can then be used for various downstream tasks such as image classification, object detection, or as input to a Vision Language Model.

## CLIP: Contrastive Language–Image Pre-training

To understand the nuances of more advanced Vision Transformers like SIGL, it's beneficial to first grasp the fundamentals of CLIP (Contrastive Language–Image Pre-training), a foundational model developed by OpenAI. CLIP is designed to learn joint representations of images and text, enabling it to understand the semantic relationship between visual and textual content.

### Image and Text Encoders

CLIP employs two separate encoders:

*   **Image Encoder:** Typically a Vision Transformer or a Convolutional Neural Network (CNN), the image encoder processes input images and transforms them into image embeddings.
*   **Text Encoder:** A Transformer-based text encoder processes input text descriptions and converts them into text embeddings.

### Image and Text Embeddings and Contrastive Learning

CLIP is trained using a contrastive learning approach. It is provided with batches of images and corresponding text descriptions.

1.  **Embedding Generation:** For each image in the batch, the image encoder generates an image embedding. Similarly, for each text description, the text encoder generates a text embedding.
2.  **Dot Product Calculation:** The dot product between all pairs of image embeddings and text embeddings within the batch is computed. This results in a similarity matrix where each cell (i, j) represents the similarity score between the i-th image embedding and the j-th text embedding.

    > **Dot Product:**  In linear algebra, the dot product of two vectors is a scalar value that represents the cosine similarity between the vectors when they are normalized. In this context, a higher dot product indicates greater similarity between embeddings.
3.  **Contrastive Loss (Cross-entropy with Softmax):**  CLIP is trained to maximize the dot product between embeddings of correctly paired images and text descriptions, while minimizing the dot product between embeddings of non-corresponding pairs.  The loss function used is typically cross-entropy loss applied in conjunction with the softmax function.

    > **Cross-entropy Loss:** A common loss function used in classification and contrastive learning tasks. It measures the difference between the predicted probability distribution and the true probability distribution. In CLIP, it encourages high similarity for correct pairs and low similarity for incorrect pairs.

    > **Softmax Function:** A function that converts a vector of raw scores into a probability distribution. In CLIP, it's used to normalize the similarity scores and create probabilities for each image-text pair within the batch.

Specifically, for each image, CLIP aims to assign a high probability to its corresponding text description and low probabilities to all other text descriptions in the batch. The same process is applied in reverse for each text description, aiming for a high probability for its corresponding image and low probabilities for others.

### Limitations of Softmax Loss in CLIP

While effective, the softmax loss function used in the original CLIP model has a computational bottleneck.  It forces the model to compare every image with *all* text descriptions in the batch to calculate the loss and update gradients. This process is computationally expensive and not easily parallelizable.

*   **Batch Dependency:** Softmax loss is inherently batch-dependent. The probability distribution is calculated relative to all items within the current batch.
*   **Computational Cost:**  Calculating softmax across the entire batch for each image and text pair becomes increasingly expensive as the batch size grows.
*   **Limited Parallelization:** The batch-wise nature of softmax makes it challenging to parallelize the training process efficiently across multiple devices.

## SIGL: Sigmoid Loss for Language Image pre-training

SIGL (Sigmoid Loss for Language Image pre-training) addresses the limitations of CLIP’s softmax loss by introducing a more efficient and flexible loss function: sigmoid loss. SIGL, developed by Google, is presented as an improvement over CLIP, particularly in terms of training efficiency and scalability.

### Motivation for SIGL: Efficiency and Flexibility

The primary motivation behind SIGL is to overcome the computational inefficiencies and inflexibility associated with softmax loss in CLIP. SIGL aims to achieve:

*   **Improved Training Efficiency:** By eliminating the need for batch-wise comparisons, SIGL significantly reduces the computational cost of training, especially with large batch sizes.
*   **Enhanced Parallelizability:** SIGL’s formulation allows for easier parallelization of training across multiple GPUs or TPUs, leading to faster training times.
*   **Increased Flexibility:** SIGL is more flexible in handling diverse datasets and training scenarios as it is less constrained by batch composition.

### Sigmoid Loss vs. Softmax Loss

The key difference lies in how the loss is calculated:

*   **Softmax Loss (CLIP):**  Forces the model to compare each image with all other text descriptions in the batch to determine the correct pairing. The loss is calculated based on the probability distribution across all pairs in the batch.
*   **Sigmoid Loss (SIGL):**  Treats each image-text pair independently. For each pair, it predicts a score (ideally close to 1 for correct pairs and 0 for incorrect pairs) and calculates the loss based on this individual prediction using a sigmoid function and binary cross-entropy loss.

    > **Sigmoid Loss:** In the context of SIGL, sigmoid loss refers to the use of a sigmoid activation function followed by a binary cross-entropy loss. The sigmoid function squashes the output to a range between 0 and 1, making it suitable for binary classification tasks (correct pair vs. incorrect pair).

### Advantages of SIGL: Parallelization and Efficiency

By adopting sigmoid loss, SIGL gains several advantages:

*   **Pair-wise Independence:** SIGL processes each image-text pair independently, removing the batch dependency of softmax.
*   **Enhanced Parallelization:** This pair-wise independence allows for straightforward parallelization. Different image-text pairs (or matrices of pairs) can be processed and their losses calculated independently on different devices.
*   **Computational Efficiency:** SIGL avoids the all-pairs comparison required by softmax, leading to significant computational savings, especially with large batches.
*   **Scalability:** SIGL's efficiency and parallelizability make it more scalable for training on massive datasets and with large models.

SIGL is notably used in Google's VLMs like PaLI-X and PaLM-E as the vision encoder, showcasing its practical effectiveness in real-world applications.

## Coding a SIGL Vision Transformer from Scratch: Conceptual Explanation

The transcript provides a conceptual walkthrough of building a SIGL Vision Transformer from scratch using Python and the Hugging Face Transformers library. While the transcript doesn't present fully executable code within the video itself, it meticulously explains each step, from setting up the environment to validating the implementation against pre-trained Hugging Face models. The following section summarizes the key coding steps and concepts explained in the transcript.

### Setting up the Environment and Loading Resources

The process begins by importing necessary libraries from the Hugging Face `transformers` library:

*   `AutoProcessor`: For preprocessing input images to the model's expected format.
*   `SigVisionModel`: Holds the pre-trained weights of the SIGL Vision Transformer model.
*   `SigVisionConfig`:  Defines the architecture and configuration parameters of the SIGL Vision Transformer.

The code then loads a pre-trained SIGL model and its processor from a Hugging Face checkpoint: `"google/siglip-base-patch16-224"`. This checkpoint specifies a SIGL base model with a patch size of 16 and trained on 224x224 images.

### Exploring Model Architecture

The transcript highlights exploring the structure of the loaded pre-trained model. It points out key components like:

*   `SigVisionEmbeddings`:  The embedding layer responsible for patch and position embeddings.
*   `SigVisionEncoder`: The Transformer encoder consisting of multiple layers.
*   Layers within the encoder: Layer Normalization (`LayerNorm`), Multi-Head Attention (`ScaleDotProductAttention`, `MultiAttention`), and Multi-Layer Perceptron (`MLP`).

This exploration provides a roadmap for building the model from scratch, mirroring the architecture of the pre-trained model.

### Image Preprocessing

Before feeding images into the model, they need to be preprocessed. The `AutoProcessor` is used to:

*   **Resize Images:**  Resizes input images to 224x224 pixels, as specified by the model configuration.
*   **Convert to Tensor:** Transforms images into PyTorch tensors, the numerical data structure used by PyTorch models.
*   **Normalize Pixels:** Normalizes pixel values using mean and standard deviation values derived from the ImageNet dataset. This normalization is a common practice in computer vision to improve model performance and training stability.

    > **Tensor:**  A multi-dimensional array, similar to a NumPy array, but optimized for numerical computation, especially on GPUs. Tensors are the fundamental data structure used in deep learning frameworks like PyTorch.

The preprocessed image is then "unsqueeze" to add a batch dimension, even when processing a single image. Transformers expect input in batches.

    > **Batch Dimension:** The first dimension of a tensor that represents a collection of independent input samples processed together. Even when processing a single image, a batch dimension of size 1 is typically added.

### Patch Embeddings

The transcript explains how patch embeddings are created using a convolutional layer (`nn.Conv2d`).

*   **Convolutional Layer for Patching:** A 2D convolutional layer with a kernel size and stride equal to the patch size (16x16 in this case) is used to divide the input image into non-overlapping patches.

    > **Convolutional 2D (Conv2d):** A type of neural network layer that performs convolution operations on 2D input data, such as images. In ViTs, it's used initially to divide the image into patches.

    > **Kernel Size:** The size of the convolutional filter that slides across the input image. In patch embedding, the kernel size is equal to the desired patch size.

    > **Stride:** The step size at which the convolutional filter moves across the input image. In patch embedding with non-overlapping patches, the stride is also equal to the patch size.

*   **Linear Projection:** The convolutional layer also performs a linear projection, transforming each patch into an embedding vector of the desired embedding dimension (768 in this example).

### Position Embeddings

Position embeddings are crucial for Vision Transformers to understand the spatial arrangement of patches. The transcript describes:

*   **Creating Position IDs:**  A sequence of numbers from 0 to the number of patches minus 1 (196 in this case for a 224x224 image with 16x16 patches) is created to represent the position of each patch.
*   **Position Embedding Layer:** An embedding layer (`nn.Embedding`) is used to map each position ID to a position embedding vector.
*   **Adding Position Embeddings:** The position embeddings are added element-wise to the patch embeddings.  Before addition, the patch embeddings are flattened and transposed to ensure compatible dimensions.

### Combining Patch and Position Embeddings

The combination of patch and position embeddings forms the input to the Transformer encoder layers.  The resulting embeddings now contain both visual information from the patches and spatial information about their location in the image.

### Visualizing Embeddings

The transcript demonstrates visualizing the patch embeddings to illustrate the difference between untrained (randomly initialized) embeddings and trained embeddings (from the Hugging Face checkpoint). Trained embeddings exhibit smoother, more structured patterns, indicating that they have learned meaningful representations from the training data.

### Structuring Code into Classes

To organize the code, the transcript demonstrates encapsulating the embedding process within classes:

*   `SigVisionConfig`: A data class to store configuration parameters like embedding dimension, patch size, and image size.
*   `SigVisionEmbeddings`: A class inheriting from `nn.Module` that implements the patch embedding and position embedding layers, and the forward pass to combine them.

### Multi-Head Attention

The core of the Transformer encoder is the multi-head attention mechanism. The transcript explains two implementations:

*   **Single-Head Attention (Conceptual):**  Explains the fundamental concepts of attention:
    *   **Key, Query, Value Projections:** Linear transformations (`nn.Linear`) are used to project input embeddings into key, query, and value vectors.

        > **Key, Query, Value:**  The three core components of the attention mechanism in Transformers. Keys and queries are used to calculate attention weights, while values are aggregated based on these weights.
    *   **Attention Score Calculation:**  Dot product between queries and keys (transpose of keys) is computed to determine the attention scores, representing the affinity between patches.
    *   **Scaling and Softmax:** Attention scores are scaled down (divided by the square root of the head size) and then passed through a softmax function to create attention weights (probabilities).
    *   **Value Aggregation:** Attention weights are multiplied with value vectors, and the results are summed to produce the output of the attention head.

*   **Vectorized Multi-Head Attention (Hugging Face Style):**  Implements multi-head attention in a more efficient, vectorized manner, aligning with the Hugging Face implementation:
    *   **Combined Key, Query, Value Projections:**  Instead of separate projections for each head, single projection layers are used for keys, queries, and values.
    *   **Reshaping for Heads:** The output of these projections is reshaped to split the embedding dimension into multiple heads, processing all heads in parallel.
    *   **Parallel Attention Calculation:** Attention scores, softmax, and value aggregation are performed in parallel across all heads.
    *   **Concatenation and Output Projection:**  The outputs from all heads are concatenated back together, and a final linear projection is applied to match the output dimension to the input dimension.
    *   **Dropout:** Dropout regularization is applied after the attention weights calculation to prevent overfitting.

    > **Dropout:** A regularization technique used in neural networks where randomly selected neurons are ignored during training. This helps prevent overfitting and improves generalization.

### MLP Layer

The Multi-Layer Perceptron (MLP) layer, also known as the feed-forward network, is another crucial component of the Transformer encoder.  The transcript describes a typical MLP implementation:

*   **Two Linear Layers:**  Consists of two fully connected linear layers (`nn.Linear`).
*   **Intermediate Dimension:** The first linear layer projects the input embedding dimension (hidden size) to a higher intermediate dimension.
*   **Non-linearity (GELU):** A non-linear activation function, specifically GELU (Gaussian Error Linear Unit), is applied after the first linear layer.

    > **GELU (Gaussian Error Linear Unit):** A non-linear activation function often used in Transformers and other deep learning models. It is known for its good performance in various tasks.
*   **Projection Back to Hidden Size:** The second linear layer projects the intermediate dimension back to the original hidden size, ensuring the output dimension matches the input dimension.

### Encoder Layer

The encoder layer combines the multi-head attention and MLP layers with layer normalization and residual connections:

*   **Layer Normalization:** Layer normalization (`nn.LayerNorm`) is applied before both the multi-head attention and MLP layers.

    > **Layer Normalization:** A normalization technique that normalizes the activations within each layer of a neural network. It helps stabilize training and often improves performance.
*   **Residual Connections:** Residual connections (skip connections) are used to add the original input embeddings to the output of both the multi-head attention and MLP layers. This helps with gradient flow and allows for training deeper networks.

    > **Residual Connection (Skip Connection):** A connection that bypasses one or more layers in a neural network, adding the input of the bypassed layers to their output. Residual connections are crucial for training deep networks effectively.

### Vision Transformer Model (Putting it all together)

Finally, the transcript demonstrates assembling the complete Vision Transformer model:

*   `SigVisionEncoder`: A class that stacks multiple encoder layers (`SigVisionEncoderLayer`). The number of layers is a configurable parameter.
*   `SigVisionTransformer`: The main Vision Transformer class that integrates:
    *   `SigVisionEmbeddings`: Embedding layer.
    *   `SigVisionEncoder`: Encoder layers.
    *   `nn.LayerNorm`: Post-layer normalization applied after the encoder.
*   **Forward Pass:** The forward pass of the `SigVisionTransformer` class takes pixel values as input, passes them through the embedding layer, encoder, and post-layer normalization, and returns the final image embeddings.

### Sanity Checks and Validation

Throughout the coding process, the transcript emphasizes sanity checks and validation:

*   **Shape Verification:** Checking the shapes of tensors at each stage to ensure they match expectations.
*   **Parameter Matching with Hugging Face:**  Comparing the initialized weights and biases of the scratch-built model with those of the pre-trained Hugging Face model to verify correct implementation.
*   **Output Comparison:**  Comparing the output of the scratch-built model with the output of the Hugging Face model for the same input to ensure numerical correctness.
*   **Key Matching:** Validating that the keys in the state dictionaries of both models match, confirming that the weights are being loaded into the correct layers.

These rigorous checks ensure that the scratch-built model is functionally equivalent to the pre-trained Hugging Face model.

### Applications of Vision Transformers

The transcript concludes by briefly mentioning the applications of Vision Transformers:

*   **Image Classification:** ViTs can be used as image classifiers by training a classification head on top of the image embeddings.
*   **Vision Language Models (VLMs):** ViTs serve as powerful vision encoders in VLMs, enabling models to understand and process both visual and textual information for tasks like image captioning, visual question answering, and more.
*   **Other Vision and Vision-Language Tasks:** ViTs are versatile and can be adapted for a wide range of computer vision and multimodal tasks.

## Conclusion

This chapter has provided a comprehensive overview of Vision Transformers, starting from their fundamental principles to a conceptual walkthrough of building a SIGL Vision Transformer from scratch. By understanding the concepts of patch embeddings, position embeddings, self-attention, and the overall Transformer architecture, and by contrasting CLIP and SIGL loss functions, you gain a solid foundation for further exploration into the exciting field of Vision Transformers and their applications in computer vision and multimodal AI. The conceptual coding walkthrough, though not fully executable code, provides valuable insights into the implementation details and validation strategies essential for building and verifying such models.
