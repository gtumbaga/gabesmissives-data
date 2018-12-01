# CSS Form Validation
---

So, I had no idea that we had new CSS Pseudo classes for form validation in HTML5 :o.
For example, you can create an input field of type "email":
```
<input id="myEmail" type="email" required>
```
And use CSS to style it if it is invalid:
```
input:invalid {
  border-color: red;
}
```

This blew my mind! lol.  BUT, to take it even further, you can use JS to verify your form, simply by checking `validity.valid` on the element.

Below is a short example:
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title></title>
    <style>
      input {
        border: solid 1px black;
      }
      input:invalid {
        border-color: red;
      }
    </style>
</head>
<body>
  <form>
    <input id="myEmail" type="email" required>
  </form>
  <button onclick="checkIfValid()">Check Validity</button>

  <script>
    const element = document.getElementById('myEmail');

    const checkIfValid = () => {
      const myAnswer = (element.validity.valid) ? "its valid!" : "not valid...";
      console.log(myAnswer);
    }


  </script>
</body>
</html>
```

---
sources:
- https://css-tricks.com/form-validation-ux-html-css/
