# lab07-machine-learning


I made a program that shows a picture of a happy minion if smiling and sad minion if frowning.

GIF:

![minonfion](https://user-images.githubusercontent.com/43520504/202362340-54fcb110-00d1-4ae1-9479-321271560694.gif)

Code:
```// Copyright (c) 2019 ml5
//
// This software is released under the MIT License.
// https://opensource.org/licenses/MIT

/* ===
ml5 Example
Webcam Image Classification using a pre-trained customized model and p5.js
This example uses p5 preload function to create the classifier
=== */

// Classifier Variable
let classifier;
// Model URL
let imageModelURL = 'https://teachablemachine.withgoogle.com/models/V7eJQQdvG/';

// Video
let video;
let flippedVideo;
// To store the classification
let label = "";
let happy_img;
let sad_img;

// Load the model first
function preload() {
  classifier = ml5.imageClassifier(imageModelURL + 'model.json');
  happy_img = loadImage("dmoi.jpg");
  sad_img = loadImage("fefeeee.jpg");
}

function setup() {
  createCanvas(320, 260);
  // Create the video
  video = createCapture(VIDEO);
  video.size(320, 240);
  video.hide();

  flippedVideo = ml5.flipImage(video)
  // Start classifying
  classifyVideo();
}

function draw() {
  background(0);
  // Draw the video
  image(flippedVideo, 0, 0);

  // Draw the label
  fill(255);
  textSize(16);
  textAlign(CENTER);
  
    // TODO: Custom logic based on labels
  if (label === "Class 1") {
    //image(peek_img, 0, 0);
    image(happy_img, 0, 0, happy_img.width*0.5, happy_img.height*0.5);
    text("Banana!!!!", width / 2, height - 4);
  } else if (label === "Class 2") {
    image(sad_img, 0, 0, sad_img.width*0.25, sad_img.height*0.25);
    text("No Banana :(!", width / 2, height - 4);
  }
}

// Get a prediction for the current video frame
function classifyVideo() {
  flippedVideo = ml5.flipImage(video)
  classifier.classify(flippedVideo, gotResult);
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
}```

1. Create a brief demo with Teachable Machine
  - Go to https://teachablemachine.withgoogle.com/
  - Follow the instrcutions for an Image Project (standard image model)
  - Train a model to recognize something from your webcam
  - Export your model, upload it!
  - Work off off this base code: https://editor.p5js.org/kongsally/sketches/QlyiZmMNp
  - Copy the base code into this web editor for [p5.js](https://editor.p5js.org/)
  - Replace the trained model link in the base code with a link to your trained model.
  - Code some kind of visual that reacts to the output of your classifier! See https://p5js.org/reference/ for reference

2. Create a program that uses gesture recognition
  - https://editor.p5js.org/kongsally/sketches/I2HuS0w1T  

## Submission Instructions
- Create a pull request against this repo
- push your code and/or a link to a gif or video of your work
