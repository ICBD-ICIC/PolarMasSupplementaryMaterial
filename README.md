
# A Large Language Model Agentic Approach to Study Affective Polarization - Supplementary Material

In this repository, you will find:

* The complete code for the presented platform.

* A detailed, step-by-step guide on how to run the platform.

* Implementations of the examples described in the paper, including agent configurations, outputs, and instructions to run them.

* An example of an agent's memory contents for Example 1.

* The persona descriptions and their corresponding political standpoints from Section 5.2, along with the code and data used to generate them and instructions on how to run it.

## Platform Requirements Installation and Execution

The platform code is contained in the `polarmas_platform.py` file. It includes two main classes: `Agent` and `Platform`, implementing all methods and functionalities as described in the associated paper.

We developed and tested the platform using Python version 3.13. If you choose to use a different Python version, please be aware that we cannot guarantee correct execution or full compatibility.

Before running the platform, it is recommended to create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

Then install the required dependencies:

```bash
pip install -r requirements.txt
```

You must also set up a Google API key for Gemini Studio AI. Create an API key in [Google AI Studio](https://aistudio.google.com/app/apikey), and set it as an environment variable by updating the `.env` file (replace the placeholder `your_api_key` with your actual key).

## Examples and Experiments

We provide the output files used in the paper within the `outputs` directory. However, you can also reproduce these experiments yourself. Please note that the results may vary between runs—even with the same configurations—because the agents use a language model with a temperature of 0.7, which introduces randomness in the output.

To get started, you can run Experiment 1 with the following command:

```
python ./paper_example.py
```

The output will be printed to the console and saved as a JSON file in the `outputs` directory. The filename will start with `paper_example`. For agent configuration details, refer to the file `agents/paper_example.csv`.

If you want the full view of the agents' memory throughout the experiment, refer to `paper_example_memory.txt`.

### Cross-Partisan Conversation

This experiment includes two variants: `political` and `non_political`.

- Output files are saved in: `outputs/cross_partisan_conversation/`
- Agent configurations are stored in: `agents/cross_partisan_conversation/`

Each run produces uniquely named files to distinguish between the variants.

**Before running**, make sure to uncomment the desired experiment configuration in `cross_partisan_conversation.py`.

Then, run the experiment with:

```
python ./cross_partisan_conversation.py
```

### Simulating Social Media

This experiment includes three variants:
- `simulating_social_media`
- `simulating_social_media_non_partisan`
- `simulating_social_media_extremist`

Output files are saved in: `outputs/simulating_social_media/` and agent configurations are stored in: `agents/simulating_social_media/`.

Each variant produces uniquely named output files for easy identification.

**Before running**, uncomment the appropriate experiment name in `simulating_social_media.py`.

Then, execute the experiment with:

```
python ./simulating_social_media.py
```
## Tweet to Persona

All files related to this section are located in the `personas` directory.

The file `persona_descriptions.csv` contains 171 persona descriptions along with their corresponding political affiliations:

- **Democrats:** 26  
- **Republicans:** 128  
- **Neutrals (Non-partisan):** 17  

In addition to the dependencies listed in `requirements.txt`, you must install more packages:

    pip install google-generativeai
    pip install openpyxl

In `persona_creation.py`, replace the placeholder `your_excel_file_here` with the path to an Excel file. The Excel file must include a column named `"text"` containing the content (e.g., tweets) to be used for persona generation.
You can use the included example file `climate_change_tweets.xls`. This file is the one used in the paper's experiments to generate personas from real-world climate change-related tweets.

> You can use any kind of text at your discretion, but this tool has only been tested with tweets.

This tool uses **Gemini Flash 2.0**, which requires an API key. Make sure your API key is set up as described in the platform’s instructions.

> ⚠️ **Note:** Google Studio AI has a rate limit of 1500 API calls per day. Since each persona requires 2 API calls, we recommend limiting the number of personas generated in a single run.

Then, to run it execute:

```
python ./persona_creation.py
```

The generated personas will be saved to `persona_descriptions.csv`.
