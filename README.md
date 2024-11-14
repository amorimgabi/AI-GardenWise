# AI GardenWise - a Gardening Q&A Fine-Tuned Gemma Model

This project involves fine-tuning the **Gemma-2b-en model** with a custom dataset of gardening-related questions and answers. The model, named **AI GardenWise**, provides expert guidance on various gardening topics such as soil preparation, plant selection, watering schedules, pest control, and more. The project is part of a fellowship hosted by KaggleX.

## Project Overview

The objective of this project is to build a chatbot to assist home and community gardeners with relevant, accurate information. Using a fine-tuned version of Gemma 2b, the model is trained with a growing dataset of 939 examples to answer user queries in an informative and supportive manner.

## Dataset

The dataset, `dataset_plants_v5.jsonl`, consists of 939 examples of gardening-related instructions and responses. Each entry in the dataset is formatted as follows:

```json
{
  "instruction": "How often should I water my tomato plants?",
  "response": "Tomato plants typically need watering every 2-3 days, depending on the weather and soil conditions..."
}
```

Each entry is preprocessed into a single string format for input to the model.

## Model

We use the `GemmaCausalLM` model from `keras_nlp` with the Gemma 2b preset and apply **LoRA** (Low-Rank Adaptation) to optimize memory use during fine-tuning. We also set a sequence length limit of 256 tokens to manage input length.

### Requirements

- Python 3.x
- TensorFlow
- keras_nlp
- Pandas
- JSON

### Installation

To install the required packages, use the following command:

```bash
pip install tensorflow keras_nlp pandas
```

### Usage

1. **Set up the Dataset:** Load the JSONL dataset and format it as strings for each example.
2. **Instantiate the Model:** Use the Gemma 2b model from `keras_nlp.models.GemmaCausalLM`.
3. **Preprocess the Data:** Format each question-response pair as a single input string.
4. **Fine-tune the Model:** Compile and fine-tune the model with the `AdamW` optimizer, using `SparseCategoricalCrossentropy` as the loss function.

### Example Code

Here’s a simplified version of the code to load, preprocess, and fine-tune the model:

```python
import os
import json
import pandas as pd
import tensorflow as tf
from tensorflow import keras
from keras_nlp.models import GemmaCausalLM

# Load and preprocess the dataset
data_path = "/kaggle/input/gardening-q-and-a/dataset_plants_v5.jsonl"
data_list = []
with open(data_path) as file:
    for line in file:
        features = json.loads(line)
        template = "Instruction:\n{instruction}\n\nResponse:\n{response}"
        data_list.append(template.format(**features))

# Load Gemma model and configure settings
gemma_lm = GemmaCausalLM.from_preset("gemma2_2b_en")
gemma_lm.backbone.enable_lora(rank=4)
gemma_lm.preprocessor.sequence_length = 256

# Set up the optimizer
optimizer = keras.optimizers.AdamW(learning_rate=5e-5, weight_decay=0.01)
optimizer.exclude_from_weight_decay(var_names=["bias", "scale"])

# Compile and train the model
gemma_lm.compile(
    loss=keras.losses.SparseCategoricalCrossentropy(from_logits=True),
    optimizer=optimizer,
    weighted_metrics=[keras.metrics.SparseCategoricalAccuracy()],
)
gemma_lm.fit(data_list, epochs=1, batch_size=1)
```

# Kaggle

The fine-tuned model can be downloaded at Kaggle:

Model card - 
![image](https://github.com/user-attachments/assets/06d4f92e-acfd-4dbe-85bf-fd47ead77cfa)

## Contributions

Contributions, suggestions, and improvements are welcome. Please open an issue or submit a pull request to propose changes.



