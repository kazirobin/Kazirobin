# Input Autofill Reset

This code is a CSS rule that targets the input elements when the browser autofills them. Autofill is a feature that allows browsers to automatically fill in form fields with previously entered data, such as usernames, passwords, and addresses.

```css
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
    -webkit-transition-delay: 9999s;
    transition-delay: 9999s;
}
```