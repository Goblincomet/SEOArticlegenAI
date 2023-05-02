# SEO Article Generator
This project is a tool to automatically generate 10's to 100's of thousand SEO-optimized articles using OpenAI's Davinci Model. It reads prompts from a CSV file, sends the prompts to the OpenAI API, and processes the generated responses into structured articles, which are then saved to a separate CSV file.

## How it works
The script has two main components:

- The `prompt_generator.py` script, which generates a list of prompts based on an SEO template file.
- The `main` script, which processes the generated prompts using OpenAI's Davinci and saves the generated articles to a CSV file.

## Prompt Generation
The prompt_generator.py script takes an SEO template file as input, which contains a list of keys in the following format:
```
Category,object,type
BikeBrands	Scott	bikebrand
BikeBrands	Orbea	bikebrand
BikeBrands	Raleigh	bikebrand
BikeBrands	Merida	bikebrand
BikeBrands	What is {bikebrand}?	question
BikeBrands	A beginner's guide to {bikebrand} bikes	question
BikeBrands	{bikebrand} bike review: Pros and cons	question
BikeBrands	Top alternatives to {bikebrand} bikes	question
...
```

Each row represents a category, an object, and its type. The script generates a list of prompts by combining objects and their types. The prompts are then saved to an output CSV file, which will be used as input for the main script.

These are then keyed into statements to create a semantic sequence:

```
e.g. Based on the above statement "BikeBrands	{bikebrand} bike review: Pros and cons	question"

The above produces the following permutations:
- Orbea bike review: Pros and cons
- Raleigh bike review: Pros and cons
```


## Article Generation
The main script reads the prompts from the output CSV file generated by prompt_generator.py. For each prompt, it sends a request to OpenAI's API, passing the prompt and some additional parameters like temperature, max tokens, top-p, frequency penalty, and presence penalty.

The Davinci model processes the prompt and generates a response. The script then processes the response and extracts the article's title, subtitle, and body. The article is then saved to a separate CSV file.

### Usage
1. Set up your OpenAI API key and organization ID as environment variables. You can use a .env file for this purpose:
```
OPENAI_API_KEY=your_openai_api_key
OPENAI_ORGANIZATION_ID=your_openai_organization_id (**Optional**)
```
2. Modify the USE_SAMPLE_PROMPTS variable in the main script to control whether to use the input file or sample prompts:
```
USE_SAMPLE_PROMPTS = True  # Set to False to use input file
```
3. Run the main script:
```
python main.py
```
The script will generate a list of prompts based on the SEO template file, send the prompts to OpenAI's API, and save the generated articles to a CSV file.
