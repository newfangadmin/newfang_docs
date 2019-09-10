# Web SDK

The Newfang SDK for Web Apps.

### Installation

Download your SDK from [Dev Portal](https://developer.newfang.io)

### Usage

#### Getting Started

Add your library to the html

```markup
<script src="../path/to/sdk/newfang-downloader.js"></script>
<script src="../path/to/sdk/newfang-uploader.js"></script>
<script src="../path/to/sdk/newfang_utils.js"></script>
```

#### Uploader

```javascript
const Uploader = window.newfang_uploader.default;

const uploader = new Uploader({
    file // HTML5 file object
});


uploader.on("error", (e) => console.log(e));

uploader.on("upload_progress", (percentage) => {
    console.log("upload progress: ", percentage + "%");
});

uploader.on("upload_complete", (url) => {
    console.log({ url });
    //upload complete
});

uploader.start_upload()
```

#### Downloader

```javascript
const Downloader = window.newfang_downloader.default;

downloader = new Downloader(uri, { 
    downloadPath: "/path/to/download",
    type: "Download",
    useWorkers: true
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

downloader.download(file_name_with_extension);
```

#### Delete

```javascript
const Utils = window.newfang_utils.default;

const util = new Utils({ uri });

util.on("success", () => {
    console.log("File removed successfully");
});

util.on("error", error => {
    console.log({ error });
});

util.remove(cb);
//optional cb
```

### Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

### License

None

