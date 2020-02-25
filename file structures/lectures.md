## [Comma-separated values](https://en.wikipedia.org/wiki/Comma-separated_values) (CSV) File Format:
```
Year,Make,Model,Description,Price
1997,Ford,E350,"ac, abs, moon",3000.00
1999,Chevy,"Venture ""Extended Edition""","",4900.00
1999,Chevy,"Venture ""Extended Edition, Very Large""",,5000.00
1996,Jeep,Grand Cherokee,"MUST SELL!
air, moon roof, loaded",4799.00
```
To begin with,let's create a simple csv file from [Mockaroo](https://www.mockaroo.com/), a online test data generator tool. 

* popular way of exchanging data between applications.
* simple format to keep tabular information
* each line of the file is a data record. Each record consists of one or more fields, separated by commas.
* '\r\n' is used to signify the end of line of text
* in some files, values are surrouned by quotation marks, which may need to be striped off.

## Create and download data in CSV in plain JavaScript (Bronze)

Most applications allow users to save and export the data as csv format so these data can be imported to other applications such as Excel or apps written in Python for data analysis.

In this example, you will see how to let your users save data (an 2-D array) from the browser. 
1. open the read_csv_blank.html in your code editor. You will see a 2-D array named heros.

1. create a download button with onclick event handler function downloadCSV(). 
```html
 <button onclick="downloadCSV();"> Download Class List(CSV)</button>
 ```

3. create the function downloadCSV()
    1. create a string that will become the content of the CSV file. In the first line we add the header row and finish with a newline (\r\n). 
    ```javascript
    var content = 'ImportIdentifier,PreferredName,LastName,Dob,FormGroup\r\n';
    ```
    2. using a for loop ,we first add all the values within each hero array with the join() method to the content string,and finish it with a newline(\r\n). Once the loop is done, we finish adding the values for all elements in the heros array,separated with commas. 
    ```javascript
    for(let hero of heros){
               
      content += hero.join() + '\r\n';
            
    };
    ```

    3. Once we have the content done, we create a an **a** element and in the link (the href part) we add the URI-encoded version of the future CSV file. We can even add the future name of the file which is 'class list.csv' in our case. Without that Chrome just saved the file calling it 'download.csv'.
    ```javascript
    var link = document.createElement('a');
    link.href = 'data:text/csv;charset=utf-8,' + encodeURI(content);
    link.target = '_blank';//download in a new window
    link.download = 'class_list.csv';
    ```
    4. The last step is to trigger the newly created element which tell the browser to download the "file". link.click()
    ```javascript
    link.click();
    ```

## Parse a CSV file with plain JavaScript (Silver)

This example will guide you through parsing a user-uploaded csv file into a table. **You need to use the CSV file generated from the Bronze challenge.**

This task can be broken down into 4 smaller ones.
1. create the interface to let users upload a csv file from the browser.
1. use the [HTML5 File API](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications) to load and process files from local file system to memory. A [FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader/onload) object is needed to do the heavylifting for us.
1. split the text read from csv file into arrays 
1. iterate arrays to generate table

Let's get started.
1. create a input field of the file type and a upload button, which will trigger the uploadCSV() function.
```html
<input type="file" id="fileUpload1" />
<button onclick="uploadCSV();">Upload</button>
```
2. create a function named uploadCSV()
```javascript
function uploadCSV(){

}
```
3. load file data with FileReader:
    1. create a new FileReader object.
    ```javascript
    var reader = new FileReader();
    ```
    2. use the readAsText() method to specify the file for the reader to read. As the name suggests, it will store the file data as a text string.
    ```javascript
    var fileUpload = document.getElementById('fileUpload1');
    reader.readAsText(fileUpload.files[0]);
    ```
    3. specify what to do when when read operation is complete , the readyState is changed to done, the loaded event is triggered. Write your function here to render the table. Use e.target.result to access the text string(read from file). You can console.log the result to observe the format of the data.

    ```javascript
    reader.onload = function (e){
      console.log(e.target.result);//e holds the info of the onload event
    }
    ```
    4. make sure you've got the data before moving to the next step. The text string stored in the result property has no structure. How can we convert it into an array? Remember in a csv file, at the end of each line of text, there is a \r\n? We can use newline symbol to split the text into an array, each element of which represents a line/record in the file.
    ```javascript
    var rows = e.target.result.split("\n");
    ```
    5. use for ... of loop to create a new row in a table. You can console.log the row to see what each row looks like
    ```javascript
    let table = document.createElement('table');
    for (let row of rows) {
       console.log(row);
       newRow = table.insertRow();           
    }
    ```
    6. before adding cells to the new row, split the row into an array called cells,which contain the value for each field.
    ```javascript   
    let cells = row.split(',');
    ```
    7. use for...of loops to create new cells to the new row. This is a nested loop
    ```javascript
     for (let cell of cells) {
       let newCell = newRow.insertCell();
       newCell.innerHTML = cell;
     }
    ```
   ### You may wonder why we use for..of loop instead the native for loops. 
   Generaly, for..of loop is the most robust way of iterating over an array or objects. With for...of loop, you have access to the element inside the array. Whereas with for loop, you have the access to the INDEX. Sometimes, this can be useful. For more information, please refer to this [awesome article](https://thecodebarbarian.com/for-vs-for-each-vs-for-in-vs-for-of-in-javascript)

Congratulations you have completed the above chanllenges. 
You are so close to reach the Gold level!

## Display heros' age in a separate column (Gold)
For the final challenge, based on the silver challenge, you need to parse the data and add a new column showing the age of the heros.

Hint:
1. you need to work out how to create a Date object from a string. 
2. you may need to use the native for loops instead of for...of and think about why? 


# XML

## Opener
Suppose your fellow colleauges ask you for help with the following two tasks:
1. [parsing XML data from open weather map](https://community.particle.io/t/parsing-xml-data-from-openweather-map/22047).
1. [how to create a product feed in XML](https://community.shopify.com/c/Shopify-Discussion/How-to-create-Custom-Product-XML/td-p/366075) 

The two scenarios above are common applications of XML. As a software developer, you are very likely to write software modules to create, retrieve, extract data from XML files.
For more details on product feed, check out this [article](https://api2cart.com/ecommerce/product-feeds-work-e-commerce/)

### What is XML?
XML is a software- and hardware-independent tool for storing and transporting data.
* XML stands for eXtensible Markup Language
* XML is a markup language much like HTML
* XML was designed to store and transport data
* XML was designed to be self-descriptive

Go to this link to look at a [sample XML](https://codebeautify.org/xmlviewer#)

#### XML vs HTML
* XML was designed to carry data - with focus on what data is
* HTML was designed to display data - with focus on how data looks
* XML tags are not predefined like HTML tags are

### XML vs CSV
Most XML applications will work as expected even if new data is added (or removed). However, this won't apply to CSV. On Friday, we will write a module to make comparison between them.

### Jargons
Elements, tags, node
* An element consists of an opening tag, its attributes, any content, and a closing tag.
* A tag – either opening or closing – is used to mark the start or end of an element.
* A node is a part of the hierarchical structure that makes up an XML document. “Node” is a generic term that applies to any type of XML document object, including elements, attributes, comments, processing instructions, and plain text.

### Request XML data from server
All modern browsers have a built-in XMLHttpRequest object to request data from a server.

It allows developers to:
* Update a web page without reloading the page
* Request data from a server - after the page has loaded
* Receive data from a server  - after the page has loaded
* Send data to a server - in the background

### Try it yourself - request XML data (Bronze)
```javascript
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
       // Typical action to be performed when the document is ready:
       console.log(this.responseXML);// this refers to the XMLHttpRequest object you just created. The data is stored in its responseXML property. You should define your own callback function here to manipulate the data retrieved from the server.
    }
};
xhttp.open("GET", "sample.xml", true);
xhttp.send();
```
The code is explained perfectly in [W3School tutorials](https://www.w3schools.com/xml/xml_http.asp)

Your next job is to extract value from the XML document. 
To prepare you for this, you can open the sample XML file in the browser. Open your console window and type the following command to observe the results

There are various ways to access the value of one element.
```javascript
document.getElementsByTagName('CD')
document.getElementsByTagName('CD')[0]
document.getElementsByTagName('TITLE')
document.getElementsByTagName('TITLE')[0]
document.getElementsByTagName('TITLE')[0].innerhtml
document.getElementsByTagName('TITLE')[0].firstChild
document.getElementsByTagName('TITLE')[0].childNodes[0].nodeValue
```
When you feel confident accessing the values of all elements, you can have some real fun playing with the data.
### Silver challenge -- display the XML data in a table

Should you have any issue, you can refer to the file named display_xml.html

### Gold challenge -- retrieve and display data from open weather API

### Resources:
* [More challenges on W3School](https://www.w3schools.com/xml/ajax_applications.asp)
* [open weather API](https://openweathermap.org/api)