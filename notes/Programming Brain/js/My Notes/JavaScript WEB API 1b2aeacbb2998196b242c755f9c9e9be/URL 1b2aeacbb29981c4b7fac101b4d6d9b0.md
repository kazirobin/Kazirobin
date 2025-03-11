# URL

The **`URL`** interface is used to parse, construct, normalize, and encode URLs. It works by providing properties that allow you to easily read and modify the components of a URL.

You normally create a new `URL` object by specifying the URL as a string when calling its constructor, or by providing a relative URL and a base URL. You can then easily read the parsed components of the URL or make changes to the URL.

If a browser doesn't yet support the `URL()` constructor, you can access a URL object using the `Window` interface's `URL` property. Be sure to check to see if any of your target browsers require this to be prefixed.

## Constructor

Creates and returns a `URL` object referencing the URL specified using an absolute URL string, or a relative URL string and a base URL string.

```jsx
const url = new URL("https://developer.mozilla.org");
```

## Instance Properties

[**hash Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/hash%20Property%201b2aeacbb29981a99972e02e4a52e9ea.md)

[**host Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/host%20Property%201b2aeacbb2998112b52cebf33484c8f8.md)

[**hostname Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/hostname%20Property%201b2aeacbb299812ebda4d7d9781efcdb.md)

[**href Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/href%20Property%201b2aeacbb29981faa6e0d15b9a35309f.md)

[**origin Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/origin%20Property%201b2aeacbb29981419a1aea7b97175c7d.md)

[**password Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/password%20Property%201b2aeacbb29981589831f8c8bab060c5.md)

[**pathname Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/pathname%20Property%201b2aeacbb29981e4af0ff4c1777ece41.md)

[**port Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/port%20Property%201b2aeacbb29981eeae88cd60c0a0c0de.md)

[**protocol Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/protocol%20Property%201b2aeacbb2998130960cd6f22361c5f5.md)

[**search Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/search%20Property%201b2aeacbb29981a68ef3e4af6a017f5c.md)

[**searchParams Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/searchParams%20Property%201b2aeacbb2998123bf44d82994777f68.md)

[**username Property**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/username%20Property%201b2aeacbb29981c68f24f47eeaf32329.md)

## Static Method

[**canParse()**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/canParse()%201b2aeacbb2998179b7e9f315b46282ad.md)

[**createObjectURL()**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/createObjectURL()%201b2aeacbb29981a488f9c81145567467.md)

[**revokeObjectURL()**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/revokeObjectURL()%201b2aeacbb2998193ac71c04b246717b4.md)

## Instance methods

[**toJSON()**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/toJSON()%201b2aeacbb29981fa93bbd37513a41124.md)

[**toString()**](URL%201b2aeacbb29981c4b7fac101b4d6d9b0/toString()%201b2aeacbb299814db54ef88f3b334ec3.md)