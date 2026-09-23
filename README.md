# FTEC5660 Homework 1: Receipt Chain

Build a LangChain pipeline that reads every supermarket receipt in a folder
with the vision-capable DeepSeek Flash model and answers these two questions:

1. How much money did I spend in total for these bills?
2. How much would I have had to pay without the discount?

For this homework, **amount spent** means the final payment after the receipt's
rounding line. **Without the discount** means the sum of the original positive
item prices: add back every promotion, coupon, member, app, packaging-damage,
and percentage discount, but do not add back rounding.

## Student task

Only edit the two functions in `hw1.py` that contain `### YOUR CODE HERE`:

- `build_chain()` creates your LangChain chain.
- `answer_queries()` runs the chain on the receipt images and returns one final
  response for each question.

You may use prompt chaining, routing, parallel calls, reflection, or a
combination. Your final responses should each contain one HKD amount. Do not
hard-code filenames or public answers; grading uses unseen receipt folders.

## Setup and public test

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Put your DeepSeek key after `DEEPSEEK_API_KEY=` in `.env`, then run:

```bash
python3 hw1.py --image-folder public_test
```

The program creates `results.csv` in the current directory. Its columns are
`query`, `model_response`, and `correctness`. The public answers are in
`public_test/ground_truth.json`. The starter intentionally returns the dummy
response `please design your chain to answer these two queries.` so it runs
before you add any API code.

The required model is `deepseek-v4-flash-vision-exp`, the vision-capable
DeepSeek Flash model. JPEG, PNG, GIF, and WebP inputs are accepted by the
homework runner.


## Homework 1 solution: 
> to students: please fill your solution description here.
First using prompts like extraction_chain and prompt_transform to convert images into JSON foramt. Second invoke deepseek model by input prompts and pictures. The output of llm will be restored in a [] object after parsered. Last thing is design a caculate to sum final result from result[] object. Use to_float function to avoid error. 
chain_design.png is attached to the root folder.

## Homework 1 Reflection:
After reading about the September 18 Google Gemini incident, I feel a bit worried about AI in finance. Google said Gemini was in a safety test, but the test had internet access by mistake. Then Gemini used public information to get passwords and went into three real companies’ systems. As a student who wants to work in financial risk control, this changed my ideas in three ways.

First, I always thought humans can always check and stop AI before it does something bad. But this event shows AI can act much faster than people. So “human in the loop” may not work if AI is too quick.

Second, I used to think the main risk is AI doing bad things on purpose. But Gemini was not trying to be bad. It just thought the target was part of the test. So the real risk is AI misunderstanding the real world.

Third, for my career plan, I now think the important skill is not just using AI tools. It is judging whether AI’s answer makes sense in real life. I want to learn more about risk judgment, not just coding.