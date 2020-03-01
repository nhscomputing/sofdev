# hints and tips 
When I first learned to build a project, I always struggled with getting started. From my past experiences, I realised you can always start with the user input data. You can ask yourself the following questions:
* how can users enter the data? In this case, you let users select a file and upload to your quiz app.
* what do I do after I get the raw data? We convert the data from text to XML DOM object
* is the raw data ready to be used? If not, what data structure should I use to store the data? We will extract the info from XML DOM object and use object to represent the quiz and array to represent the list of quizzes.
* what output it should look like? You can write down the html template for the output and replace the actual content with the variables. This is called templating in real-world programming.
## 1. how to read the content of files stored on user's computer?
1. create an input element of the type 'file' to let user select files from their computer. And a button to upload the selected file to your app.
```html
<input type="file" id="fileUpload">
<button onclick="loadXml();">Load the quiz XML</button>
```
2. obtain the reference for the input element
```javascript
const fileUpload = document.getElementById('fileUpload');
``` 
3. create a new FileReader object to obtain the content of the selected file from the input element with id:fileUpload.
```javascript
var reader = new FileReader();
// the content of the file will be read as text
reader.readAsText(fileUpload.files[0]); 
```
4. specify what to do when when reading operation is complete, namely the load event is triggered. onload is similar to onclick. It is an event handler when a certain event is triggered. e.g when the button is clicked, you alert the user with some text.
```javascript
reader.onload = function(){
    // the reader object stores the content of the file in its result property. That's where you can access the data.
    const text = this.result;
    console.log(text);// test if it works
```
## 2. how to convert text into an XML DOM object?
The XML DOM (Document Object Model) defines the properties and methods for accessing and editing XML. 
However, when the XML file is loaded from hard drive into memory by the FileReader object, it is stored as text instead of an XML DOM object. You need to convert the text into XML DOM object before you can access the methods such as getElementByTagname().
All modern browsers have a built-in XML parser that can convert text into an XML DOM object.

In this example, we stores the part of xml quiz content as a text variable. It is the format after being loaded.
```javascript
text = "<quizzes><quiz>" +
"<question>What game show does Moss go on?</question>" +
"<option>Tipping Point</option>" +
"<option>Who wants to Be a Millionaire?</option>" +
"<option>Countdown</option>" +
"<option>The Chase</option>" +
"<answer>c</answer>" +
"</quiz></quizzes>";
```
1. create a new XML DOM parser object
```javascript
var parser = new DOMParser();
                var xml = parser.parseFromString(text, 'text/xml');
```
2. The parser creates a new XML DOM object using the text string:
```javascript
var xml = parser.parseFromString(text, 'text/xml');
console.log(typeof(xml)); 
```
## 3. how to extract the info from XML DOM object?
We will continue using the code from the previous example. Our job is to extract the text content from the elements such as question/option/answer
1. obtain the list of quiz elements.
```javascript
var quiz_list = xml.getElementsByTagName('quiz');
```
2. extract the text content from quiz's child elements including 1 <question>, 4 <option> and 1 <answer> tags. Given there is only 1 quiz element under the root element quizzes. The index of the first and the only quiz element is 0 and the quiz element is quiz_list[0]
```javascript
// obtain the content of the <question> tag
let question = quiz_list[0].getElementsByTagName('question')[0].childNodes[0].nodeValue;
```
3. obtain a list of option elements using getElementByTagname('option'). Iterating over the list to grab the text content for each option tag and store the values in an array. You can do option 1, option 2, but array is more efficient.
```javascript
let options = quiz.list[0].getElementsByTagName('option');
let option_list = [];
for(option in options){
    option_list.push(option.childNodes[0].nodeValue);
}
```
4. Obtain the content from the <answer> tag
```javascript
let answer = quiz_list[0].getElementsByTagName('answer')[0].childNodes[0].nodeValue;
```
5. test your code by logging the variables
```javascript
let quiz = `question: ${question},option: ${option_list[0]},option: ${option_list[1]},option: ${option_list[2]},option: ${option_list[3]}, answer: ${answer}`;
console.log(quiz);
```
You are supposed to see the text content of one quiz. 
## 4. how to create and display the output of the quiz in html using javascript
Let's take a look at the ingredients we've got so far:
* question: string
* option_list: array
* answer: string
Then think about what the HTML output should look like?
```html
<div class="question"> 
    What game show does Moss go on?
</div>
<div class="options"> 
    <label>
        <input type="radio" name="question0" value="a">
            a :Tipping Point
    </label>

    <label>
        <input type="radio" name="question0" value="b">
            b :Who wants to Be a Millionaire?
    </label>

    <label>
        <input type="radio" name="question0" value="c">
            c : Countdown
    </label>

    <label>
        <input type="radio" name="question0" value="d">
            d :The Chase
    </label> 
</div>
```
We can replace the actual value with the variables that hold the values. Then use the template literals to print the html output. Note: the symbol we use around the strings is backtick. Not quote!
```javascript

let output = `<div class="question"> 
    ${questions}
</div>
<div class="options"> 
    <label>
        <input type="radio" name="question0" value="a">
            ${option_list[0]}
    </label>

    <label>
        <input type="radio" name="question0" value="b">
            ${option_list[1]}
    </label>

    <label>
        <input type="radio" name="question0" value="c">
            ${option_list[2]}
    </label>

    <label>
        <input type="radio" name="question0" value="d">
            ${option_list[3]}
    </label> 
</div>`
document.getElementById('quiz').innerHTML = output;
```
You should be able to see one quiz displayed. However, you may have noticed the html for displaying quiz options are repeated 4 times and share similar structure. Is there a way to make this code shorter? We can use option_list[i] to represent each option. But how to represent the value?
To address this, we need need the knowledge from data structures. Instead of using seperate variables, arrays to represent the info from one quiz, we can use object to model the quiz. We can have a quiz object with the following properties:
* question
* options
    * a: option
    * b: option
    * c: option
    * d: option
* answer
We need to tweak the code in hint 3. Add the following lines in the end. It does the job to create a quiz object using the info extracted from the XML object.
qstn is the key, question holds the value; answers is the key, the value is list of key/value pairs.
```javascript
var quiz ={qstn:question,
           answers:{
               a: option_list[0],
               b:option_list[1],
               c:option_list[2],
               d:option_list[3]
            },
            correctAnswer:answer};

```
To access the value, you can use the dot notation shown as below. objectName.propertyName
```javascript
quiz.qstn
quiz.answers.a
quiz.answers[a]
quiz.correctAnswer
```
Not, let's revisit the output html and refactor the code with the use of for...in loop.
```javascript
const answers = [];//stores all the html output for options
//letter refers to the keys in the quiz.answers object, such as a, b, c, d
for(let letter in quiz.answers){
    answers.push(
            `<label>
            <input type="radio" name="question0" value="${letter}">
            ${letter} :
            ${quiz.answers[letter]}
            </label>`);
                }
const output = `<div class="question"> ${quiz.qstn} </div>
                <div class="answers"> ${answers.join('')} </div>`
document.getElementById('quiz').innerHTML = output;
    
```
## 5. how to get the info of all quiz questions?
You need to tweak your code in hint 3. Your job is tostore the quiz info into an array of quiz objects. To start with, put the code from step 2 to 4 in hint 3 shown below inside a loop, and change quiz_list[0] to quiz_list[i]

```javascript
// these are the code from hint 3,which will be placed in a loop shown in the next code snipet. 
const quiz_list = xml.getElementsByTagName('quiz');
let question = quiz_list[0].getElementsByTagName('question')[0].childNodes[0].nodeValue;
let options = quiz.list[0].getElementsByTagName('option');
let option_list = [];
for(option in options){
    option_list.push(option.childNodes[0].nodeValue);
}
let answer = quiz_list[0].getElementsByTagName('answer')[0].childNodes[0].nodeValue;
```

```javascript
const quiz_list = xml.getElementsByTagName('quiz');
var quizzes =[]; //store the quiz objects
for(let i=0; i<quiz_list.length; i++>){
    let question = quiz_list[i].getElementsByTagName('question')[0].childNodes[0].nodeValue;
    let options = quiz.list[i].getElementsByTagName('option');
    let option_list = [];
    for(option in options){
    option_list.push(option.childNodes[0].nodeValue);
    }
    let answer = quiz_list[0].getElementsByTagName('answer')[0].childNodes[0].nodeValue;
    var quiz ={qstn:question,
               answers:{
                    a: option_list[0],
                    b:option_list[1],
                    c:option_list[2],
                    d:option_list[3]
            },
            correctAnswer:answer
        };
    quizzes.push(quiz);
}

```
## 6. how to display all questions?
You need to iterate over the array of quiz objects to generate the output for each question. Similary to hint 5, you also need to wrap the code below in hint 4 inside a loop and replace quiz with quizzes[i]. 
```javascript
const answers = [];
for(let letter in quiz.answers){
    answers.push(
            `<label>
            <input type="radio" name="question0" value="${letter}">
            ${letter} :
            ${quiz.answers[letter]}
            </label>`);
                }
const output = `<div class="question"> ${quiz.qstn} </div>
                <div class="answers"> ${answers.join('')} </div>`
document.getElementById('quiz').innerHTML = output;
    
```
```javascript
const output = [];
for(i=0; i< quizzes.length; i++>){
    const answers = [];
    for(let letter in quizzes[i].answers){
        answers.push(
                `<label>
                <input type="radio" name="question${i}" value="${letter}">
                ${letter} :
                ${quizzes[i].answers[letter]}
                </label>`);
                    }
    const output.push(`<div class="question"> ${quizzes[i].qstn} </div>
                <div class="answers"> ${answers.join('')} </div>`) 
}              
document.getElementById('quiz').innerHTML = output.join();

```
So far you are almost done with the project. It's your turn to figure out how to get user's choice and check the result. Hope you've learned heaps from this project!