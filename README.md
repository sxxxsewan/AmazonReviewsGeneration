# Amazon Reviews Generation with DistilGPT-2

This project implements a text generation model based on **DistilGPT-2** for generating Amazon-style product reviews. The model is conditioned on three input attributes:

* Review rating (1–5 stars)
* Customer country
* Review topic

The model learns review patterns from historical Amazon reviews and generates realistic review texts based on the provided parameters.

## Project Structure

```text
.
├── train.ipynb          # Model training pipeline
├── test.ipynb           # Model evaluation and inference
├── models/             # Pretrained model files
├── data/               # Dataset directory
└── README.md
```

## Features

* Data preprocessing and cleaning
* Review generation conditioned on rating, country, and topic
* Fine-tuning of DistilGPT-2
* Automatic evaluation using:

  * Perplexity
  * BLEU
  * ROUGE
* Interactive review generation

## Dataset

The model was trained on Amazon customer reviews containing:

* Review text
* Rating
* Country
* Review title/topic

During preprocessing:

* Missing values are removed
* Ratings are converted to numerical values
* Review titles are used as topics
* Text is cleaned and normalized

## Model

The project uses **DistilGPT-2**, a lightweight version of GPT-2 that provides a good balance between generation quality and computational efficiency.

Special prompt tokens are used to condition generation:

```text
|<prompt>| RATING:<rating> COUNTRY:<country> TOPIC:<topic> |<review>|
```

Example:

```text
|<prompt>| RATING:5 COUNTRY:US TOPIC:Delivery |<review>|
```

## Installation

Install the required packages:

```bash
pip install torch transformers datasets evaluate sacrebleu rouge-score pandas numpy matplotlib tqdm
```

## Training

To train the model from scratch, open and run:

```bash
train.ipynb
```

The notebook performs:

1. Data loading and preprocessing
2. Train/validation/test split
3. Tokenizer preparation
4. DistilGPT-2 fine-tuning
5. Saving model weights and metadata

## Pretrained Models

The repository already contains pretrained model weights inside the `models/` directory.

**You do not need to retrain the model to run evaluation or generate reviews.**

Simply load the saved model from the `models/` folder and run the inference notebook.

## Testing and Evaluation

To evaluate the model and generate reviews, run:

```bash
test.ipynb
```

The notebook calculates:

* Perplexity
* BLEU score
* ROUGE-1
* ROUGE-2
* ROUGE-L

It also generates example reviews and visualizes evaluation results.

## Example Generation

Input:

```text
Rating: 1
Country: GB
Topic: Delivery issues
```

Generated review:

```text
The delivery took much longer than expected. The package arrived damaged and customer support was not helpful. Overall, a disappointing experience.
```

## Results

The model demonstrates the ability to generate coherent reviews that reflect:

* Sentiment associated with the rating
* Topic-specific vocabulary
* Country-related patterns present in the training data

## Future Improvements

* Larger transformer architectures
* Additional conditioning features
* Better topic extraction
* Human evaluation of generated reviews
* Hyperparameter optimization

## Author

Developed as a Natural Language Processing project focused on conditional text generation using Transformer-based language models.
