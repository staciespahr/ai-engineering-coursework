# ai-engineering-coursework

This repository contains my coursework for my AI Architecture & Development CSC595 course

## Assignment 1: API and Local Model Setup

For this assignment, I tested two ways of interacting with large language models: using the Hugging Face API and running a model locally with Ollama.

### Hugging Face API

The `api_test.py` script sends a prompt to a model using the Hugging Face API and prints the generated response in the terminal. I used ChatGPT to help write and troubleshoot the script while setting up the API connection.

The API key is stored as an environment variable and is not included in this repository.

To install the required package:

    pip install huggingface_hub

To run the script:

    python api_test.py

### Ollama

I also used Ollama to run Llama 3.2 3B locally.

To download and run the model:

    ollama pull llama3.2:3b
    ollama run llama3.2:3b

Screenshots in this repository show the successful Hugging Face API call and Ollama session.