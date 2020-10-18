# vue3-simple-file-input

Simple file input made for Vue.js, just install and add a v-model to the component. This accept a variety of files types. Be confidente to ask more file inputs at twitter to [@mrdarkjeda](https://www.twitter.com/@darkjeda)

## Installation

As usual, just use
```
npm i vue3-simple-file-input
```

## Usage
In any .vue component file just add the import for the component, by example
```js
import FileInput from 'vue3-simple-file-input'
```

and add it in your components section as:

```js
components {
  FileInput
}
```

This component needs a v-model to work as a return variable. So in your template HTML section use it as:
```html
<file-input v-model="YourModel">
```

This returns an object with 4 inner variables:
```
response = {
  file: <- This is the file itself
  fileName: <- The file name
  fileBlob: <- The file blob in case you need to add it into a FormData and send it in a HTTP Request,
  fileType: <- The file type
}
```

In case the window file selection is closed, this may return NULL


#### Optional
This component plugin accept 6 general file types and other few more options, so if you want to use one, use it like:
```
Excel files
<file-input v-model="YourModel" is-excel>

Word files
<file-input v-model="YourModel" is-word>

Image files
<file-input v-model="YourModel" is-image>

Video files
<file-input v-model="YourModel" is-video>

PDF files
<file-input v-model="YourModel" is-pdf>

Audio files
<file-input v-model="YourModel" is-audio>

Change background color to the button
<file-input v-model="YourModel" button-background-color="#YouColorHere">

Change text color to the button
<file-input v-model="YourModel" button-text-color="#YouColorHere">

Change the placeholder input text
<file-input v-model="YourModel" placeholder-input-text="Your Placeholder Here">

Change the placeholder button text
<file-input v-model="YourModel" placeholder-button-text="Your Placeholder Here">
```

And of course, you can leave it without a file type, it will accept any file type.

## License
[MIT](https://choosealicense.com/licenses/mit/)