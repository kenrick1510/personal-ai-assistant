# Prompt experiments

This is my experiment log for Project 1, Milestone 2.

## How to run an experiment

1. Open `experiment.py`.
2. Paste your current system prompt into `PROMPT_A`.
3. Paste it again into `PROMPT_B`, then change ONE thing.
4. Put two or three test messages in `TEST_INPUTS`.
5. In the terminal, run: `python experiment.py`
6. Read the replies. Each prompt answers each message three times.
7. Fill in one experiment below.
8. If B was better, B becomes your new `PROMPT_A` for the next experiment.

When all three experiments are done:

1. Copy your winning prompt into `SYSTEM_PROMPT` in `streamlit_app.py`.
2. Commit your changes.
3. Click Sync. Commit alone does not update your live app.
4. Open your live URL and check that the assistant uses the new prompt.

Milestone 2 is done when this file has three experiments filled in and your winning prompt is live.

---

## Experiment 1: instructions

**The one thing I changed:**

SYSTEM_PROMPT_B = """You generate sample test data for a gaming inventory system.
Generate realistic fictional gaming records containing console, genre, and player mode."""

**Test messages I used:**
"Generate a sample gaming dataset."

"Generate three RPG gaming records."

"Generate sample multiplayer gaming records."

**What happened across the runs:**
Across the three runs for each test message, Prompt A generated a wide variety of datasets, including player telemetry, character statistics, matchmaking information, and inventory items. Although the responses were relevant to gaming, they did not consistently focus on game records or include the fields I wanted.

In comparison, Prompt B consistently generated records containing console, genre, and player mode. For example, when asked to generate three RPG records, Prompt B produced fictional game titles with different RPG genres, consoles, and player modes. However, the output formatting still varied between tables, JSON, and bullet points, and some responses included additional information beyond the requested fields

**Keep or revert, and why:**
I decided to keep Prompt B because the additional instructions improved the relevance and consistency of the generated data across the runs. The model followed the intended gaming inventory structure more closely instead of generating unrelated gaming statistics. However, the inconsistent output formatting suggests that further improvements are needed, particularly by providing examples and defining output constraints in the next experiments.

---

## Experiment 2: examples

**The one thing I changed:**
I added an example JSON record to SYSTEM_PROMPT_B showing the expected structure with three fields: console, genre, and player_mode. This experiment tested whether one-shot prompting would help the model generate more consistent gaming records

**Test messages I used:**
"Generate a sample gaming dataset."

"Generate three RPG gaming records."

"Generate sample multiplayer gaming records."

**What happened across the runs:**
Prompt A generated relevant gaming records containing console, genre, and player mode, but the formatting varied between JSON, tables, and bullet points. It also included additional fields such as game titles, inventory status, and completion percentages.

In comparison, Prompt B followed the example more closely. When asked to generate three RPG records, it consistently returned JSON arrays containing the three specified fields across all three runs. For the general gaming dataset, it also produced JSON arrays in all three runs instead of switching between different formats.

However, I noticed that Prompt B sometimes included explanations before the JSON output. In one multiplayer test, it also generated malformed JSON with missing field names. This showed that providing an example improved consistency but did not guarantee valid JSON every time.

**Keep or revert, and why:**
I decided to keep Prompt B because the example improved the consistency of the generated records and helped the model follow the intended structure. Compared with Prompt A, the responses were more predictable and contained fewer unnecessary fields.

However, some responses still included additional explanations or formatting errors. For Experiment 3, I will test whether adding explicit output constraints can make the generated JSON more reliable and suitable for use in a gaming inventory system.
---

## Experiment 3: output constraints

**The one thing I changed:**
exactly three fields: console, genre, and player_mode. I also specified that multiple records should be returned as a JSON array without additional explanations or Markdown formatting
**Test messages I used:**
"Generate a sample gaming dataset."

"Generate three RPG gaming records."

"Generate sample multiplayer gaming records."
**What happened across the runs:**
Prompt A generally followed the example from Experiment 2 and generated records containing the three required fields. However, some responses still included introductory explanations and Markdown code blocks. For example, when generating a general gaming dataset, Prompt A introduced the data with a description before displaying the JSON.

In comparison, Prompt B consistently returned JSON arrays without additional explanations or Markdown formatting across all nine runs. When asked to generate three RPG records, it produced exactly three records, each containing the required fields. The multiplayer tests also produced structured records with appropriate player modes, such as online multiplayer, local co-op, and competitive multiplayer.

However, the number of records still varied when the user did not specify an exact quantity. For example, the multiplayer responses contained different numbers of records across the three runs.
**Keep or revert, and why:**
I decided to keep Prompt B because the output constraints improved the consistency and predictability of the generated data. Unlike Prompt A, Prompt B followed the requested JSON-only format without adding unnecessary text.

This makes the output more suitable for integration into a gaming inventory system because it can be processed programmatically without first removing explanations or Markdown formatting.

Overall, this experiment showed that combining clear instructions, an example, and explicit output constraints produced the most consistent results across the three experiments.
---

## My winning system prompt

```
Prompt B from Experiment 3 is your winning system prompt. You can copy it into SYSTEM_PROMPT in streamlit_app.py and into the My winning system prompt section of experiments.md.

One limitation: the experiment output supports that B consistently followed the JSON-only presentation format, but the log does not show a separate automated JSON validation test.
```
