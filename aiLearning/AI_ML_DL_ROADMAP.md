# AI / ML / DL Mastery Roadmap
### From Software Engineer to AI/ML Expert — A Complete Technical Roadmap

**Author context:** Software Engineer with basic AI/ML/DL knowledge → Advanced Practitioner
**Estimated total duration:** 12–18 months (part-time, ~10–15 hrs/week) | 6–9 months (full-time)
**Format:** Each topic includes Prerequisites → Core Concepts → Architecture → Real-World Applications → Tools → Resources → Milestone Project

---

## Table of Contents

1. [How to Use This Roadmap](#how-to-use-this-roadmap)
2. [Phase 0: Environment & Tooling Setup](#phase-0-environment--tooling-setup)
3. [Phase 1: Mathematical Foundations](#phase-1-mathematical-foundations)
4. [Phase 2: Python for ML & Data Handling](#phase-2-python-for-ml--data-handling)
5. [Phase 3: Core Machine Learning](#phase-3-core-machine-learning)
6. [Phase 4: Model Evaluation & Optimization](#phase-4-model-evaluation--optimization)
7. [Phase 5: Deep Learning Foundations](#phase-5-deep-learning-foundations)
8. [Phase 6: Computer Vision (CNNs)](#phase-6-computer-vision-cnns)
9. [Phase 7: Sequence Models (RNN/LSTM/GRU)](#phase-7-sequence-models-rnnlstmgru)
10. [Phase 8: Transformers & Attention](#phase-8-transformers--attention)
11. [Phase 9: NLP & Large Language Models](#phase-9-nlp--large-language-models)
12. [Phase 10: Generative AI (GANs, VAEs, Diffusion)](#phase-10-generative-ai-gans-vaes-diffusion)
13. [Phase 11: Reinforcement Learning](#phase-11-reinforcement-learning)
14. [Phase 12: LLM Engineering (RAG, Fine-tuning, Agents)](#phase-12-llm-engineering-rag-fine-tuning-agents)
15. [Phase 13: MLOps & Production Deployment](#phase-13-mlops--production-deployment)
16. [Phase 14: Advanced/Research-Level Topics](#phase-14-advancedresearch-level-topics)
17. [Capstone Project Ideas](#capstone-project-ideas)
18. [Recommended Learning Resources](#recommended-learning-resources)
19. [Suggested Timeline](#suggested-timeline)

---

## How to Use This Roadmap

Each topic block follows this structure:

```
### Topic Name
- Prerequisites:        What you must know before starting
- Core Concepts:        The theory/ideas to internalize
- Architecture:         How the system/model is structured internally
- Real-World Applications: Products you could actually build
- Tools/Libraries:      What to use in practice
- Hands-on Project:     A concrete exercise to cement the topic
```

**Rule of thumb:** Don't move to the next phase until you can (a) explain the current topic to someone else in plain English, and (b) implement it from scratch at least once without a library (for foundational topics), then re-implement it using standard libraries (for practical fluency).

---

## Phase 0: Environment & Tooling Setup

### Topic: Dev Environment
- **Prerequisites:** Basic command-line usage (you have this as an SWE).
- **Core Concepts:** Virtual environments, dependency isolation, reproducibility.
- **Architecture:**
  ```
  Local Machine
  ├── conda/venv environment (Python 3.10+)
  ├── Jupyter Lab / VS Code + Jupyter extension
  ├── Git + GitHub (version control for notebooks/models)
  └── GPU access: Google Colab (free) → Kaggle Kernels → Cloud (AWS/GCP) → Local GPU
  ```
- **Real-World Application:** Every ML project starts here — this is your "Hello World" infra.
- **Tools:** `conda`/`venv`, `pip`, Jupyter, VS Code, Docker (later), Git.
- **Hands-on:** Set up a repo with `environment.yml`, a notebook, and push to GitHub with a proper `.gitignore` for datasets/models.

---

## Phase 1: Mathematical Foundations

> You don't need a PhD in math, but you need enough to *understand why* algorithms work, not just call `.fit()`.

### 1.1 Linear Algebra
- **Prerequisites:** High-school algebra.
- **Core Concepts:** Vectors, matrices, matrix multiplication, transpose, dot/cross product, eigenvalues & eigenvectors, matrix decomposition (SVD, PCA basis), norms (L1/L2).
- **Architecture (mental model):** Data = matrices. A neural network layer = matrix multiplication + bias + non-linearity. Almost all ML operations are linear algebra at scale (GPU-accelerated tensor ops).
- **Real-World Application:** Image data as tensors (H×W×C), recommendation systems (matrix factorization), PCA-based compression/dimensionality reduction for search/analytics dashboards.
- **Tools:** NumPy, `numpy.linalg`.
- **Hands-on:** Implement matrix multiplication, SVD-based image compression, and PCA from scratch using only NumPy.

### 1.2 Calculus
- **Prerequisites:** Linear Algebra basics.
- **Core Concepts:** Derivatives, partial derivatives, chain rule, gradients, gradient descent, Jacobians/Hessians (conceptual).
- **Architecture (mental model):** Training = "walk downhill on an error surface using the gradient as your compass." Backpropagation is just repeated chain-rule application.
- **Real-World Application:** Understanding *why* a model "learns" — critical for debugging vanishing/exploding gradients in production DL systems.
- **Tools:** NumPy, symbolic tools like SymPy (optional), manual derivations on paper.
- **Hands-on:** Implement gradient descent from scratch to fit a line (linear regression) without scikit-learn.

### 1.3 Probability & Statistics
- **Prerequisites:** Basic algebra.
- **Core Concepts:** Probability distributions (Normal, Bernoulli, Binomial, Poisson), Bayes' theorem, conditional probability, expectation/variance, hypothesis testing, p-values, confidence intervals, MLE (Maximum Likelihood Estimation), Central Limit Theorem.
- **Architecture (mental model):** Every ML model is a probabilistic statement — classification outputs are probability distributions over classes; loss functions are often derived from MLE (e.g., cross-entropy = negative log-likelihood).
- **Real-World Application:** A/B testing for product features, fraud detection (anomaly = low-probability event), spam filters (Naive Bayes), confidence intervals in dashboards/analytics tools.
- **Tools:** `scipy.stats`, `statsmodels`.
- **Hands-on:** Build a Naive Bayes spam classifier from scratch using Bayes' theorem manually.

### 1.4 Optimization Basics
- **Prerequisites:** Calculus, Linear Algebra.
- **Core Concepts:** Convex vs non-convex functions, local/global minima, learning rate, momentum, SGD, Adam optimizer (conceptual now, deep dive later in Phase 5).
- **Real-World Application:** Tuning training speed/stability for any DL model you'll build later.
- **Tools:** NumPy for manual implementation.
- **Hands-on:** Implement vanilla Gradient Descent, Momentum, and compare convergence speed on a toy loss surface.

---

## Phase 2: Python for ML & Data Handling

### 2.1 NumPy, Pandas, Matplotlib/Seaborn
- **Prerequisites:** Python fundamentals (you have this).
- **Core Concepts:** Vectorized operations, broadcasting, DataFrames, groupby/merge/pivot, data visualization principles.
- **Real-World Application:** Any data pipeline — cleaning sales data, log analysis, exploratory data analysis (EDA) for a business dashboard.
- **Tools:** `numpy`, `pandas`, `matplotlib`, `seaborn`, `plotly`.
- **Hands-on:** Take a messy real-world CSV (e.g., Kaggle's Titanic or a company dataset) and do full EDA — missing values, outliers, distributions, correlations.

### 2.2 Data Preprocessing & Feature Engineering
- **Prerequisites:** Pandas, basic statistics.
- **Core Concepts:** Handling missing data (imputation), encoding categorical variables (one-hot, label, target encoding), feature scaling (standardization, normalization), feature selection, handling imbalanced datasets (SMOTE, class weights), outlier detection.
- **Architecture (pipeline):**
  ```
  Raw Data → Cleaning → Encoding → Scaling → Feature Selection → Train/Val/Test Split → Model
  ```
- **Real-World Application:** Preparing customer churn data, credit scoring datasets, sensor/IoT data for any downstream ML model.
- **Tools:** `scikit-learn.preprocessing`, `imbalanced-learn`, `feature-engine`.
- **Hands-on:** Build a reusable `sklearn.Pipeline` for preprocessing a real dataset end-to-end.

---

## Phase 3: Core Machine Learning

### 3.1 Supervised Learning — Regression
- **Prerequisites:** Linear algebra, calculus, Pandas.
- **Core Concepts:** Linear Regression, Ridge/Lasso (regularization), Polynomial Regression, assumptions of linear models, cost function (MSE).
- **Architecture:**
  ```
  Input features (X) → Weighted sum (W·X + b) → Predicted value (ŷ)
  Loss = MSE(y, ŷ) → Gradient Descent updates W, b
  ```
- **Real-World Application:** House price prediction, sales forecasting, demand estimation, salary prediction tools.
- **Tools:** `scikit-learn.linear_model`.
- **Hands-on:** Predict housing prices (Boston/California housing dataset) with Linear + Ridge + Lasso, compare performance.

### 3.2 Supervised Learning — Classification
- **Prerequisites:** Regression concepts, probability.
- **Core Concepts:** Logistic Regression, Decision Trees, K-Nearest Neighbors (KNN), Support Vector Machines (SVM), Naive Bayes, decision boundaries, sigmoid/softmax functions.
- **Architecture:**
  ```
  Logistic Regression: X → Linear combination → Sigmoid → Probability → Threshold → Class
  Decision Tree: Recursive binary splits based on feature thresholds minimizing impurity (Gini/Entropy)
  SVM: Find maximum-margin hyperplane separating classes (kernel trick for non-linear data)
  ```
- **Real-World Application:** Email spam detection, credit card fraud detection, medical diagnosis (disease/no disease), customer churn prediction.
- **Tools:** `scikit-learn` (LogisticRegression, DecisionTreeClassifier, SVC, KNeighborsClassifier).
- **Hands-on:** Build a churn prediction classifier; compare Logistic Regression vs Decision Tree vs SVM using accuracy/precision/recall.

### 3.3 Ensemble Methods
- **Prerequisites:** Decision Trees.
- **Core Concepts:** Bagging (Random Forest), Boosting (AdaBoost, Gradient Boosting, XGBoost, LightGBM, CatBoost), Stacking, bias-variance tradeoff.
- **Architecture:**
  ```
  Random Forest: Many decision trees trained on bootstrapped samples → majority vote/average
  Gradient Boosting: Sequential trees, each correcting the errors (residuals) of the previous one
  ```
- **Real-World Application:** Kaggle-competition-grade tabular models — loan default prediction, click-through-rate (CTR) prediction, insurance risk scoring. **This is the most commonly used ML approach in real industry tabular-data products.**
- **Tools:** `scikit-learn.ensemble`, `xgboost`, `lightgbm`, `catboost`.
- **Hands-on:** Take a Kaggle tabular competition dataset and build an XGBoost/LightGBM model; tune hyperparameters with `Optuna`.

### 3.4 Unsupervised Learning
- **Prerequisites:** Linear algebra (PCA), distance metrics.
- **Core Concepts:** K-Means Clustering, Hierarchical Clustering, DBSCAN, PCA (dimensionality reduction), t-SNE/UMAP (visualization), Anomaly Detection (Isolation Forest, One-Class SVM).
- **Architecture:**
  ```
  K-Means: Initialize k centroids → Assign points to nearest centroid → Recompute centroids → Repeat until convergence
  ```
- **Real-World Application:** Customer segmentation (marketing), anomaly detection in network traffic (cybersecurity), document clustering, gene expression analysis.
- **Tools:** `scikit-learn.cluster`, `scikit-learn.decomposition`, `umap-learn`.
- **Hands-on:** Segment customers from an e-commerce dataset using K-Means + PCA visualization.

---

## Phase 4: Model Evaluation & Optimization

### Topic: Evaluation Metrics & Validation
- **Prerequisites:** All of Phase 3.
- **Core Concepts:**
  - Classification: Accuracy, Precision, Recall, F1-score, ROC-AUC, Confusion Matrix, PR curves.
  - Regression: MAE, MSE, RMSE, R².
  - Cross-validation (k-fold, stratified), train/val/test splits, data leakage.
  - Overfitting vs Underfitting, Bias-Variance tradeoff, Regularization (L1/L2, Dropout later).
  - Hyperparameter tuning: Grid Search, Random Search, Bayesian Optimization (Optuna).
- **Real-World Application:** Deciding whether a fraud model is *actually* production-ready (precision/recall tradeoffs matter more than raw accuracy in imbalanced real-world problems like fraud or disease detection).
- **Tools:** `scikit-learn.metrics`, `Optuna`, `MLflow` (for experiment tracking).
- **Hands-on:** Take any earlier model and do proper k-fold CV + hyperparameter tuning + log experiments with MLflow.

---

## Phase 5: Deep Learning Foundations

### 5.1 Neural Networks Basics
- **Prerequisites:** Linear algebra, calculus (gradients), Phase 3 classification concepts.
- **Core Concepts:** Perceptron, Multi-Layer Perceptron (MLP), activation functions (ReLU, Sigmoid, Tanh, Softmax), forward propagation, backpropagation, loss functions (Cross-Entropy, MSE), weight initialization, vanishing/exploding gradients.
- **Architecture:**
  ```
  Input Layer → [Linear → Activation] × N Hidden Layers → Output Layer → Loss
                        ↑___________ Backpropagation (chain rule) ___________|
  ```
- **Real-World Application:** Any tabular deep learning task, basis for everything that follows (CV, NLP, GenAI all build on this).
- **Tools:** `PyTorch` (recommended for learning — more explicit/pythonic) or `TensorFlow/Keras`.
- **Hands-on:** Implement a 2-layer neural network from scratch using only NumPy (forward + backward pass), then re-implement using PyTorch.

### 5.2 Training Deep Networks
- **Prerequisites:** 5.1.
- **Core Concepts:** Optimizers (SGD, Momentum, RMSProp, Adam), learning rate scheduling, batch size effects, Batch Normalization, Dropout, early stopping, weight decay, gradient clipping.
- **Real-World Application:** Making any deep model actually converge reliably in production — this is 80% of practical DL debugging skill.
- **Tools:** PyTorch (`torch.optim`, `torch.nn`), TensorBoard/Weights & Biases for monitoring.
- **Hands-on:** Train an MLP on MNIST/Fashion-MNIST; experiment with different optimizers/regularization and log results on W&B.

---

## Phase 6: Computer Vision (CNNs)

### Topic: Convolutional Neural Networks
- **Prerequisites:** Phase 5 (NN basics), basic image representation (pixels as tensors).
- **Core Concepts:** Convolution operation, filters/kernels, stride, padding, pooling (max/avg), feature maps, receptive fields, classic architectures (LeNet, AlexNet, VGG, ResNet, EfficientNet), transfer learning, data augmentation.
- **Architecture:**
  ```
  Input Image → [Conv → BatchNorm → ReLU → Pool] × N → Flatten/GlobalPool → FC Layer(s) → Softmax
  (ResNet adds skip/residual connections to allow much deeper networks without vanishing gradients)
  ```
- **Real-World Application:** Image classification (product categorization), object detection (self-driving cars, retail shelf monitoring — YOLO/Faster R-CNN), facial recognition, medical image diagnosis (tumor detection), OCR, quality-control defect detection in manufacturing.
- **Tools:** `torchvision`, `timm` (pretrained models), `OpenCV`, `albumentations` (augmentation), `YOLOv8/Ultralytics` for detection.
- **Hands-on:** Fine-tune a pretrained ResNet/EfficientNet on a custom image classification dataset (transfer learning); then try object detection with YOLOv8 on a custom dataset.

---

## Phase 7: Sequence Models (RNN/LSTM/GRU)

### Topic: Recurrent Architectures
- **Prerequisites:** Phase 5, basic understanding of sequential/time-series data.
- **Core Concepts:** RNN cell mechanics, vanishing gradient problem in RNNs, LSTM (forget/input/output gates), GRU, bidirectional RNNs, sequence-to-sequence models, teacher forcing.
- **Architecture:**
  ```
  x_t → [RNN/LSTM/GRU Cell] → h_t (hidden state passed to next timestep)
  Seq2Seq: Encoder (compresses input sequence) → Context Vector → Decoder (generates output sequence)
  ```
- **Real-World Application:** Stock price forecasting, sensor time-series anomaly detection, early machine translation systems, text generation (pre-Transformer era), speech recognition.
- **Tools:** PyTorch `nn.LSTM`/`nn.GRU`.
- **Hands-on:** Build an LSTM-based time-series forecaster (e.g., stock/weather data) and a simple character-level text generator.

> **Note:** RNN/LSTM are increasingly legacy for NLP (replaced by Transformers) but are still important for understanding sequence modeling fundamentals and are still used in some time-series/streaming contexts.

---

## Phase 8: Transformers & Attention

### Topic: The Transformer Architecture
- **Prerequisites:** Phase 5, Phase 7 (helps to appreciate *why* attention was revolutionary), linear algebra (matrix multiplications for attention scores).
- **Core Concepts:** Self-attention, multi-head attention, positional encoding, Query/Key/Value mechanism, encoder-decoder structure, layer normalization, the "Attention is All You Need" paper concepts.
- **Architecture:**
  ```
  Input Embeddings + Positional Encoding
        ↓
  [Multi-Head Self-Attention → Add & Norm → Feed-Forward → Add & Norm] × N (Encoder)
        ↓
  [Masked Self-Attention → Cross-Attention → Feed-Forward] × N (Decoder)
        ↓
  Output Projection → Softmax
  ```
- **Real-World Application:** This is the architecture behind virtually all modern AI products — ChatGPT/Claude, Google Translate, GitHub Copilot, search ranking, document summarization tools.
- **Tools:** `PyTorch`, `Hugging Face Transformers` library.
- **Hands-on:** Implement a minimal Transformer encoder from scratch (attention + FFN block) on a toy task; then use Hugging Face to fine-tune BERT for text classification.

---

## Phase 9: NLP & Large Language Models

### 9.1 Classic NLP Pipeline
- **Prerequisites:** Basic Python string processing.
- **Core Concepts:** Tokenization, stemming/lemmatization, TF-IDF, Bag-of-Words, word embeddings (Word2Vec, GloVe), n-grams.
- **Real-World Application:** Search engines, basic chatbots, keyword extraction, document similarity tools.
- **Tools:** `NLTK`, `spaCy`, `gensim`.
- **Hands-on:** Build a document similarity/search tool using TF-IDF and cosine similarity.

### 9.2 Modern NLP with Transformer-based LLMs
- **Prerequisites:** Phase 8 (Transformers).
- **Core Concepts:** BERT (encoder-only, understanding tasks), GPT family (decoder-only, generation tasks), T5 (encoder-decoder), pretraining vs fine-tuning, tokenization (BPE, WordPiece, SentencePiece), embeddings and semantic search, model scaling laws (conceptual).
- **Architecture:** See Phase 8 — BERT uses encoder stack only; GPT uses decoder stack only (causal/masked self-attention so each token only attends to previous tokens).
- **Real-World Application:** Sentiment analysis systems, chatbots, text summarization tools, code generation assistants, semantic search engines, content moderation systems.
- **Tools:** `Hugging Face Transformers`, `Hugging Face Datasets`, `sentence-transformers`.
- **Hands-on:** Fine-tune a BERT model for a custom classification task (e.g., support-ticket categorization); build a semantic search tool using `sentence-transformers`.

---

## Phase 10: Generative AI (GANs, VAEs, Diffusion)

### 10.1 Autoencoders & VAEs
- **Prerequisites:** Phase 5, Phase 6 (for image-based examples).
- **Core Concepts:** Encoder-decoder compression, latent space, Variational Autoencoders (probabilistic latent space, reparameterization trick).
- **Architecture:**
  ```
  Input → Encoder → Latent Vector (z) → Decoder → Reconstructed Output
  (VAE: Encoder outputs mean & variance of a distribution instead of a single point)
  ```
- **Real-World Application:** Anomaly detection (reconstruction error), data denoising, image compression, synthetic data generation for rare classes.
- **Tools:** PyTorch.
- **Hands-on:** Build an autoencoder for anomaly detection on a fraud/sensor dataset.

### 10.2 GANs (Generative Adversarial Networks)
- **Prerequisites:** 10.1, CNNs (Phase 6).
- **Core Concepts:** Generator vs Discriminator, adversarial training, mode collapse, DCGAN, StyleGAN (conceptual).
- **Architecture:**
  ```
  Noise (z) → Generator → Fake Image
  Fake/Real Image → Discriminator → Real or Fake? (Binary Classification)
  Both networks trained adversarially (minimax game)
  ```
- **Real-World Application:** Synthetic image generation, deepfake detection (understanding the tech helps build detectors), data augmentation for rare classes, style transfer apps.
- **Tools:** PyTorch.
- **Hands-on:** Build a DCGAN to generate handwritten digits (MNIST) or simple faces.

### 10.3 Diffusion Models
- **Prerequisites:** 10.1, 10.2 (conceptual contrast helps), probability (Markov chains).
- **Core Concepts:** Forward diffusion (adding noise), reverse diffusion (denoising), U-Net architecture, classifier-free guidance, latent diffusion (Stable Diffusion's approach).
- **Architecture:**
  ```
  Training: Image → Add noise progressively (forward process) → Model learns to predict/remove noise at each step
  Inference: Pure noise → Iteratively denoise (reverse process, guided by text/conditioning) → Generated Image
  ```
- **Real-World Application:** Text-to-image generation (Stable Diffusion/DALL·E-style products), image inpainting/editing tools, video generation.
- **Tools:** Hugging Face `diffusers` library.
- **Hands-on:** Use `diffusers` to run/fine-tune a small Stable Diffusion pipeline (LoRA fine-tuning on a custom style/subject).

---

## Phase 11: Reinforcement Learning

### Topic: RL Fundamentals to Deep RL
- **Prerequisites:** Probability, Phase 5 (for Deep RL), basic dynamic programming concepts.
- **Core Concepts:** Markov Decision Processes (MDP), states/actions/rewards/policy, value functions, Q-learning, exploration vs exploitation, Deep Q-Networks (DQN), Policy Gradient methods (REINFORCE), Actor-Critic methods (A2C/A3C), PPO (Proximal Policy Optimization — used in RLHF for LLMs).
- **Architecture:**
  ```
  Agent ⇄ Environment loop:
  Agent observes State (s) → chooses Action (a) via Policy π(a|s) → Environment returns Reward (r) + new State (s')
  Goal: Learn policy π maximizing cumulative discounted reward
  ```
- **Real-World Application:** Game-playing AI (AlphaGo-style), robotics control, recommendation systems (bandits), resource allocation/scheduling optimization, **RLHF (Reinforcement Learning from Human Feedback) — the technique used to align LLMs like ChatGPT/Claude**.
- **Tools:** `Gymnasium` (OpenAI Gym successor), `Stable-Baselines3`, `Ray RLlib`.
- **Hands-on:** Train a DQN agent to solve CartPole/LunarLander in Gymnasium; then read about PPO and how RLHF applies it to LLM fine-tuning.

---

## Phase 12: LLM Engineering (RAG, Fine-tuning, Agents)

> This is the most in-demand practical skill set in 2025-2026 industry AI roles.

### 12.1 Prompt Engineering & LLM APIs
- **Prerequisites:** Phase 9.2.
- **Core Concepts:** Zero-shot/few-shot prompting, chain-of-thought prompting, system/user/assistant roles, temperature/top-p sampling, context windows, structured output generation.
- **Real-World Application:** Any LLM-powered feature — customer support bots, content generation tools, coding assistants.
- **Tools:** Anthropic API (Claude), OpenAI API, `LangChain`/`LlamaIndex` (orchestration, optional but common).
- **Hands-on:** Build a CLI tool that uses an LLM API to summarize/analyze documents with well-engineered prompts.

### 12.2 Embeddings & Vector Databases
- **Prerequisites:** Phase 9.2 (embeddings concept).
- **Core Concepts:** Dense vector embeddings, cosine similarity search, approximate nearest neighbor (ANN) search (HNSW, IVF).
- **Real-World Application:** Semantic search, document Q&A systems, recommendation engines.
- **Tools:** `FAISS`, `Pinecone`, `Weaviate`, `ChromaDB`, `pgvector`.
- **Hands-on:** Build a semantic search engine over a document collection using embeddings + FAISS/Chroma.

### 12.3 RAG (Retrieval-Augmented Generation)
- **Prerequisites:** 12.1, 12.2.
- **Core Concepts:** Chunking strategies, retrieval pipeline, context injection, re-ranking, hybrid search (keyword + semantic), handling hallucination/grounding.
- **Architecture:**
  ```
  User Query → Embed Query → Vector DB Similarity Search → Retrieve Top-K Chunks
       → Inject Chunks + Query into LLM Prompt → Generated, Grounded Answer
  ```
- **Real-World Application:** Internal company knowledge-base chatbots, customer support systems grounded in documentation, legal/medical document Q&A tools. **This is the #1 practical LLM product pattern used in industry.**
- **Tools:** `LangChain`, `LlamaIndex`, vector DBs above.
- **Hands-on:** Build a full RAG chatbot over a set of PDFs (e.g., your company docs or a textbook) with citation of sources.

### 12.4 Fine-tuning LLMs
- **Prerequisites:** Phase 9.2, Phase 5.2 (training dynamics).
- **Core Concepts:** Full fine-tuning vs Parameter-Efficient Fine-Tuning (PEFT), LoRA/QLoRA, instruction tuning, dataset formatting for fine-tuning, quantization (4-bit/8-bit).
- **Real-World Application:** Domain-specific assistants (legal, medical, code) where prompting alone isn't sufficient, custom-tone chatbots for brands.
- **Tools:** Hugging Face `transformers` + `peft` + `bitsandbytes`, `Axolotl`.
- **Hands-on:** LoRA fine-tune a small open-source model (e.g., Llama 3 8B or Mistral 7B) on a custom instruction dataset using a free Colab GPU.

### 12.5 AI Agents
- **Prerequisites:** 12.1–12.3.
- **Core Concepts:** Tool use/function calling, ReAct pattern (reasoning + acting), multi-step planning, agent memory, multi-agent orchestration, evaluation of agentic systems.
- **Architecture:**
  ```
  User Goal → Agent (LLM) → Plans steps → Calls Tools (search/code/API) → Observes results
       → Iterates until goal met or max steps reached → Final Answer
  ```
- **Real-World Application:** Autonomous coding assistants (like Claude Code), research assistants, workflow automation bots, customer service agents that can actually take actions (not just answer).
- **Tools:** `LangGraph`, `Claude Agent SDK` / Anthropic tool-use API, `AutoGen`, `CrewAI`.
- **Hands-on:** Build a multi-tool agent (web search + calculator + code execution) that can autonomously answer multi-step questions.

---

## Phase 13: MLOps & Production Deployment

### Topic: Taking Models to Production
- **Prerequisites:** Solid grasp of at least one full model pipeline (Phases 3–9), general software engineering/DevOps knowledge (you already have this as an SWE — big advantage here).
- **Core Concepts:** Model versioning, experiment tracking, CI/CD for ML, model serving (REST/gRPC), containerization, model monitoring (data drift, model drift), A/B testing in production, feature stores, batch vs real-time inference, scaling inference (GPU serving, quantization, batching).
- **Architecture:**
  ```
  Data Pipeline → Feature Store → Training Pipeline (tracked via MLflow/W&B)
       → Model Registry → CI/CD → Containerized Serving (Docker + K8s)
       → API Gateway → Monitoring (drift/latency/errors) → Feedback Loop → Retraining
  ```
- **Real-World Application:** This is *how every real ML product actually runs* — recommendation engines at scale, fraud detection systems processing millions of transactions, any production LLM application.
- **Tools:** `MLflow`, `DVC` (data version control), `Docker`, `Kubernetes`, `FastAPI`/`TorchServe`/`Triton Inference Server`, `Prometheus`/`Grafana` (monitoring), cloud ML platforms (AWS SageMaker, GCP Vertex AI, Azure ML).
- **Hands-on:** Take any earlier model, wrap it in a FastAPI service, containerize with Docker, deploy on a free-tier cloud instance, and set up basic monitoring/logging.

---

## Phase 14: Advanced/Research-Level Topics

*(Pick based on interest/career direction — you don't need all of these)*

| Topic | What It Covers | Application |
|---|---|---|
| **Explainable AI (XAI)** | SHAP, LIME, attention visualization, model interpretability | Regulatory compliance (finance/healthcare), trust/debugging |
| **Federated Learning** | Training across decentralized devices without moving raw data | Privacy-preserving mobile ML (keyboard prediction, health apps) |
| **Multi-modal Models** | Combining vision + text + audio (CLIP, Flamingo-style, GPT-4V-style) | Visual question answering, multi-modal search, accessibility tools |
| **Graph Neural Networks (GNNs)** | Learning on graph-structured data (GCN, GAT, GraphSAGE) | Social network analysis, fraud rings detection, molecule/drug discovery, recommendation |
| **Model Compression** | Quantization, pruning, knowledge distillation | Running models on edge devices/mobile, cost reduction at scale |
| **AI Safety & Alignment** | RLHF deep dive, constitutional AI, red-teaming, adversarial robustness | Building trustworthy, safe AI products |
| **Time Series Deep Learning** | Temporal Fusion Transformers, N-BEATS, Prophet | Advanced forecasting for finance/supply chain |
| **Speech/Audio ML** | ASR (Whisper-style), TTS, speaker diarization | Voice assistants, transcription tools, accessibility |

---

## Capstone Project Ideas

Pick 2–3 across different phases to build a strong portfolio:

1. **End-to-end tabular ML product:** Fraud/churn detection with XGBoost + FastAPI + Docker deployment + monitoring dashboard.
2. **Computer vision app:** Real-time object detection (YOLOv8) deployed as a web app (e.g., defect detection, PPE compliance monitor).
3. **RAG-based internal knowledge assistant:** Full pipeline — document ingestion, chunking, embeddings, vector DB, LLM answer generation with citations, deployed as a chatbot.
4. **Fine-tuned domain LLM:** LoRA-fine-tuned open-source model specialized for a niche domain (e.g., legal contract analysis, customer support for your industry).
5. **Autonomous AI agent:** Multi-tool agent that can research a topic, write code, run it, and report results — a mini "Claude Code" clone.
6. **Generative AI app:** Text-to-image fine-tuning (LoRA on Stable Diffusion) for a custom style/product catalog generator.

---

## Recommended Learning Resources

**Courses**
- Andrew Ng — *Machine Learning Specialization* & *Deep Learning Specialization* (Coursera)
- fast.ai — *Practical Deep Learning for Coders*
- CS231n (Stanford) — Convolutional Neural Networks for Visual Recognition (free lectures/notes online)
- CS224n (Stanford) — NLP with Deep Learning
- Hugging Face NLP Course (free, hands-on, excellent for Transformers/LLMs)
- DeepLearning.AI — *LangChain for LLM Application Development*, *How Diffusion Models Work*, *RLHF* short courses

**Books**
- *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* — Aurélien Géron
- *Deep Learning* — Goodfellow, Bengio, Courville (the theory bible)
- *Designing Machine Learning Systems* — Chip Huyen (for MLOps/production thinking)
- *Speech and Language Processing* — Jurafsky & Martin (free online, for NLP depth)

**Practice Platforms**
- Kaggle (competitions + datasets + public notebooks to learn from)
- Hugging Face Hub (models, datasets, Spaces for deployment practice)
- Papers With Code (to see SOTA + implementations for any topic)

**Stay Current**
- arXiv (cs.LG, cs.CL, cs.CV categories)
- Papers With Code trending section
- Hugging Face blog, Anthropic/OpenAI/Google DeepMind research blogs

---

## Suggested Timeline

| Weeks | Focus |
|---|---|
| 1–3 | Phase 0, 1, 2 (Math + Python + Data handling) |
| 4–7 | Phase 3, 4 (Core ML + Evaluation) — build 2-3 classic ML projects |
| 8–10 | Phase 5 (DL Foundations) |
| 11–13 | Phase 6 (CV) |
| 14–15 | Phase 7 (Sequence models) |
| 16–18 | Phase 8, 9 (Transformers + NLP/LLMs) |
| 19–21 | Phase 10 (GenAI: GANs/VAE/Diffusion) |
| 22–23 | Phase 11 (RL) |
| 24–28 | Phase 12 (LLM Engineering: RAG, Fine-tuning, Agents) — **highest ROI for current job market** |
| 29–32 | Phase 13 (MLOps) |
| 33+ | Phase 14 (Advanced topics based on specialization) + Capstone projects |

> **Fast-track note:** If your goal is to get industry-relevant quickly (e.g., for a job switch), you can compress by doing Phases 0–5 solidly, then jumping straight to Phase 8, 9, 12, and 13 — this covers the majority of real-world LLM/product-focused roles. Come back for CV (Phase 6), GenAI (Phase 10), and RL (Phase 11) based on your specific job target.

---

## Final Notes

- **Build in public:** Push every project to GitHub with a clear README, even small ones. This becomes your portfolio.
- **Depth over breadth initially:** Better to deeply understand Linear/Logistic Regression and Backpropagation than to superficially skim 20 topics.
- **Re-implement before you rely on libraries:** For at least the core topics (gradient descent, a neural net, attention mechanism), write it from scratch once. This is what separates "library user" from "practitioner who understands the system."
- **As a software engineer, your unfair advantage is Phase 13 (MLOps)** — most ML practitioners are weak at production engineering. Lean into this.
