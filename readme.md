# AMD AI Premier League (AAIPL) - Hackathon
at IIT DELHI
## Overview

This project implements two AI agents for a competitive question-and-answer tournament:
- **Q-Agent**: Generates puzzle-based questions
- **A-Agent**: Answers those questions

---

## Quick Start

### 1. Environment Setup

```bash
# Clone or navigate to your project directory
cd AAIPL

# Install dependencies (if needed)
pip install -r requirements.txt
```

### 2. Run Q-Agent (Generate Questions)

```bash
python -m agents.question_agent \
  --output_file "outputs/questions.json" \
  --num_questions 20 \
  --verbose
```

**Output**: `outputs/questions.json`

### 3. Run A-Agent (Answer Questions)

```bash
python -m agents.answer_agent \
  --input_file "outputs/filtered_questions.json" \
  --output_file "outputs/answers.json" \
  --verbose
```

**Output**: `outputs/answers.json`

---

## Project Structure

```
AAIPL/
├── agents/
│   ├── question_model.py          # Q-Agent model (edit this)
│   ├── question_agent.py          # Q-Agent runner
│   ├── answer_model.py            # A-Agent model (edit this)
│   └── answer_agent.py            # A-Agent runner
├── assets/
│   ├── topics.json                # Available topics
│   ├── topics_example.json        # Example questions
│   ├── sample_question.json       # Expected Q format
│   └── sample_answer.json         # Expected A format
├── utils/
│   └── build_prompt.py            # Prompt utilities
├── outputs/
│   ├── questions.json             # Generated questions
│   ├── filtered_questions.json    # Validated questions
│   ├── answers.json               # Generated answers
│   └── filtered_answers.json      # Validated answers
├── qgen.yaml                      # Q-Agent config
├── agen.yaml                      # A-Agent config
├── tutorial.ipynb                 # Training guide
└── README.md                      # Full documentation
```

---

## Key Files to Modify

### `agents/question_model.py`
Implement your Q-Agent model here. Must return questions in JSON format:

```json
{
  "topic": "Logical Reasoning",
  "question": "Your question here?",
  "choices": ["A) Option 1", "B) Option 2", "C) Option 3", "D) Option 4"],
  "answer": "A",
  "explanation": "Brief explanation (optional)"
}
```

### `agents/answer_model.py`
Implement your A-Agent model here. Must return answers in JSON format:

```json
{
  "answer": "A",
  "reasoning": "Brief reasoning (optional)"
}
```

---

## Question Topics

Your Q-Agent must generate questions from these topics:

1. **Logical Reasoning** - Syllogisms
2. **Puzzles** - Seating Arrangements (Linear, Circular)
3. **Blood Relations & Family Tree** - Generation-based logic
4. **Alphanumeric Series** - Mixed series questions

See `assets/topics_example.json` for examples.

---

## Configuration Files

### `qgen.yaml` - Question Generation Config
- `max_tokens`: Max tokens for questions (don't exceed)
- Model parameters and generation settings

### `agen.yaml` - Answer Generation Config
- `max_tokens`: Max tokens for answers (don't exceed)
- Model parameters and generation settings

---

## Scoring

**A-Agent Score** = (Correct Answers / Total Questions) × 100

**Q-Agent Score** = (Incorrect Answers by Opponent / Total Questions) × 100

---

## Constraints

| Constraint | Limit |
|-----------|-------|
| Question generation time | < 13 seconds per question |
| Answer generation time | < 9 seconds per answer |
| Minimum format compliance | ≥ 50% of questions |
| Language | English only |
| External models | Not allowed |
| RAG techniques | Not allowed |

---

## Validation Checklist

- [ ] Questions follow JSON format with all required fields
- [ ] Answers follow JSON format with required "answer" field
- [ ] All questions pertain to specified topics
- [ ] Model checkpoints load correctly
- [ ] Output files generate without errors
- [ ] Code is pushed to GitHub (except `hf_models/`)
- [ ] No hardcoding or RAG techniques used

---

## Testing Your Agents

### Test Q-Agent output:
```python
import json

with open("outputs/questions.json", "r") as f:
    questions = json.load(f)

print(f"Generated {len(questions)} questions")
print(f"First question: {questions[0]}")
```

### Test A-Agent output:
```python
import json

with open("outputs/answers.json", "r") as f:
    answers = json.load(f)

print(f"Generated {len(answers)} answers")
print(f"First answer: {answers[0]}")
```

---

## Debugging Tips

1. **Check logs**: Run with `--verbose` flag for detailed output
2. **Validate JSON**: Use `json.tool` to check format
3. **Token counts**: Monitor token usage in configuration files
4. **Response time**: Track generation speed for each question/answer

---

## Submission Requirements

- [ ] All code in `AAIPL/` folder
- [ ] Model checkpoints in `AAIPL/hf_models/` (copied from read-only cache)
- [ ] Agents callable via `python -m agents.question_agent` and `python -m agents.answer_agent`
- [ ] Outputs generate to `outputs/questions.json` and `outputs/answers.json`
- [ ] Code pushed to GitHub before deadline
- [ ] No modifications to original model files in `/root/.cache/`

---

## Resources

- **Full Documentation**: See `README.md`
- **Training Guide**: `tutorial.ipynb`
- **Sample Questions**: `assets/topics_example.json`
- **Format Specs**: `assets/sample_question.json` & `assets/sample_answer.json`

---

## Support

For questions or clarifications, reach out on Discord or check the full README.md.

Good luck! 🚀
