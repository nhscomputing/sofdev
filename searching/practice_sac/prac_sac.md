# Module 3 Practice
The interface will look like the screenshot below:

![final](https://content.screencast.com/users/Sensei2020/folders/Jing/media/6265c924-1828-4596-8565-09c553ef04cb/2020-03-22_2002.png)
## Step 1: manipulate the csv text data into an array of objects.
* Input: the CSV file(refer to the read_write_csv_raw.html under file structure folder)
* Output: the array of objects
* If it is hard for you, you can store the data in a 2D array
* Interface: input(file) field and a button

![CSV file](https://content.screencast.com/users/Sensei2020/folders/Jing/media/07103681-68f5-4e29-8f10-5a5bfb51198a/2020-03-22_1816.png)
![objects](https://content.screencast.com/users/Sensei2020/folders/Jing/media/5d1243f0-77e8-4bb4-9d1c-066acd4ce5a0/2020-03-22_1818.png)

## Step 2: filter the objects by a property
* create a function that can search the array of objects for a target under a specific property, e.g. find the objects whose first name is 'Zac' or whose date contain Feb.
* the function should take in 3 parameters, e.g. filterBy(arr,key,value)
* why bother create this function? You can resue the code for filtering by various of properties. e.g. you may need to search the objects that match both a certain first name and dates which contains a certain month. That means you can call the filterBy function with different parameters instead of rewriting the same code.
## Step 3: search the objects by the user choice of inputs
* Input: user types in a firstname, an ID, selects a month
* Output: array of objects that match with the search key criteria
* iterate over the input fields and call filerBy function with the right parameters
## Step 4: display the search result
* use backtick (`) to prepare for the table html output(refer to the quiz project)
* loop through the result array to append each row in the table

Resources:
[find an object in an array based on the object's property](https://www.linkedin.com/pulse/javascript-find-object-array-based-objects-property-rafael)
[convert a csv file into JS objects](https://stackoverflow.com/questions/28543821/convert-csv-lines-into-javascript-objects)