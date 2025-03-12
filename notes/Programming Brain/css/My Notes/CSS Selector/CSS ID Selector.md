# CSS ID Selector

The ID selector selects an HTML element based on the value of its ID attribute.

Keep in mind that the ID of an element should be unique in a document, meaning there should only be one HTML element with that given ID value. You cannot use the same ID value on a different element besides that one.

To select an element with a specific ID, use the hash character, `#`, followed by the name of the ID value:

```css
#my_id {
    property: value;
}
```

The code above will match only the unique element with the ID value of `my_id`.

It's worth mentioning that it is best to try and limit the use of this selector and opt for using the class selector instead. Applying styles using the ID selector is not ideal because the styles are not reusable.