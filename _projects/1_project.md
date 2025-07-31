---
layout: page
title: Trajectory Prediction
description: Deep learning-based trajectory prediction using Agroverse 2 dataset.
img: assets/img/trajectory-bg.jpg
importance: 1
category: work
---

This project was built as part of the **Trajectory Prediction Challenge** using the [Argoverse 2 Motion Forecasting Dataset](https://www.argoverse.org/av2.html). The competition focused on developing models capable of accurately predicting the future trajectories of diverse road agents (vehicles, pedestrians, cyclists, buses, motorcycles, etc.) in complex, real-world driving scenarios.

We used a modified version of Argoverse 2, with each scenario containing **11 seconds of bird's-eye-view data** sampled at **10Hz**, including agent centroid and heading. The model predicts future trajectories in challenging urban environments with long-range interactions and social complexity.

[🔗 View the code on GitHub](https://github.com/hero1601/trajectory-prediction)

---

### Project Goals

- Develop an accurate, generalizable motion forecasting model.
- Handle rare events, non-linear motion, and interaction-heavy scenes.
- Contribute to safe and interpretable **autonomous vehicle planning**.

---

### Dataset

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/input_heatmap.png" title="Input Dataset Visualization" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/output_heatmap.png" title="Output Dataset Visualization" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Visualization of trajectories in the Agroverse 2 dataset.
</div>

- **Dataset**: Argoverse 2 Motion Forecasting (Modified)
- **Scenarios**: 11s per agent, sampled at 10Hz
- **Agents**: Buses, motorcycles, pedestrians, cars, etc.
- **Features**:
  - Bird's-eye-view positions (x, y) and heading
  - Social and temporal context
  - Long-range prediction targets
  - Multi-modal output

---

### Model Overview

We designed a custom LSTM-based architecture that:

- **Encodes** each agent’s trajectory with an LSTM
- **Pools** surrounding agents using a **learned attention mechanism**
- **Combines** ego and social context features
- **Predicts** the entire 60-step trajectory in one forward pass

This approach proved to be more interpretable and stable than Transformer-based baselines, especially under limited compute.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/model-diagram.png" title="Model Architecture" class="img-fluid rounded z-depth-1 w-50" %}
  </div>
</div>
<div class="caption" style="text-align: center">
  Our best-performing model encodes temporal and social context to predict future motion.
</div>

---

### Experiments & Results

We evaluated multiple baselines:

- **Linear Regression** — poor generalization
- **MLP** — handled nonlinearities but lacked temporal awareness
- **LSTM** — strong performance on ego-only data
- **SocialLSTM** — added multi-agent context
- **My Model** — achieved **best performance** via attention and feature augmentation

<table>
  <thead>
    <tr>
      <th>Model Variant</th><th>Validation MSE</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Full Model (w/ attention, features)</td><td>7.7383</td></tr>
    <tr><td>Without Normalization</td><td>423.1483</td></tr>
    <tr><td>Without Attention</td><td>8.6116</td></tr>
    <tr><td>Without Augmentation</td><td>9.5708</td></tr>
    <tr><td>Without Speed/Acceleration</td><td>8.1191</td></tr>
  </tbody>
</table>

**Final metrics**:
- **MAE**: 1.2879
- **MSE**: 7.7383

---

### Predictions

After training the model, the final validation mean absolute error (MAE) was 1.2879, validation mean
squared error (MSE) was 7.7383, and validation normalized MSE was 0.1579. These metrics indicate that the model performs well on the validation set and is likely to generalize effectively to unseen data.

On Looking at the qualitative results of the models, it was observed that the model’s accuracy will vary depending on the nature of the ground truth trajectory. When the trajectory is a linear path such as Sample 1701 (shown in Figure), the model predicts it very accurately. However, when the ground truth trajectory involves more erratic or complex behavior, such as suddenly turning or stopping, as shown in Samples 49, 1368, and 1043, the model is much less accurate in its prediction.

<div class="row">
  <div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/prediction.png" title="Prediction" class="img-fluid rounded z-depth-1 w-75"%}
  </div>
</div>
<div class="caption" style="text-align: center">
  Visualizations of predicted trajectories (in red) compared to ground truth paths (in blue) on test sequences.
</div>

---

### Key Takeaways

- **Normalization** around the ego vehicle is essential for generalization.
- **Social context** improves prediction quality, especially in crowded or interactive scenes.
- **Attention mechanisms** outperform rigid social pooling.
- **Feature engineering** (e.g., speed & acceleration) meaningfully boosts performance.

---

