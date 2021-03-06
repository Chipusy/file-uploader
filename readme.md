# Fine Uploader #

Originally developed/designed by Andrew Valums.   
Currently maintained by Ray Nicholus.

*If you have found Fine Uploader useful, please consider [donating](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=6ZMVZSC4DBRVN&lc=US&item_name=Fine%20Uploader&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted) 
to support continued maintenance and evolution of this library.*


### Announcements ###
_September 18, 2012_ - I've created a [google doc spreadsheet](https://docs.google.com/spreadsheet/ccc?key=0AnQh9-ZBDuh_dEJGZFY1dEl2SDlGUGZNLUVfanZKeXc#gid=0) 
where people can include ideas for Fine Uploader 3.0.  For some initial information about 3.0, have a look at the initial 
ideas I have in the spreadsheet, along with [this discussion](#326).  Anyone can add ideas to 
[the spreadsheet](https://docs.google.com/spreadsheet/ccc?key=0AnQh9-ZBDuh_dEJGZFY1dEl2SDlGUGZNLUVfanZKeXc#gid=0).

Also, please vote in the [Fine Uploader 3.0 poll](http://www.easypolls.net/poll.html?p=505b6af5e4b07cc0aae7deba).  
The choice is between a jQuery 3.0 version, or not.  Poll will close the night of September 23 or the morning of 
September 24 (CST).



###Table of Contents###
- [Summary](#summary)
- [Releases/Downloads](#releasesdownloads)
- [Features](#features)
- [License](#license)
- [Getting started](#getting-started)
- [qq.FileUploader - Setting up full upload widget](#qqfileuploader---setting-up-full-upload-widget)
- [Options of both FileUploader & FileUploaderBasic](#options-of-both-fileuploader--fileuploaderbasic)
- [Options of FileUploaderBasic](#options-of-fileuploaderbasic)
- [Options of FileUploader](#options-of-fileuploader)
- [Styling FileUploader](#styling-fileuploader)
- [Callbacks (FileUploader & FileUploaderBasic)](#callbacks-fileuploader--fileuploaderbasic)
- [Changing alert/messages to something more user friendly](#changing-alertmessages-to-something-more-user-friendly)
- [Instance methods](#instance-methods)
- [Troubleshooting](#troubleshooting)
- [Issue Tracker](#issue-tracker)
- [Contributors](#contributors)


### Summary ###

Welcome! This project attempts to achieve a user-friendly file-uploading experience over the web.
It's built as a Javascript plugin for developers looking to incorporate file-uploading into their website.

This plugin uses an XMLHttpRequest (AJAX) for uploading multiple files with a progress-bar in
FF3.6+, Safari4+, Chrome and falls back to hidden-iframe-based upload in other browsers (namely IE),
providing good user experience everywhere.

It does not use Flash, jQuery, or any external libraries.

Take a look at the new evolving [Demo](http://fineuploader.com) page.

Questions?  Comments?  Problems?  Post in the [forums](https://groups.google.com/forum/#!forum/fineuploader).

Looking for the [comment thread](http://fineuploader.com/discussions.html) from the valums.com website? It is still available, but please use the [forum](https://groups.google.com/forum/#!forum/fineuploader) instead.


### Releases/Downloads ###

**You can [download released versions](https://github.com/valums/file-uploader/wiki/Releases), or, if you are more daring,
use the snapshot version on the master branch.**  


### Features ###
* Multiple file select, progress-bar in FF, Chrome, Safari
* Drag-and-drop file select in FF, Chrome
* Uploads are cancelable
* No external dependencies
* Doesn't use Flash
* Fully working with HTTPS
* Keyboard support in FF, Chrome, Safari
* Tested in IE7/8, Firefox 3/3.6/4, Safari 4/5, Chrome, and Opera 10.60
* Ability to upload files as soon as they are selected, or "queue" them for uploading at user's request later
* Display specific error messages from server on upload failure (hover over failed upload item)
* Automatic uploads (as files are selected) or queue files to me manually triggered when ready


### License ###
This plugin is open sourced under MIT license, GNU GPL 2 or later and GNU LGPL 2 or later. Please see the license.txt file for details.


### Getting started ###
The `fileuploader.js` contains two classes that are meant to be used directly.
If you need a complete upload widget (from demo) to quickly drop
into your current design, use `qq.FileUploader`.

If you want to customize uploader, by using a different looking file list
or change the behaviour or functionality use `qq.FileUploaderBasic`.

The difference between them is that `qq.FileUploader` provides a list of files,
drag-and-drop, but `qq.FileUploaderBasic` only creates button and handles validation.
Basic uploader is easier extendable, and doesn't limit possible customization.

`qq.FileUploader` extends `qq.FileUploaderBasic`, so that all the options present
in the basic uploader also exist in the full widget.


### qq.FileUploader - Setting up full upload widget ###

Include `fileuploader.js` and `fileuploader.css` into your page.
Create container element.

```html
<div id="file-uploader">
<noscript>
    <p>Please enable JavaScript to use file uploader.</p>
    <!-- or put a simple form for upload here -->
</noscript>
</div>
```

Initialize uploader when the DOM is ready. Change the action option.
For example ../server/php.php for the default folder structure.
In the server folder you will find examples for different platforms.
If you can't find the one you need, check the readme.txt in the same folder.

```javascript
var uploader = new qq.FileUploader({
	// pass the dom node (ex. $(selector)[0] for jQuery users)
	element: document.getElementById('file-uploader'),
	// path to server-side upload script
	action: '/server/upload'
});
```


### Options of both FileUploader & FileUploaderBasic ###
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Default</th>
            <th>Note</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>debug</td>
            <td>boolean</td>
            <td>false</td>
            <td>If enabled, this will result in log messages (such as server response) being written to the javascript console.
            If your browser does not support the [window.console object](https://developer.mozilla.org/en-US/docs/DOM/console.log),
            the value of this option is irrelevant.</td>
        </tr>
        <tr>
            <td>action</td>
            <td>string (path)</td>
            <td>/server/upload</td>
            <td>The is the endpoint used by both the form and ajax uploader.  In the case of the form uploader, it is part of the
            form's action attribute value along with all parameters.  In the case of the ajax uplaoder, it is makes up part of the URL
            of the XHR request (again, along with the parameters).</td>
        </tr>
        <tr>
            <td>params</td>
            <td>object</td>
            <td>{}</td>
            <td>These parameters are sent with the request to the endpoint specified in the action option.</td>
        </tr>
        <tr>
            <td>customHeaders</td>
            <td>object</td>
            <td>{}</td>
            <td>Additional headers sent along with the XHR POST request.  Note that is option is only relevant to the ajax/XHR uploader.</td>
        </tr>
        <tr>
            <td>multiple</td>
            <td>boolean</td>
            <td>true</td>
            <td>Set to false puts the uploader into what is best described as 'single-file upload mode'.  See the
            [demo](http://fineuploader.com) for an example.</td>
        </tr>
        <tr>
            <td>maxConnections</td>
            <td>integer</td>
            <td>3</td>
            <td>Maximum allowable concurrent uploads.</td>
        </tr>
        <tr>
            <td>disableCancelForFormUploads</td>
            <td>boolean</td>
            <td>false</td>
            <td>If true, the cancel link does not appear next to files when the form uploader is used.  This may be desired
            since it may not be possible to interrupt a form-based upload in some cases.</td>
        </tr>
        <tr>
            <td>autoUpload</td>
            <td>boolean</td>
            <td>true</td>
            <td>Set to false if you want to be able to begin uploading selected/queued files later, by calling uploadStoredFiles().</td>
        </tr>
        <tr>
            <td>allowedExtensions</td>
            <td>array of strings</td>
            <td>[]</td>
            <td>This may be helpful if you want to restrict uploaded files to specific file types.  Note that this validation
            option is only enforced by examining the extension of uploaded file names.  For a more complete verification of the
            file type, you should use, for example, magic byte file identification on the server side and return {"success": false}
            in the response if the file type is not on your whitelist.</td>
        </tr>
        <tr>
            <td>acceptFiles</td>
            <td>comma-separated strings</td>
            <td>null</td>
            <td>This option is used solely by the file selection dialog.  If you'd like to restict valid file types that appear in the
            selection dialog, you can do this here by listing valid content type specifiers.  See the [documentation on the accept
            attribute of the input element](https://developer.mozilla.org/en-US/docs/HTML/Element/Input) for more information.</td>
        </tr>
        <tr>
            <td>sizeLimit</td>
            <td>integer</td>
            <td>0 (no limit)</td>
            <td>Maximum allowable size, in bytes, for a file.</td>
        </tr>
        <tr>
            <td>minSizeLimit</td>
            <td>integer</td>
            <td>0 (no limit)</td>
            <td>Minimum allowable size, in bytes, for a file.</td>
        </tr>
        <tr>
            <td>inputName</td>
            <td>string</td>
            <td>qqfile</td>
            <td>This usually only useful with the ajax uploader, which sends the name of the file as a parameter, using a key name
            equal to the value of this options.  In the case of the form uploader, this is simply the value of the name attribute
            of the file's associated input element.</td>
        </tr>
        <tr>
            <td>forceMultipart</td>
            <td>boolean</td>
            <td>false</td>
            <td>While form-based uploads will always be multipart requests, this forces XHR uploads to send files using 
            multipart requests as well.</td>
        </tr>
    </tbody>
</table>


### Options of FileUploaderBasic ###
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Default</th>
            <th>Note</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>button</td>
            <td>element</td>
            <td>null</td>
            <td>Specify an element to use as the "select files" button</td>
        </tr>
    </tbody>
</table>


### Options of FileUploader ###
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Default</th>
            <th>Note</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>element</td>
            <td>element</td>
            <td>null</td>
            <td>Container for the default drop zone (if supported by browser) and files list.  **Required**</td>
        </tr>
        <tr>
            <td>listElement</td>
            <td>element</td>
            <td>null</td>
            <td>Container for the file list.  If null, the list defined in the template will be used.</td>
        </tr>
        <tr>
            <td>uploadButtonText</td>
            <td>string</td>
            <td>Upload a file</td>
            <td>Label for the file selector button</td>
        </tr>
        <tr>
            <td>cancelButtonText</td>
            <td>string</td>
            <td>cancel</td>
            <td>The cancel button text (which is more of a link than a button).</td>
        </tr>
        <tr>
            <td>failUploadText</td>
            <td>string</td>
            <td>Upload failed</td>
            <td>Text that appears next to a failed file item</td>
        </tr>
        <tr>
            <td>extraDropzones</td>
            <td>array of elements</td>
            <td>[]</td>
            <td>Useful if you'd like to to designate additional dropozones for file input.  Of course, this is not relevant if the
            form uploader is used.</td>
        </tr>
    </tbody>
</table>


### Styling FileUploader ###
The `template` option contains default elements with default classes that make up the uploader as a whole in the DOM.  For example,
the first default element in `template` is a `div` with a class of `qq-uploader`.  This is the parent element of the uploader.
The default drop area, button, and file list elements are also, by default, contained in this option.  You can use this option to
add additional elements, modify default template elements, etc.

There is also a `fileTemplate` option which contains default elements that make up one file item in the file list.

Finally, a `classes` option allows you to change the default class names for these elements.  Be sure the values in `classes`
match the class names used in the corresponding template elements (where appropriate).


### Callbacks (FileUploader & FileUploaderBasic) ###
* `onSubmit(String id, String fileName)` - called when the file is submitted to the uploader portion of the code.
Note that this does not mean the file upload will begin at this point.  Return `false` to prevent submission to the uploader.
* `onComplete(String id, String fileName, Object responseJSON)` - called when the file upload has finished.
* `onCancel(String id, String fileName)` - called when the file upload has been cancelled.
* `onUpload(String id, String fileName)` - called just before the file upload begins
* `onProgress(String id, String fileName, int uploadedBytes, int totalBytes) - called during the upload, as it progresses.  Only used by the XHR/ajax uploader.


### Changing alert/messages to something more user friendly ###

You may want to change the default alert implementation and messages as you see fit.  This is possible by overriding the
`showMessage` function option, as well as the `messages` properties in FileUploaderBasic and the `extraMessages` properties
in FileUploader.  The default `showMessage` function simply invokes `alert` with the message text.  One instance in which t
his is used is when the user attempts to select an invalid file for upload.  There are general message
types with default text that can be overriden as well.


### Instance methods ###

* `setParams(Object newParams)` - Set the parameters sent along with the request after initializing the uploader.  It can be nicely used in `onSubmit` callback.
* `uploadStoredFiles()` - If `!autoUpload`, this will begin uploading all queued files.


### Troubleshooting ###

If you can't get the uploader to work, please try the following steps
before asking for help.

If the upload doesn't complete, saying "failed":

* Set the `debug` option of the FileUploader to true.
* Open the page where you have a FileUploader.
* Open developer console in your browser.
* Try to upload the file. You should see a server response.

It should be `{"success":true}` for completed requests. If it's not,
then you have a problem with your server-side script.


### Issue Tracker ###

Have a bug or feature request? Please [create an issue here on GitHub](https://github.com/valums/file-uploader/issues) 
that conforms with [necolas's guidelines](https://github.com/necolas/issue-guidelines).


### Contributors ###

We would love developers to contribute any improvements and bugfixes they produce.
See [How do I contribute to other's code in GitHub?](http://stackoverflow.com/questions/4384776/how-do-i-contribute-to-others-code-in-github).

Thanks to everybody who contributed, either by sending bug reports or donating. The project wouldn't be possible without all this generous help. Thank you!

If you have found Fine Uploader useful, please consider [donating](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=6ZMVZSC4DBRVN&lc=US&item_name=Fine%20Uploader&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted) 
to support continued maintenance and evolution of this library.
