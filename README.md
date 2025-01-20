# Quiz Analysis and Insights Generation

This repository contains a Python-based solution for analyzing quiz data and generating insights. It processes historical and current quiz data to provide performance metrics, trends, and recommendations for improvement.

## Features

### Data Download
**Functionality:** Downloads JSON data from specified URLs and saves it locally.
- **Key Libraries:** `requests`, `json`
- **Usage:**
  ```python
  # Download JSON data from URLs
  response = requests.get(url, verify=False if "jsonkeeper.com" in url else True)
  with open(file_path, "w") as file:
      json.dump(data, file, indent=4)
  ```

---

### Data Loading and Initial Exploration
**Functionality:** Loads JSON data into memory and converts it into a pandas DataFrame for easy analysis.
- **Key Libraries:** `json`, `pandas`
- **Usage:**
  ```python
  # Load and explore data
  with open(current_quiz_endpoint_path, 'r') as file:
      current_quiz_endpoint = json.load(file)
  historical_quiz_df = pd.DataFrame(historical_quiz_data)
  ```

---

### Topic Accuracy Analysis
**Functionality:** Analyzes accuracy trends by topic from historical quiz data.
- **Key Logic:**
  ```python
  for quiz in historical_quiz_data:
      topic = quiz['quiz']['topic']
      accuracy = correct_answers / total_questions
      topic_accuracy[topic].append(accuracy)
  ```
- **Output:** Aggregated accuracies by topic.

---

### Current Quiz Performance Summary
**Functionality:** Summarizes the performance of the current quiz.
- **Key Metrics:** Total Questions, Correct Answers, Accuracy (%)
- **Usage:**
  ```python
  current_quiz_summary = {
      "Total Questions": len(current_quiz_questions),
      "Correct Answers": current_quiz_endpoint['correct_answers'],
      "Accuracy (%)": current_quiz_endpoint['accuracy']
  }
  ```

---

### Data Visualization
**Functionality:** Generates plots for historical performance trends, topic accuracies, and difficulty distribution.
- **Key Libraries:** `matplotlib`
- **Examples:**
  ```python
  plt.bar(topics, accuracies_by_topic, color='skyblue')
  plt.plot(range(len(scores)), scores, marker='o', label='Scores', color='b')
  ```

---

### Recommendations
**Functionality:** Provides targeted recommendations based on quiz analysis.
- **Logic:**
  ```python
  if weak_areas:
      recommendations.append("Focus on foundational concepts in weak areas.")
  ```
- **Output:** Suggestions for improving performance.

---

### Student Persona Definition
**Functionality:** Defines a student persona based on strengths, weaknesses, and score consistency.
- **Usage:**
  ```python
  persona = {
      "Persona Label": persona_label,
      "Strengths": strengths,
      "Weaknesses": weaknesses,
      "Score Consistency": "Consistent" if consistent else "Inconsistent"
  }
  ```
- **Output:** JSON representation of the student persona.

---

## Installation
1. Clone the repository:
   ```bash
   git clone <repository_url>
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## Usage
Run the script in a Python environment:
```bash
python script.py
```
The outputs include data summaries, visualizations, and a student persona JSON file.

---

## License
This project is licensed under the MIT License.
