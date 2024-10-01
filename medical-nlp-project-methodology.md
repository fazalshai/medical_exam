# Medical NLP Project: Methodology and Approach

## 1. Data Preprocessing

### Approach:
- We assumed the data was in CSV format with columns for 'Report Name', 'History', 'Observation', and 'Impression'.
- We combined 'Report Name', 'History', and 'Observation' as input, and used 'Impression' as the target output.

### Methodology:
- Used pandas to load and process the CSV data.
- Created input-output pairs for each report.
- Split the data into training and evaluation sets (300 for training, 30 for evaluation).

### Assumptions:
- The CSV file contains all necessary columns.
- The data is clean and doesn't require extensive preprocessing.

## 2. Model Selection and Fine-tuning

### Approach:
- Initially attempted to use the Gemma 2B model, then switched to GPT-2 small due to memory constraints.
- Focused on optimizing for limited computational resources (Colab environment).

### Methodology:
- Used Hugging Face's Transformers library for model loading and fine-tuning.
- Implemented a custom tokenization function to prepare data for language modeling.
- Utilized the Trainer class from Transformers for the fine-tuning process.

### Assumptions:
- A smaller model (GPT-2) can still provide meaningful results for this task.
- The medical reports can be effectively processed within a 128-token limit.

## 3. Memory Optimization

### Approach:
- Iteratively adjusted the setup to work within Colab's memory constraints.
- Eventually switched to CPU training when GPU memory was insufficient.

### Methodology:
- Reduced model size (from Gemma 2B to GPT-2 small).
- Decreased maximum token length from 512 to 128.
- Implemented gradient accumulation and mixed precision training (when using GPU).
- Forced CPU usage when GPU memory was still insufficient.

### Assumptions:
- The trade-off between model size/complexity and ability to run in a constrained environment is acceptable for this project.

## 4. Training Process

### Approach:
- Focused on making the training process run successfully, even if at reduced speed or capacity.

### Methodology:
- Used a relatively small number of epochs (3) to keep training time manageable.
- Implemented logging and progress bars for better monitoring.
- Prepared the data for causal language modeling by setting up proper labels.

### Assumptions:
- Three epochs are sufficient for the model to learn meaningful patterns from the data.
- The small batch size (4) is adequate for effective training.

## 5. Evaluation (Planned)

### Approach:
- Plan to use perplexity and ROUGE scores for model evaluation.

### Methodology:
- Will generate impressions using the fine-tuned model on the evaluation set.
- Will compute perplexity to measure how well the model predicts the sample text.
- Will use ROUGE scores to compare generated impressions with the ground truth.

### Assumptions:
- Perplexity and ROUGE scores are appropriate metrics for this medical report generation task.
- The evaluation set (30 samples) is representative of the overall data distribution.

## General Assumptions and Limitations

1. The project assumes that the medical reports follow a consistent format and language style.
2. We assume that fine-tuning a general-purpose language model (like GPT-2) can adapt it sufficiently for medical report generation.
3. Due to resource constraints, we're not able to use larger, potentially more suitable models like GPT-3 or specialized medical language models.
4. The approach doesn't incorporate domain-specific medical knowledge beyond what's present in the training data and the pre-trained model's knowledge.
5. We assume that the ethical and privacy considerations related to medical data have been addressed before the data was provided for this project.

This methodology reflects an iterative process of adapting to technical constraints while trying to maintain the core objectives of the project. The focus has been on creating a working pipeline that can be further optimized or scaled up given more resources.
