# lab07-machine-learning

![](lab07.gif)

Model:
```
// Copyright (c) 2019 ml5
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

// TODO: Upate your model URL
let imageModelURL = 'https://teachablemachine.withgoogle.com/models/vm-18A1lO/';

// Video
let video;
let flippedVideo;
// To store the classification
let label = "";
let peek_img;

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
  
  peek_img = createImg("https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/844e0a8e-3ac6-49c6-b2d4-4f762e7605d9/d6qm7cx-846498fd-6e5c-41b3-9b41-b5f432cf3c1f.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzg0NGUwYThlLTNhYzYtNDljNi1iMmQ0LTRmNzYyZTc2MDVkOVwvZDZxbTdjeC04NDY0OThmZC02ZTVjLTQxYjMtOWI0MS1iNWY0MzJjZjNjMWYuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.qK-H_DOU3WIFDiqaV3z7WGsH6m8PGkc-GAglOEjIJvI");
  peek_img.hide();

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
  if (label === "Class 2") {
    image(peek_img, 0, 0, peek_img.width*0.75, peek_img.height*0.75);
    text("Hello by Toothless", width / 2, height - 4);
  } else if (label === "Class 1") {
    text("Hello by Wenqing!", width / 2, height - 4);
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
  label = results[0].label;
  // Classifiy again!
  classifyVideo();
}
```
