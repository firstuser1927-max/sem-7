# DLPP Unit 1 Reference Sheet: Deep Learning Basics

**Subject:** Deep Learning Principles and Practices (3174201) | **Unit:** 1 (Introduction)

---

## 🔑 Key Definitions (Must-Know for Exams)

*   **Deep Learning (DL):** A subset of Machine Learning that uses multi-layered Artificial Neural Networks (ANNs) to automatically learn representations and hierarchical features from raw data.
*   **Feature Engineering:** The manual process of extracting relevant characteristics, shapes, or features from raw data before passing it to a Machine Learning algorithm. *Deep Learning eliminates this bottleneck.*
*   **Artificial Neural Network (ANN):** A computational model inspired by the structure and function of biological neural networks (the human brain).
*   **Black Box Problem:** The lack of interpretability in deep learning models due to their millions/billions of internal weights, making it extremely difficult to explain *why* a model made a specific prediction.
*   **Hidden Layers:** The layers of nodes between the input layer and the output layer in a neural network that extract increasingly complex patterns (e.g., edges ➡️ shapes ➡️ objects).

---

## 📊 Summary Comparison Tables

### 1. Machine Learning (ML) vs. Deep Learning (DL)
| Dimension | Machine Learning (Traditional) | Deep Learning |
| :--- | :--- | :--- |
| **Data Requirements** | Performs well on small/medium datasets. | Requires massive amounts of data to achieve high accuracy. |
| **Feature Extraction** | Depends on human experts (Feature Engineering). | Automatically learns features from raw data. |
| **Hardware** | Runs efficiently on standard CPUs. | Requires specialized hardware (GPUs/TPUs) for parallel math. |
| **Training Time** | Quick (minutes to hours). | Slow (days to weeks). |
| **Interpretability** | High (e.g., easy to see Decision Tree branches). | Low (Black Box). |

### 2. Biological (BNN) vs. Artificial (ANN) Neurons
| Biological Brain Component | Artificial equivalent | Practical Function |
| :--- | :--- | :--- |
| **Dendrite** | **Inputs ($x_1, x_2, \dots$)** | Receives signals/features from the environment or other nodes. |
| **Synapse** | **Weights ($w_1, w_2, \dots$)** | Represents the strength or importance of the connection. |
| **Soma (Cell Body)** | **Activation Function ($\sigma$)** | Sums incoming weighted signals and decides whether to fire. |
| **Axon** | **Output ($y$)** | Transmits the output signal to the next layer. |

---

## 🚀 Key Applications & Challenges

### Applications in Detail:
1.  **Computer Vision (CV):** Object detection (YOLO), image classification (ResNet), and motion tracking in self-driving cars.
2.  **Natural Language Processing (NLP):** Machine Translation (Google Translate), Sentiment Mining, and Generative Chatbots (ChatGPT/Gemini).
3.  **Medical Analysis:** Diagnostics of X-rays/MRIs to detect cancer or lung diseases.

### Major Challenges:
*   **Data Hunger:** Extremely high dependency on labeled data.
*   **High Computational Cost:** High energy consumption and requirement for expensive GPUs.
*   **Interpretability & Trust:** Hard to audit, leading to safety and bias concerns.

---

## 📝 Top GTU Exam Questions (Practice List)

1.  **Explain the difference between Machine Learning and Deep Learning with a neat diagram. (5 Marks)**
    *   *Tip:* Draw the ML flow (features extracted by hand) vs. the DL flow (raw data directly into network).
2.  **Define ANN. Compare the biological neuron components with their artificial counterparts. (5 Marks)**
    *   *Tip:* Include the BNN/ANN comparison table and draw a simple single-node artificial neuron.
3.  **Discuss the applications and challenges of Deep Learning in detail. (7 Marks)**
    *   *Tip:* Split your answer clearly into "Applications" (categorized by CV, NLP, and Healthcare) and "Challenges" (highlighting data, hardware, and the Black Box problem).
