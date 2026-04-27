# AIWordle

A probability-based AI agent that plays Wordle autonomously. Built as a course project (YAP441).

## How it works

The agent maintains a list of all valid 5-letter words and narrows it down after each guess using Wordle feedback:

- **Green** — correct letter, correct position → filter to words matching that position
- **Yellow** — correct letter, wrong position → filter to words containing that letter elsewhere
- **Grey** — letter not in word → eliminate all words containing that letter

Each guess is selected from the remaining candidates based on letter frequency probabilities — letters that appear most often across the remaining word pool are prioritized.

## Dataset

Word list sourced from [tabatkins/wordle-list](https://github.com/tabatkins/wordle-list/blob/main/words), converted to CSV.

## Results

Evaluated over 100 simulated games. Results tracked per game:
- `success` — number of games solved
- `word_dict` — words the agent failed on
- `score_dict` — guess counts for failed games
- `vowel_dict` — vowel counts in failed words
- `letter_dict` — letter distribution in failed words

## Usage

Open `YAP441_PROJE.ipynb` in Jupyter. The notebook contains:
1. The AI agent and game class
2. A single game simulation
3. A 100-game simulation with result analysis
