# Submission 

Name: Megan Reddy

I trained my model using "thumbs up" and "thumbs down" images to create a denoiser.

![training_data](https://user-images.githubusercontent.com/20704997/202355821-2f3d1ede-2471-479a-87e7-50dfc17daeb4.PNG)

![machine_learning](https://user-images.githubusercontent.com/20704997/202355829-9a554bb2-3bef-4a3a-9963-3a425fe18b0e.gif)

Code:

```
// Classifier Variable
let classifier;
// Model URL
let imageModelURL = 'https://teachablemachine.withgoogle.com/models/V0DcPEVDb/';

// Video
let video;
let flippedVideo;
// To store the classification
let label = "";
let noisy_img;
let denoised_img;

// Load the model first
function preload() {
  noisy_img = loadImage('cover_pathtraced_100.png');
  denoised_img = loadImage('cover_denoised_1000.PNG');
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
  
  // Draw the image
  noisy_img.resize(200, 200);
  image(noisy_img, 120, 0);

  // Draw the label
  fill(255);
  textSize(16);
  textAlign(CENTER);
  //text(label, width / 2, height - 4);
  
  if (label === "Thumbs Up") {
    image(denoised_img, 120, 0, 200, 200);
    text("Denoised!", width / 2, height - 4);
  } else if (label === "Thumbs Down") {
    text("Pathtraced", width / 2, height - 4);
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
  - Work off off this base code: https://editor.p5js.org/kongsally/sketches/QlyiZmMNp
  - Copy the base code into this web editor for [p5.js](https://editor.p5js.org/)
  - Replace the trained model link in the base code with a link to your trained model.
  - Code some kind of visual that reacts to the output of your classifier! See https://p5js.org/reference/ for reference

2. Create a program that uses gesture recognition
  - https://editor.p5js.org/kongsally/sketches/I2HuS0w1T  

## Submission Instructions
- Create a pull request against this repo
- push your code and/or a link to a gif or video of your work
