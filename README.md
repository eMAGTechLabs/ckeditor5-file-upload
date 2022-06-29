# ckeditor5-file-upload
CKEditor5 File Upload Plugin

This plugin allows you to upload file that have mime type application/*.


# Installation

```
npm i @emagtechlabs/ckeditor5-file-upload
```
or
```
yarn add @emagtechlabs/ckeditor5-file-upload
```

# Usage

Update src/ckeditor.js with:
```javascript
import FileUpload from "@emagtechlabs/ckeditor5-file-upload/fileupload";
import SimpleFileUploadAdapter from "@emagtechlabs/ckeditor5-file-upload/src/simplefileuploadadapter";

Editor.builtinPlugins = [
  // ...
  FileUpload,
  SimpleFileUploadAdapter,
  // ...
];

Editor.defaultConfig = {
  // ...
  simpleFileUpload: {
    url: 'http://my-custom-link.com',
	withCredentials: true,
	headers: {
		'X-CSRF-TOKEN': 'CSRF_TOKEN',
		Authorization: 'Bearer <JSON Web Token>',
	},
    fileTypes: [
      '.pdf',
      '.doc',
      '.docx',
      '.xls',
      '.xlsx'
    ]
  },
  toolbar: {
    items: [
      // ...
      'fileUpload',
      // ...
    ]
  },
  // ...
};
```
Then
```
npm run build
```
or
```
yarn build
```
# How it works

The plugin creates a link entity inside editor content with an empty href attribute and when the upload process is completed the server response should contains an resourceUrl key which points to the uploaded file on the server. The value of the resourceUrl key will be added to the empty href attribute of the previously created link. 

### Communication protocol
When the file upload process starts, the adapter sends a POST request to config.simpleFileUpload.url.

### Configuring allowed file types
Use the simpleFileUpload.url configuration option to define the allowed file MIME types that can be uploaded to CKEditor 5.

By default, users are allowed to upload pdf, doc, docx, xls, xlsx documents.

### Upload file
When the file upload process is initiated, in the editor content appears a link with href attribute empty and text link corresponds to the  uploaded file name.

![Toolbar Inputs](https://bucket-doc-s1.s3.eu-central-1.amazonaws.com/images/print4.png)
<br/>

### Upload progress
This upload adapter will show users about the file upload progress with the help of a progress bar.
The progress bar has a button to cancel the file upload process.

### Upload complete
When the file has been successfully uploaded, the server should return an object containing the resourceUrl key which points to the uploaded file on the server. The value of the resourceUrl key will be added to the empty href attribute of the previously created link. 

![Toolbar Inputs](https://bucket-doc-s1.s3.eu-central-1.amazonaws.com/images/print3.png)
<br/>