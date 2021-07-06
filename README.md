# Form troubleshooter

Chrome extension to find and fix common form problems.

![image](https://user-images.githubusercontent.com/205226/124280594-c7b74a00-db40-11eb-8770-78a857815480.png)

![image](https://user-images.githubusercontent.com/205226/124281671-d9e5b800-db41-11eb-93d4-32b268c10a74.png)

![image](https://user-images.githubusercontent.com/205226/124281578-c0447080-db41-11eb-8a13-f04b1badd920.png)


## Installation 

When released, this extension will be available from the [Chrome Web Store](https://chrome.google.com/webstore/category/extensions).

For the moment, you'll need to install it from the local files.

1. [Download the code](https://github.com/GoogleChromeLabs/form-troubleshooter/archive/refs/heads/main.zip) 
or clone the repo: `git clone git@github.com:GoogleChromeLabs/form-troubleshooter.git`.
1. In Chrome, navigate to `chrome://extensions`.
1. Enable **Developer mode**.
1. Click the **Load unpacked** button and select the top-level directory containing the extension.
1. You can pin the extension so its icon is always visible: from the Chrome **Extensions** menu, 
select **Form Troubleshooter**.


## Usage

Visit a page you want to check and click the extension icon. The extension popup has three sections:

* **Overview of form and form field elements**
* **Errors**
* **Warning**

The extension retrieves and audits form element and attribute every time the icon is clicked.

**Save as HTML** saves the report as a local HTML file.

You can try out the extension on the test page [form-problems.glitch.me](https://form-problems.glitch.me).


## How it works

The extension checks the current page for form and form field elements each time it's opened.

1. The extension icon is clicked to open [popup.html](popup.html).
1. popup.js [sends a message](js/popup.js#L34) to [content-script.js](js/content-script.js#L32) that 
the popup has opened.
1. content-script.js [gets data](js/popup.js#L33) for form and form field elements on the current page. 
1. content-script.js [stores the data](js/popup.js#L42) using chrome.storage.
1. content-script.js [sends a message](js/content-script.js#L57) that element data has been stored.
1. On [getting the message](js/popup.js#L42), popup.js [gets the data from chrome.storage](js/popup.js#L50).
1. popup.js [runs the audits](js/popup.js#L54) defined in [audits.js](js/audits.js#L27), to check 
the form elements and attributes in the page.
1. popup.js [displays an overview](js/popup.js#L58) of form and form field data in popup.html.
1. audits.js [displays results](js/audits.js#L59) of the audits in popup.html.


## Feedback and feature requests

Feedback and audit suggestions welcome!

* [Make a comment or request](https://forms.gle/Sm7DbKfLX3hHNcDp9)
* [File a bug](https://github.com/samdutton/form-troubleshooter/issues/new)


## TODO

* Link to and/or highlight problematic elements.
* Move code for displaying audit results [out of audits.js](js/audits.js#L59).
* Move constants to external file.
* Check for forms (or other elements) that don't have a closing tag.
* Suggest alternatives to invalid attribute names, e.g. for `autcomplete`.
* Convert `map(field => stringifyElement(field));` to a single function.
* Sort out form field/element naming (labels and buttons are not fields).

---

This is not a Google product.
