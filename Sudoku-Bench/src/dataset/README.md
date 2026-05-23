---
license: mit
dataset_info:
- config_name: challenge_100
  features:
  - name: puzzle_id
    dtype: string
  - name: sudokupad_url
    dtype: string
  - name: author
    dtype: string
  - name: title
    dtype: string
  - name: rules
    dtype: string
  - name: initial_board
    dtype: string
  - name: solution
    dtype: string
  - name: rows
    dtype: int64
  - name: cols
    dtype: int64
  - name: visual_elements
    dtype: string
  - name: encoded_puzzle
    dtype: string
  splits:
  - name: test
    num_bytes: 442301
    num_examples: 100
  download_size: 233739
  dataset_size: 442301
- config_name: ctc
  features:
  - name: youtube_id
    dtype: string
  - name: sequential_number
    dtype: int64
  - name: date
    dtype: string
  - name: lgc_timestamp
    dtype: float64
  - name: puzzle_id
    dtype: string
  - name: sudokupad_url
    dtype: string
  - name: author
    dtype: string
  - name: title
    dtype: string
  - name: rules
    dtype: string
  - name: initial_board
    dtype: string
  - name: solution
    dtype: string
  - name: rows
    dtype: int64
  - name: cols
    dtype: int64
  - name: visual_elements
    dtype: string
  - name: encoded_puzzle
    dtype: string
  splits:
  - name: test
    num_bytes: 18479173
    num_examples: 2565
  download_size: 6739069
  dataset_size: 18479173
- config_name: nikoli_100
  features:
  - name: puzzle_id
    dtype: string
  - name: sudokupad_url
    dtype: string
  - name: author
    dtype: string
  - name: title
    dtype: string
  - name: rules
    dtype: string
  - name: initial_board
    dtype: string
  - name: solution
    dtype: string
  - name: rows
    dtype: int64
  - name: cols
    dtype: int64
  - name: visual_elements
    dtype: string
  - name: encoded_puzzle
    dtype: string
  splits:
  - name: test
    num_bytes: 97444
    num_examples: 100
  download_size: 73883
  dataset_size: 97444
configs:
- config_name: challenge_100
  data_files:
  - split: test
    path: challenge_100/test-*
- config_name: ctc
  data_files:
  - split: test
    path: ctc/test-*
- config_name: nikoli_100
  data_files:
  - split: test
    path: nikoli_100/test-*
---
<h1 align="center">
  <b>Sudoku-Bench</b><br>
</h1>
  
<p align="center">
  📝 <a href="https://pub.sakana.ai/sudoku">[Leaderboard]</a>
  📝 <a href="https://arxiv.org/abs/2505.16135">[Technical Report]</a>
  📝 <a href="https://sakana.ai/sudoku-bench">[Blog Post]</a><br>
  🤗 <a href="https://huggingface.co/datasets/SakanaAI/Sudoku-Bench">[Sudoku-Bench puzzle dataset]</a>
  🤗 <a href="https://huggingface.co/datasets/SakanaAI/Sudoku-CTC-Reasoning">[Sudoku-CTC-Reasoning dataset]</a>
</p>

## Sudoku-Bench puzzle dataset

The `SakanaAI/Sudoku-Bench` puzzle dataset contains three subsets:

- `challenge_100`: A collection of 100 creative Sudoku puzzles.
    - `test` split: 100 puzzles
- `nikoli_100`: A collection of 100 beautiful handmade standard Sudoku puzzles designed by Nikoli.
    - `test` split: 100 puzzles
- `ctc`: A larger collection of puzzles featured as puzzles solves in the [Cracking the Cryptic](https://www.youtube.com/c/CrackingTheCryptic) (CTC) YouTube channel.
    - `test` split: 2565 puzzles

## Subset details

### `challenge_100` subset

The purpose of the `challenge_100` subset is to evaluate the reasoning capabilities of LLMs on a diverse set of Sudokus.

The subset includes
- 15 4×4 puzzles (Sudoku variants)
- 15 6×6 puzzles (Sudoku variants)
- 50 9×9 puzzles (Sudoku variants)
- 20 9×9 puzzles (standard Sudoku) taken from the `nikoli_100` set

The selection of puzzles covers a range of difficulty. The 9×9 puzzles are roughly evenly distributed across difficulty levels 1 through 5 (using the [Logic Masters](https://logic-masters.de/Raetselportal/) difficulty scale). Around 5 puzzles are more difficult than the standard 5-star difficulty and are considered a challenge to the best human solvers. Difficulty is not a reflection of how complex the puzzle appears, and is not necessarily related to the length of the ruleset. Difficulty is a measure of how much skill and time is required for a human solver and is more closely a reflection of the depth of the idea required to find the puzzle's break-in.

The 4×4 puzzles are significantly easier and most are rated 1-star difficulty. A subset of the 4×4 puzzles are quite simple and predominately test the model's ability to understand the constraints of Sudoku variant.

Taken as a whole, the `challenge_100` includes a broad spectrum of difficulty and can be used to evaluate the performance of reasoning models of varying capabilities.

### `nikoli_100` subset

The `nikoli_100` subset contains 100 beautiful handmade standard Sudoku puzzles designed by Nikoli, the Japanese puzzle company that popularized Sudoku.

[Algorithimcally generated Sudoku puzzles](https://www.kaggle.com/datasets/rohanrao/sudoku) tend to find only puzzles of a certain type, namely whose solution path is similarly algorithmic. Human setters are more capable of creating puzzles that require deeper reasoning and creativity in the solve: see [this video](https://www.youtube.com/watch?v=mlLq8qaTLBo), for an example.

### `ctc` subset

The `ctc` subset contains 2565 puzzles featured as puzzles solves in the Cracking the Cryptic channel. The `ctc` subset can be used in conjunction with the reasoning traces in [huggingface.co/datasets/SakanaAI/Sudoku-CTC-Reasoning](https://huggingface.co/datasets/SakanaAI/Sudoku-CTC-Reasoning). That is, you may wish to use the reasoning traces together with prompts derived from the content of the puzzle being solved, which the `ctc` subset can provide.

## Puzzle details

Each puzzle in `SakanaAI/Sudoku-Bench` contains the fields:

#### Puzzle data
- `puzzle_id`: Identifier for the puzzle
- `sudokupad_url`: Link to play the puzzle on [Sudokupad](https://sudokupad.app)
- `author`: Creator of the puzzle
- `title`: Name of the puzzle
- `rules`: The puzzle rules
- `initial_board`: String representation of the starting grid (empty cells shown as '.')
- `solution`: String representation of the completed grid (81 digits for a 9×9 puzzle)
- `rows`: Number of rows in the puzzle
- `cols`: Number of columns in the puzzle
- `visual_elements`: JSON-encoded string containing detailed specifications for visual components like circles, lines, and other custom markings specific to the puzzle variant (see [Sudoku-Bench/src/sudokupad_interaction/puzzle_tools](https://github.com/SakanaAI/Sudoku-Bench/blob/main/src/sudokupad_interaction/puzzle_tools.py) for the extraction of the visual elements)
- `encoded_puzzle`: A compressed representation of the puzzle using SudokuPad's encoding scheme; for loading the puzzle directly in an offline SudokuPad (see [Sudoku-Bench/src/sudokupad_interaction/README.md](https://github.com/SakanaAI/Sudoku-Bench/blob/main/src/sudokupad_interaction/README.md))

The puzzles from the `ctc` subset contain additional fields:

#### Video metadata
- `youtube_id`: The YouTube ID of the video from which the puzzle was solved
- `sequential_number`: The index of the puzzle in the video (for videos where multiple puzzles are solved; in most cases this is 1)
- `date`: The upload date of the video
- `lgc_timestamp`: The time in seconds when the phrase "let's get cracking" is said indicating the start of the solve in the video

## Example puzzle: Parity Fish

<img width="229" alt="Image" src="https://github.com/user-attachments/assets/48820b54-78bf-47af-ad04-f64ad7a0dd13" style="float: right;"/>

The puzzle Parity Fish by Marty Sears is included in the `challenge_100` dataset.

- `puzzle_id`: `'sxsm_MartySears_580c6fdbbba9bfb0e71ae19044f02d4c'` (using SudokuPad's internal `id` field)
- `sudokupad_url`: `'https://sudokupad.app/wsj7iunsg6'` (link to the puzzle on SudokuPad)
- `author`: `'Marty Sears'`
- `title`: `'Parity Fish'`
- `rules`: `'Normal sudoku rules apply; fill the grid with the digits 1-9 so that digits don\'t repeat in any row, column, and marked 3x3 box.\\nTwo cells adjacent along a red line must contain one even digit and one odd digit.\\nTwo cells connected by a white dot contain consecutive digits.\\nTwo cells connected by a black dot contain digits where one is double the other.',`
- `initial_board`: `'.................................................................................'` (empty cells are represented as `.`)
- `solution`: `'854369172976251834123478956419582367568937421237146598785694213691823745342715689'`
- `rows`: `9`
- `cols`: `9`

### Visual elements

The `visual_elements` field is a JSON-encoded string containing detailed specifications for visual components of the puzzle. In the Parity Fish puzzle, there are 24 visual elements: 5 black dots, 16 white dots, and 3 red lines. You can display the visual elements using the `pretty_print_visual_elements` function in [`src/eval.utils`](https://github.com/SakanaAI/Sudoku-Bench/blob/main/src/eval/utils.py) in the [SakanaAI/Sudoku-Bench](https://github.com/SakanaAI/Sudoku-Bench) repo

```python
import datasets
import json
from eval.utils import pretty_print_visual_elements

puzzle = datasets.load_dataset("SakanaAI/Sudoku-Bench", "challenge_100")['test'][23]  # Parity Fish puzzle
print(pretty_print_visual_elements(json.loads(puzzle['visual_elements'])))
# - shape: circle, color: white (stroke color: black), location: between r4c8 and r4c9
# - shape: circle, color: white (stroke color: black), location: between r5c8 and r5c9
# - shape: circle, color: white (stroke color: black), location: between r6c8 and r6c9
# - shape: circle, color: white (stroke color: black), location: between r5c1 and r5c2
# - shape: circle, color: white (stroke color: black), location: between r8c3 and r9c3
# - shape: circle, color: white (stroke color: black), location: between r7c1 and r8c1
# - shape: circle, color: white (stroke color: black), location: between r1c1 and r2c1
# - shape: circle, color: white (stroke color: black), location: between r7c7 and r7c8
# - shape: circle, color: white (stroke color: black), location: between r7c1 and r7c2
# - shape: circle, color: white (stroke color: black), location: between r9c8 and r9c9
# - shape: circle, color: white (stroke color: black), location: between r8c5 and r8c6
# - shape: circle, color: white (stroke color: black), location: between r1c4 and r2c4
# - shape: circle, color: white (stroke color: black), location: between r7c6 and r8c6
# - shape: circle, color: white (stroke color: black), location: between r2c7 and r3c7
# - shape: circle, color: white (stroke color: black), location: between r1c2 and r1c3
# - shape: circle, color: white (stroke color: black), location: between r1c5 and r2c5
# - shape: circle, color: black, location: between r3c2 and r4c2
# - shape: circle, color: black, location: between r4c7 and r4c8
# - shape: circle, color: black, location: between r2c3 and r3c3
# - shape: circle, color: black, location: between r9c2 and r9c3
# - shape: circle, color: black, location: between r8c8 and r9c8
# - line, color: red, coords: r3c2, r3c3, r3c4, r3c5, r3c6, r4c7, r5c8, r6c7, r7c6, r7c5, r7c4, r7c3, r7c2
# - line, color: red, coords: r4c1, r4c2, r5c3, r6c4, r7c4
# - line, color: red, coords: r6c1, r6c2, r5c3, r4c4, r3c5
```

The intermediate `json.loads(puzzle['visual_elements']))` is a list of dictionaries, each of which is a verbose description extracted from the SudokuPad rendering engine. We encourage the user to adopt their own `pretty_print_visual_elements` function to display the visual elements in a way that is most useful for their application.

Please see [`src/sudokupad_interaction/puzzle_tools`](https://github.com/SakanaAI/Sudoku-Bench/blob/main/src/sudokupad_interaction/puzzle_tools.py) for more details on the `visual_elements` field.

### Encoded puzzle

The `encoded_puzzle` field is a byte64 encoding of the puzzle using SudokuPad's internal encoding method.

The `encoded_puzzle` field can be used to obtain an alternate URL for the puzzle. Namely, `https://sudokupad.app/wsj7iunsg6` and [`https://sudokupad.app/{parity fish's encoded_puzzle string}`](https://sudokupad.app/sclN4SwJgXA5AzgHjAtgfQLIEMBOAXAngZQFMsZkBWADgAYBjANgDMwAjV9ATmYeasIHYAjOkID2VACziGVAExhxNKABpEhbOjDp1EYDAD2AV0w1C0fAbB6A1gYAEGK4Uy2AbjNlkAdLM8zxAWhoaBjJ0CjpldANsAAs9TGgMHFxbIhJlTAMAG0IYaAA5eMR0LNsYC2s7TJyYW3QAB3qs3ABuWwYQLNLYwlsAc0xwWwB3EFjbHtswED6x2oF/djK9CZitKZm5qb0AOwAdKGxbTEJ64iOQHbqdlMw9YaVbGj0sg0Qdx/QdsFtizEcfgBmOCA2zMPRwTx7HYAFWGKxMXVqGgAVugTDsjiVdn06sdCD8spdeogDDAjs9MehLrZdr1CC5CFdprMsd9aTtenowD8WWMobD4U9CEinrtOTRsASwSl0CMYmNepYKbt1DTKTBCDRoiBGRtWTABXCESKsrVKRKpT9mLKwVl0VZtiqqTS+dhasMYk4uZzbCBapYDMwcqsuT1MJ5lPpXtgQLtoBQyOJAXR2AI+DJ2Hw6DIyAIKIDxAIZIW+BR2GQ6EWKxQS3Q+JXy4C+OIZMXmwJxHQyOwKGXK+xWwIU2na83xGRCzJBI32MpmLNin1TFAYthsPU8gB6LcgTwgRB9IyeZ6ILc7QEgADy2HE+U8KLOfXni/Qy709XRY1wEAESmw0AAApYN+tgAGL+jEUAAL5KCYEAANoIUoKGoShAC6SjIWhqGYdhOFKHhBEYVhxGEaRxFEZRFEEVRtGYSciFIVQShUHhLECOxSgyHhf5sVhf6cQJ3F4TIrGiUoQkIWJPF4QhLGAlx4hcWQvFKIpwnKcJqlYWJGnSUoWkGapcksXQXF8FxFBqeZwmWcJ1m6UotkGfZBnWXJgLiVhXlSV5PFYeI3kIUFUlBQFCFkMFUVSVFslYQhXn6V5RleTpIXqXhQVGUF6VRfpUVGVFJkJV5LleW5XmORlLlBW5QXVVFLlRW5UUeQldDBZ1UmdRFfDBf1Un9RFFDBaNUmjfFSGdfpnVGZ16X9fp/VGf16Wjfpo1GaNJXTc5eGdW5nXVf1Ln9W5/XVaNLmjW5o0eZheiIcAkqIYCnhtZhwwQFQniFkoMQ/X9QWxL+vijVK0DKDQEAAMQsQk2BwTIcNgXBAhw1QsEvQBIUfUojnfb9/2A8TIOAwI4P/iu0OY0oiPI6j6OY9jr2RfjhNAyTXPk2DMgQzTcF0wzNAo7DaM0Bj8Os7j4j40JRPAwDPP/hTVOQ1AtPw/TEBI6LTOSyzSg44hk0fV9Kuk0roOU/z1NQ0L2si2LEtS1jxts/1v06Yr3Nk6rfMCw7MNO7rjPi8z0se7jfHm0ovtBVb/02+rgshwjYf6xHhtRybCF0Pj9kJ8r/sp3bGtaxnesu5H7t5wXMUW/7Se87bQea47Vfh67Rt5xQHNN0rLcB239sd+nOvVwbbsy4hfD4z7lsq2X7eV5P3e17PCF/u9i/N8vavl2nwuZzXOd157SheHvQ8H4HY9r870+92zYkN4PfvW4fq+d+vWc97nNm3sRLxyXqXb+D9f5P2zjPaOiE/xyxvp/ZOECK5QNPs/QBuNfJx19l5JOXk0EhzRtAi+2DC4f3wVzQhx8I6kK3jJXB1CS5/RocHJm9C4EIX7nFShLDARsPHhwjBWDTZKHnkgqhxNBFaxISIrG6FoJAA) will load the same puzzle. Both URLs point to Sven's SudokuPad website. However, only the second method works when running SudokuPad locally and avoids a call to the SudokuPad puzzle database. To ensure longevity of the benchmark, we provide a local usage in [`src/sudokupad_interaction`](https://github.com/SakanaAI/Sudoku-Bench/tree/main/src/sudokupad_interaction).

The `encoded_puzzle` field can be ignored if using the text-only approach outlined in `src.eval` in this repo as all relevant information has already been extracted.

## Puzzle edge cases

Because of the wide array of puzzles solved, the `ctc` subset is provided "as-is". There are a number of edge cases that make a pure text representation of the puzzle incomplete:
1. Some puzzles have visual elements that are difficult to encode in the `visual_elements` field (see below for a description of the `visual_elements` field). For example, the delightful [RatRun puzzles](https://www.youtube.com/watch?v=-KXjRMkYpA4) will not have a coherent textual description of the visual elements due to the visual complexity of the puzzle.
2. Other puzzles have the `solution` field omitted as many puzzle setters choose not to disclose the solution in SudokuPad.
3. A popular recent trend is the use of fog-of-war in Sudoku puzzles. For such puzzles, all hidden elements will be exposed in the `visual_elements` field meaning the puzzle will not be presented as intended by the puzzle setter.

Please consider filtering the `ctc` subset based on your needs.

## Citation
```bibtex
@misc{seely2025sudoku-bench,
  title={{Sudoku-Bench}},
  author={Seely, Jeffrey and Imajuku, Yuki and Zhao, Tianyu and Cetin, Edoardo and Jones, Llion},
  howpublished = {\url{https://github.com/SakanaAI/Sudoku-Bench}},
  year={2025}
}
```
