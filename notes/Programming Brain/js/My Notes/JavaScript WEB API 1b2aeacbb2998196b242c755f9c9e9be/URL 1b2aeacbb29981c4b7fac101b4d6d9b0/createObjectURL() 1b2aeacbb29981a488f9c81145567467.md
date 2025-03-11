# createObjectURL()

The **`URL.createObjectURL()`** static method creates a string containing a URL representing the object given in the parameter.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API), except for [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API).

</aside>

The URL lifetime is tied to the `document` in the window on which it was created. The new object URL represents the specified `File` object or `Blob` object.

To release an object URL, call `revokeObjectURL()`.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is *not* available in Service Workers due to its potential to create memory leaks.

</aside>

## Syntax

```jsx
URL.createObjectURL(object)
```

## Parameters

- object: A `File`, `Blob`, or `MediaSource` object to create an object URL for.

## Return value

A string containing an object URL that can be used to reference the contents of the specified source `object`.

## Example: Using object URLs to display images

This example uses object URLs to display image thumbnails. In addition, it displays other file information including their names and sizes.

The HTML that presents the interface looks like this:

```html
<input
  type="file"
  id="fileElem"
  multiple
  accept="image/*"
  style="display:none" />
<a href="#" id="fileSelect">Select some files</a>
<div id="fileList">
  <p>No files selected!</p>
</div>
```

This establishes our file `<input>` element as well as a link that invokes the file picker (since we keep the file input hidden to prevent that less-than-attractive user interface from being displayed). This is explained in the section Using hidden file input elements using the click() method, as is the method that invokes the file picker.

The `handleFiles()` method follows:

```jsx
const fileSelect = document.getElementById("fileSelect"),
  fileElem = document.getElementById("fileElem"),
  fileList = document.getElementById("fileList");

fileSelect.addEventListener(
  "click",
  (e) => {
    if (fileElem) {
      fileElem.click();
    }
    e.preventDefault(); // prevent navigation to "#"
  },
  false,
);

fileElem.addEventListener("change", handleFiles, false);

function handleFiles() {
  if (!this.files.length) {
    fileList.innerHTML = "<p>No files selected!</p>";
  } else {
    fileList.innerHTML = "";
    const list = document.createElement("ul");
    fileList.appendChild(list);
    for (let i = 0; i < this.files.length; i++) {
      const li = document.createElement("li");
      list.appendChild(li);

      const img = document.createElement("img");
      img.src = URL.createObjectURL(this.files[i]);
      img.height = 60;
      img.onload = () => {
        URL.revokeObjectURL(img.src);
      };
      li.appendChild(img);
      const info = document.createElement("span");
      info.innerHTML = `${this.files[i].name}: ${this.files[i].size} bytes`;
      li.appendChild(info);
    }
  }
}

```

This starts by fetching the URL of the `<div>` with the ID `fileList`. This is the block into which we'll insert our file list, including thumbnails.

If the `FileList` object passed to `handleFiles()` is `null`, we set the inner HTML of the block to display "No files selected!". Otherwise, we start building our file list, as follows:

1. A new unordered list (`<ul>`) element is created.
2. The new list element is inserted into the `<div>` block by calling its `Node.appendChild()` method.
3. For each `File` in the `FileList` represented by `files`:
    1. Create a new list item (`<li>`) element and insert it into the list.
    2. Create a new image (`<img>`) element.
    3. Set the image's source to a new object URL representing the file, using `URL.createObjectURL()` to create the blob URL.
    4. Set the image's height to 60 pixels.
    5. Set up the image's load event handler to release the object URL since it's no longer needed once the image has been loaded. This is done by calling the `URL.revokeObjectURL()` method and passing in the object URL string as specified by `img.src`.
    6. Append the new list item to the list.