Learn more about how to use the code snippet on [github](https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image).

```html
<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
function getTotalClasses() {
    if (model) {
        return model.getTotalClasses(); // Retrieve total class count from the loaded model
    } else {
        console.error("Model is not loaded. Please initialize the model first.");
        return -1; // Return -1 as an error indicator
    }
}
// Function: getTotalClasses
// Purpose: Returns the total number of classification categories in the trained model. 
// Effect: Helps determine the number of possible outputs the model can predict.
// Parameters: 
// - None
// Return: 
// - : The number of class labels available in the model.

//Help was contained from reddit/ fellow programers for only a little bit of that part and aslo some from chat gpt to just help refrain it into shape.
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "{{(https://www.kapwing.com/w/qeRTMapynf)}}";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
       // Test to confirm correct paths
    console.log("Model URL:", modelURL);  // Check the model path
    console.log("Metadata URL:", metadataURL);  // Check the metadata path
//Got help from CHAT GPT to help see how to put the metadataUFRL and model URL IN FORMATE FOR CODING.
        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
         console.log("Model URL:", modelURL);
          console.log("Metadata URL:", metadataURL);
// Machine Learning Library: Teachable Machine Image Model
// Purpose: This library allows a program to classify images based on pre-trained data. 
// The model makes predictions by analyzing image features and determining which class 
// (category) the image belongs to, based on patterns learned during training. 
// The model’s predictions are displayed in real-time on the webpage. 
// Effect: This helps automate processes by enabling a program to identify objects 
// and classify them without direct user input, a technique used in machine learning.
// Parameters:
// - (IMAGE): The input image data captured from the webcam or selected from a file. 
// Return:
// - (STRING): The predicted class label (category) for the image with the highest probability.
// - (NUMBER): The confidence score (probability) for the predicted class label.
// Key Concepts:
// - "label-container" refers to an HTML element that displays the class labels and 
//   corresponding prediction probabilities on the webpage. This allows users to see the 
//   result of the model’s classification (MDN Web Docs, 2024).
// - "fetch" is used to retrieve external files, such as the model structure (`model.json`) and 
//   metadata (`metadata.json`), from an online or local source. This is necessary for the model 
//   to function correctly by loading its trained parameters into the program (MDN Web Docs, 2024).
// - "model.json" contains the structure of the machine learning model, including its layers, 
//   architecture, and learned weights. "metadata.json" stores information about the model’s 
//   training, including the class labels it is capable of identifying (Google Teachable Machine Docs, 2024).
// Citations:
// - MDN Web Docs. "Document Object Model (DOM) - Manipulating HTML Elements." Mozilla, 2024.  
//   [https://developer.mozilla.org/en-US/docs/Web/API/Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)
// - MDN Web Docs. "fetch() API - JavaScript." Mozilla, 2024.  
//   [https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
// - Google Teachable Machine Docs. "Exporting and Using Your Model." Google AI, 2024.  
//   [https://teachablemachine.withgoogle.com/train](https://teachablemachine.withgoogle.com/train)
//Information was conatined from reddit and information off of code.orgs websites and also wikipedia and some from Khan Academy.
//This information was written by me Ankush and refined/ re shaped into API formate by Chat Gpt To make life easy and save time.

        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
// Function: predict
// Purpose: This function analyzes an input image and predicts which class (category) it most likely belongs to, 
// based on the trained machine learning model. The prediction is made by comparing the image to the 
// model’s learned patterns, and it returns the class with the highest probability score.
// Effect: This allows the program to identify objects in images by classifying them, providing both the 
// class label and the likelihood (probability) of the classification. It is useful for image recognition tasks, 
// where the model assigns each image to a predefined category.
// Parameters:
// - (IMAGE): The input image to be classified, typically a canvas element or a webcam image.
// Return:
// - (ARRAY): An array of prediction objects, each containing:
//   - (STRING): The class label of the prediction (e.g., "cat", "dog", etc.)
//   - (NUMBER): The probability of the predicted class (between 0 and 1), indicating the confidence level.
// Data Types:
// - Parameters:
//   - (IMAGE): A `HTMLCanvasElement` or `HTMLImageElement`, depending on the source of the input (webcam or file).
// - Return:
//   - (ARRAY): An array of objects, where each object has two properties:
//     - (STRING): Class name (the predicted category label).
//     - (NUMBER): The probability of the class label.
//Information was reformed into commet format by chat gpt, information was gathyered by cord.org, and reddit.
</script>
```
