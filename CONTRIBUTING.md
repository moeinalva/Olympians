# Contributing

Thank you for improving Olympians.

## Before you begin

- Keep the notebook runnable from a clean Python environment.
- Preserve Persian datasets, prompts, and answers when they are required for the project behavior.
- Do not add evaluation questions to the few-shot examples.
- Never commit API keys, credentials, or local environment files.

## Making a change

1. Create a focused branch.
2. Update the notebook or data with the smallest necessary change.
3. Run the affected notebook cells with your own Cohere API key when practical.
4. Verify that generated submissions contain one `answer` column with the expected number of rows.
5. Describe the motivation, behavior change, and validation in your pull request.

## Data changes

Changes to `gods.json`, `questions.csv`, or `examples.csv` can alter evaluation behavior. Explain the source and intended effect of every dataset change in the pull request.
