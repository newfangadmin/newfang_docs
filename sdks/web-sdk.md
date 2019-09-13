# Web SDK

The Newfang SDK for Web Apps.

### Installation

Download your SDK from [Dev Portal](https://developer.newfang.io) and place it in your project code.

### Usage

#### Getting Started

Add your library to the html

```markup
<script src="../path/to/sdk/newfang-downloader.js"></script>
<script src="../path/to/sdk/newfang-uploader.js"></script>
<script src="../path/to/sdk/newfang_utils.js"></script>
```

#### Uploader

{% hint style="info" %}
Newfang uses a combination of your file's content hash and a convergence key to identify your file. The SDK exposes a method to generate this convergence key where you can specify: 

**App level convergence**  
No duplication of any file across your app. Only a single copy of a specific file is stored.  
No need to call _generate\_convergence\(\)_. The SDK handles this.  
  
**User level convergence**  
No duplication of any file for a specific user. Different users can upload the same file and they would be treated as different copies.  
Call _generate\_convergence\(\)_ once per user and store the _convergence_ against a specific user.  
  
**File level convergence**  
All files are duplicated. The same user can upload the same file multiple times and they would be treated as separate copies.  
Call _generate\_convergence\(\)_ each time you upload a file and store the _convergence_ against that file.
{% endhint %}



```javascript
const Uploader = window.newfang_uploader.default;

// Create an instance of the Uploader object and pass in the HTML5
// file object and the convergence
const uploader = new Uploader({
    file, // HTML5 file object
    convergence
});

// Subscribe to the 'error' event and wrap it around your error handling
uploader.on("error", (e) => {
    console.log(e);
    // Error. Do something.
});

// Subscribe to the 'progress' event and inform your view
uploader.on("upload_progress", (percentage) => {
    console.log("upload progress: ", percentage + "%");
});

// Subscribe to the 'complete' event and wrap your completion handler code
// URI is the identifier for the uploaded file and the only way to access it
uploader.on("upload_complete", (uri) => {
    console.log({ uri });
    // Upload complete. Do something.
});

// Subscribe to all events before calling start
uploader.start_upload();
```

#### Downloader

```javascript
const Downloader = window.newfang_downloader.default;

// Create an instance of the Downloader object.
// Pass it the file's URI, absolute download path, download type
// and useWorkers boolean
// Download types are 'chunked' for chunked downloads or
// 'stream' for piped streaming download
// useWorkers: true will utilize the HTML5 Web Workers feature
downloader = new Downloader(uri, {
    downloadPath: "/path/to/download",
    type: "Download",
    useWorkers: true
});

// Subscribe to the 'error' event and wrap it around your error handling
downloader.on("error", (e) => {
    console.log({ e });
    // inform your app
});

// Subscribe to the 'progress' event and inform your view
downloader.on("download_progress", (percentage) => {
    console.log("download progress: ", percentage + "%");
    // inform your app
});

// Subscribe to the 'complete' event and wrap your completion handler code
downloader.on("download_complete", () => {
    console.log("download complete");
    // inform your app
});

// Subscribe to all events before calling start
downloader.start_download("file_name_with_extension")
```

#### Delete

```javascript
const Utils = window.newfang_utils.default;

// Create an instance of the Utils object
// Pass it the file's convergence and URI
const util = new Utils({ convergence, uri });

// Subscribe to the 'error' event and wrap it around your error handling
util.on("error", error => {
    console.log({ error });
});

// Subscribe to the 'success' event and wrap your delete success handler code
util.on("success", () => {
    console.log("File removed successfully");
});

// Subscribe to all events before calling start
// Pass it an optional callback
util.start_delete(callback);
```

#### Remember

* Call the convergence once or multiple times depending on your apps use case.
* Pass in the correct convergence in order to correctly upload/delete a file.
* Start the operations\(upload/download/delete\) after subscribing to its events.

### Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

### License

None

