Raise your hand to enter "Violent" mode
```
// Classifier Variable
  let classifier;
  // Model URL
  let imageModelURL = 'https://teachablemachine.withgoogle.com/models/2qDsm85md/';
  
  // Video
  let video;
  let flippedVideo;
  // To store the classification
  let label = "";

  // Load the model first
  function preload() {
    classifier = ml5.imageClassifier(imageModelURL + 'model.json');
  }

  function setup() {
    createCanvas(320, 260);
    // Create the video
    video = createCapture(VIDEO);
    video.size(320, 240);
    video.hide();

    flippedVideo = ml5.flipImage(video);
    // Start classifying
    classifyVideo();
  }

  function draw() {
    background(0);
    // Draw the video
    image(flippedVideo, 0, 0);

    if (label == "Class 1")
        {
      // Draw the label
      fill(255);
      textSize(16);
      textAlign(CENTER);
      text("Peace", width / 2, height - 4);
      noTint();
      }
    else if(label == "Class 2")
      {
      // Draw the label
      fill(255);
      textSize(16);
      textAlign(CENTER);
      text("Violence", width / 2, height - 4);
      tint(204, 0, 0);
      }
  }

  // Get a prediction for the current video frame
  function classifyVideo() {
    flippedVideo = ml5.flipImage(video)
    classifier.classify(flippedVideo, gotResult);
    flippedVideo.remove();

  }

  // When we get a result
  function gotResult(error, results) {
    // If there is an error
    if (error) {
      console.error(error);
      return;
    }
    // The results are in an array ordered by confidence.
    // console.log(results[0]);
    label = results[0].label;
    // Classifiy again!
    classifyVideo();
  }// Classifier Variable
  let classifier;
  // Model URL
  let imageModelURL = 'https://teachablemachine.withgoogle.com/models/2qDsm85md/';
  
  // Video
  let video;
  let flippedVideo;
  // To store the classification
  let label = "";

  // Load the model first
  function preload() {
    classifier = ml5.imageClassifier(imageModelURL + 'model.json');
  }

  function setup() {
    createCanvas(320, 260);
    // Create the video
    video = createCapture(VIDEO);
    video.size(320, 240);
    video.hide();

    flippedVideo = ml5.flipImage(video);
    // Start classifying
    classifyVideo();
  }

  function draw() {
    background(0);
    // Draw the video
    image(flippedVideo, 0, 0);

    if (label == "Class 1")
        {
      // Draw the label
      fill(255);
      textSize(16);
      textAlign(CENTER);
      text("Peace", width / 2, height - 4);
      noTint();
      }
    else if(label == "Class 2")
      {
      // Draw the label
      fill(255);
      textSize(16);
      textAlign(CENTER);
      text("Violence", width / 2, height - 4);
      tint(204, 0, 0);
      }
  }

  // Get a prediction for the current video frame
  function classifyVideo() {
    flippedVideo = ml5.flipImage(video)
    classifier.classify(flippedVideo, gotResult);
    flippedVideo.remove();

  }

  // When we get a result
  function gotResult(error, results) {
    // If there is an error
    if (error) {
      console.error(error);
      return;
    }
    // The results are in an array ordered by confidence.
    // console.log(results[0]);
    label = results[0].label;
    // Classifiy again!
    classifyVideo();
  }
  ```
# lab07-machine-learning

1. Create a brief demo with Teachable Machine
  - Go to https://teachablemachine.withgoogle.com/
  - Follow the instrcutions for an Image Project (standard image model)
  - Train a model to recognize something from your webcam
  - Export your model, upload it!
  - Copy the p5.js code snippet from the export pop-up.
  - Using [p5.js](https://editor.p5js.org/), code some visual that reacts to data from your trained model
2. Create a program that uses gesture recognition

## Submission Instructions
- Create a pull request against this repo
- push your code and/or a link to a gif or video of your work
