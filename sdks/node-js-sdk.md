# Node JS SDK

## Newfang Node SDK

![](https://newfang.io/img/newfang.svg)

This is the NodeJS SDK to be used with electron or a node app.

### Installation

Download your SDK from [Dev Portal](https://developer.newfang.io)

### Usage

#### Uploader

```javascript
const Uploader = require("/path/to/sdk/newfang_uploader").default;

const convergence = Uploader.generate_convergence();

const uploader = new Uploader({
    filePath: "/path/to/your/file",
    convergence
});

uploader.on("error", (e) => console.log(e));

uploader.on("upload_progress", (percentage) => {
    console.log("upload progress: ", percentage + "%");
});

uploader.on("upload_complete", (uri) => {
    console.log({ uri });
    //upload complete
});

uploader.start_upload()
```

#### Downloader

```javascript
const Downloader = require("/path/to/sdk/newfang_downloader").default;

downloader = new Downloader(uri, { 
    downloadPath: "/path/to/download",
    type: "chunked"
});

downloader.on("download_complete", () => {
    console.log("download complete");
    // inform your app
});

downloader.on("download_progress", (percentage) => {
    console.log("download progress: ", percentage + "%");
    // inform your app
});

downloader.on("error", (e) => {
    console.log({ e });
    // inform your app
});

downloader.start_download("abc.txt")
```

#### Delete

```javascript
const Utils = require("/path/to/sdk/newfang_utils").default;

const util = new Utils({ convergence, uri });

util.on("success", () => {
    console.log("File removed successfully");
});

util.on("error", error => {
    console.log({ error });
});

util.start_delete(callback);
//optional callback
```

#### Info

* The convergence during upload and delete should be same for the same file for the process to work.
* In download type, it can be "chunked" or "stream". 
  * Download - Chunked Download 
  * Stream - Piped stream Download
* Start the operations after subscribing to events.

### Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

### License

None

