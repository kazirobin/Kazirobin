# Regex For Password

This regex pattern **enforces password policies by requiring a minimum length of 8 characters and a mix of lowercase letters, uppercase letters, digits, and special characters**.

```jsx
/^(\S*$)(?=.*[0-9])(?=.*[A-Z])(?=.*[a-z])(?=.*[~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹])[a-zA-Z0-9~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹]{8,16}$/
```

A strong password will be of a minimum 8 characters to max range according to user need (max limit is set to 16 characters for this post). It must include the following:

1. Minimum 8 characters. `{8,20}`
2. Maximum 16 characters. `{8, 20}`
3. It must not contain any whitespace. `(\\S*$)`
4. At least one uppercase character `(?=.*[A-Z])`
5. At least one lowercase character `(?=.*[a-z])`
6. At least one digit `(?=.*\\d)`
7. At least one special character `(?=.*[~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹])[a-zA-Z0-9~`!@#$%^&*()--+={}\\[\\]|\\\\:;"'<>,.?/_₹]`

### Check Password Validity Function

```jsx
/**
 * @param {string} value: passwordValue
 */
const checkPasswordValidity = (value) => {
  const isNonWhiteSpace = /^(\S*$)/;
  if (!isNonWhiteSpace.test(value)) {
    return "Password must not contain Whitespaces.";
  }

  const isContainsUppercase = /^(?=.*[A-Z]).*$/;
  if (!isContainsUppercase.test(value)) {
    return "Password must have at least one Uppercase Character.";
  }

  const isContainsLowercase = /^(?=.*[a-z]).*$/;
  if (!isContainsLowercase.test(value)) {
    return "Password must have at least one Lowercase Character.";
  }

  const isContainsNumber = /^(?=.*[0-9]).*$/;
  if (!isContainsNumber.test(value)) {
    return "Password must contain at least one Digit.";
  }

  const isContainsSymbol = /^(?=.*[~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹]).*$/;
  if (!isContainsSymbol.test(value)) {
    return "Password must contain at least one Special Symbol.";
  }

  const isValidLength = /^.{10,16}$/;
  if (!isValidLength.test(value)) {
    return "Password must be 10-16 Characters Long.";
  }

  return null;
};

//------------------
// Usage/Example:
let yourPassword = "yourPassword123?";
const message = checkPasswordValidity(yourPassword);

if (!message) {
  console.log("Hurray! Your Password is Valid and Strong.");
} else {
  console.log(message);
}

```