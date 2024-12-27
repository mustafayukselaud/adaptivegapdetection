# Adaptive Gap Detection Task (Web Implementation)

This repository implements an adaptive gap detection task using **jsPsych** for web-based psychoacoustic experiments. Participants complete a gap detection task using a two-alternative forced-choice (2AFC) paradigm, with stimuli presented as sequences of sounds.

---

## Features

- **Adaptive Procedure**: Implements a staircase procedure for determining gap detection thresholds.
- **Custom Stimuli**: Allows flexible stimulus configurations (noise bursts, tones, etc.).
- **Web-Based**: Deployable on any web server; participants can perform the task using a browser.

---

## How to Set Up and Run the Experiment

1. Clone the repository:
   ```bash
   git clone https://github.com/mustafayukselaud/adaptivegapdetection.git
   cd adaptivegapdetection
   ```

2. Host the experiment on a local or remote web server. Examples:
   - Use Python's HTTP server:
     ```bash
     python -m http.server
     ```
   - Or deploy using GitHub Pages or another web hosting service.

3. Open the `NoiseNoise.html` file in a browser. This file contains the main entry point for running the experiment.

---

## Dependencies

- **jsPsych**: A JavaScript library for creating behavioral experiments.
- **jspsych-audio-sequence-button-response.js**: A custom plugin for playing audio sequences and recording responses.
- **jspsych-nafc-adaptive.js**: A custom plugin for the n-alternative forced-choice adaptive procedure, developed by Etienne Gaudrain - https://github.com/egaudrain

These plugins are included in the repository.

---

## How It Works

1. **Stimuli Presentation**:
   - The experiment plays sequences of noise bursts separated by varying gap durations.
   - Participants identify which interval contained a detectable gap.

2. **Adaptive Threshold Estimation**:
   - The experiment uses an adaptive staircase procedure to adjust gap durations based on participants' responses.
   - Thresholds are calculated after a predefined number of trials.

3. **Output**:
   - Results, including gap thresholds and response accuracy, are saved locally or sent to a backend server (if configured).

---

## Example Configuration

### NoiseNoise.html

```html
<!DOCTYPE html>
<html>
<head>
  <script src="jspsych.js"></script>
  <script src="jspsych-audio-sequence-button-response.js"></script>
  <script src="jspsych-nafc-adaptive.js"></script>
</head>
<body>
  <script>
    const timeline = [];

    // Example configuration
    const trial = {
      type: 'jspsych-audio-sequence-button-response',
      stimulus: [['noise1.wav', 'noise2.wav']],
      choices: ['1st', '2nd'],
      gap_duration: 0.02, // Initial gap duration in seconds
      correct_choice: 0, // Index of correct response
    };

    timeline.push(trial);

    jsPsych.init({
      timeline: timeline,
      on_finish: function() {
        jsPsych.data.displayData(); // Show results at the end
      }
    });
  </script>
</body>
</html>
```

### Adaptive Settings in `jspsych-nafc-adaptive.js`

The `jspsych-nafc-adaptive.js` plugin adjusts gap durations dynamically based on the participant's responses. Modify the staircase parameters as needed in the plugin code:
```javascript
const staircaseParams = {
  stepSize: 0.005, // Change in gap duration
  maxReversals: 8, // Maximum reversals before ending
  trialsPerLevel: 3, // Trials per difficulty level
};
```

---

## Minimal Reproducible Example

To test the setup with default parameters:
1. Start a web server in the repository directory.
2. Open `NoiseNoise.html` in your browser.
3. Follow the instructions displayed on the screen.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Contact

For questions or collaborations, contact Mustafa Yüksel at mustafa.yukselaud@ankaramedipol.edu.tr
