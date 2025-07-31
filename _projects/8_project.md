---
layout: page
title: Clarifying Questions in Open-Domain Dialogue
description: Machine learning techniques for detecting and generating clarifying questions with ClariQ benchmark.
img: assets/img/clarifying-bg.jpg
importance: 1
category: work
---

This project explores how conversational AI systems can proactively ask clarifying questions when faced with ambiguous user input. Our goal is to make dialogue agents more robust and user-friendly, particularly in open-domain, information-seeking conversations.

[🔗 View the code on GitHub](https://github.com/ritikalath/NLP_TeamRAMA)

---

## Introduction

Users often struggle to articulate complex needs in a single query, causing frustration and repeated reformulations. By **detecting ambiguity** and asking targeted clarifying questions, our system improves both understanding and user satisfaction.

A conversational system's primary aim is to provide helpful answers to user requests. However, when faced with ambiguous queries, it's better for the system to *ask clarifying questions* rather than risk an incorrect response.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/clarification_examples.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

---

## Related Work

Our work combines advances in:
- **Clarifying question generation** ([Aliannejadi et al., 2019][1])
- **Dialogue system evaluation**, covering both task-oriented and open-domain settings

---

## Task Design

- **Ambiguity Scoring:** Each user request receives a score (1–4) signifying the need for clarification.
- **Clarifying Question Retrieval:** The system selects the most relevant clarifying questions for ambiguous inputs.
- **User Answers:** For every clarifying question, sample user answers simulate real dialogues.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/system_architecture.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

**Tasks:**
1. *Classification*: Predict if (and how urgently) a clarification is needed for a given user query.
2. *Retrieval*: For ambiguous queries, return a ranked list of clarifying questions.

---

## Dataset

- **ClariQ Dataset:** A benchmark collection for exploring clarifying questions in conversational search. It includes user requests ranging from clear to highly ambiguous, with each request annotated for clarification need.

- **Ambiguity Labels:** Requests are rated on a scale from 1 (clear) to 4 (very ambiguous), guiding models on when to ask clarifying questions.

- **Clarifying Questions and Answers:** For ambiguous queries, a pool of clarifying questions is provided along with sample user answers, enabling multi-turn dialogue modeling.

- **Document Collections:** Optionally, associated web documents enable evaluation of how clarifications improve downstream search quality.

This dataset supports training and evaluating models that detect ambiguity and generate or retrieve effective clarifying questions for better user interaction.

---

## Methods

#### A. Classification

We treat “when to ask clarifying questions?” as a multi-class classification task, using transformer models:

- Models used: BERT, RoBERTa, DeBERTa, ELECTRA
- Best result: ELECTRA gave highest F1, RoBERTa gave top accuracy.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/classification_result.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

#### B. Retrieval

“How to select the clarifying question?” We explore two retrieval strategies:

1. **BM25 + Transformer Re-ranker:** Retrieve top-N candidates, re-rank with BERT-family models.
2. **Full Bank Ranking:** Direct transformer ranking over the entire question bank.

- Evaluation: Recall@k for question relevance; MRR, Precision@k, nDCG for document relevance.

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/ques-relevance.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/doc-relevance.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

---

## Results

- **Classification:** ELECTRA achieved the best F1; RoBERTa achieved top accuracy for clarity detection.
- **Retrieval:** 
  - *Re-ranking*: BERT performed best for question recall.
  - *Full ranking*: ELECTRA was strongest overall, especially for large banks.
  - *Document relevance*: RoBERTa achieved the best document retrieval scores.

---

## Conclusion

Our system reliably detects ambiguity and suggests useful clarifying questions—**measurably improving search and dialogue quality** on the ClariQ benchmark. Insights:
- Attention-based transformers (ELECTRA, RoBERTa) excel at both detecting and resolving ambiguity.
- Re-ranking boosts Recall@k compared to traditional IR systems.
- Asking clarifying questions improves downstream results in open-domain dialogue.

---

[1]: https://doi.org/10.1145/3331184.3331265

