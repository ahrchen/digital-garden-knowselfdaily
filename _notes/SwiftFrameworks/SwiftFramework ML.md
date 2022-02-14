---
title: Swift Framework ML
---

### Main Idea
Core ML is capable of handling a variety of training tasks, such as recognizing images, sounds, and even motion, but in this instance we’re going to look at tabular regression. That’s a fancy name, which is common in machine learning, but all it really means is that we can throw a load of spreadsheet-like data at Create ML and ask it to figure out the relationship between various values.

Machine learning is done in two steps: we train the model, then we ask the model to make predictions. Training is the process of the computer looking at all our data to figure out the relationship between all the values we have, and in large data sets it can take a long time – easily hours, potentially much longer. Prediction is done on device: we feed it the trained model, and it will use previous results to make estimates about new data.

```swift
// Let’s start the training process now: please open the Create ML app on your Mac. If you don’t know where this is, you can launch it from Xcode by going to the Xcode menu and choosing Open Developer Tool > Create ML.

// Follow instructions here: https://www.hackingwithswift.com/books/ios-swiftui/training-a-model-with-create-ml

```


