## How do you handle HTML encoding in web development, and can you provide an example of when and how you might use it in code?

HTML encoding is a way of representing special characters in a webpage so that they can be displayed correctly by browsers. In HTML, certain characters like `<`, `>`, and `&` have special meanings. If we want to display these on a webpage without them being interpreted as HTML code, we need to use their encoded equivalents.

- `<` is encoded as `&lt;`
- `>` is encoded as `&gt;`
- `&` is encoded as `&amp;`

Assuming this as input from a form by the user:

```html
<p>User Comment: <span id="user-comment"></span></p>

<script>
  // User input containing special characters
  var userInput = '<script>alert("XSS attack");</script>';

  // Encode user input before displaying it on a webpage
  document.getElementById('user-comment').innerText = encodeHTML(userInput);

  // Function to perform encoding
  function encodeHTML(input) {
    return input.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
  }
</script>

input.replace(/&/g, '&amp;'):

This part of the code uses the replace method to search for all occurrences of the ampersand (&) in the input string (input) and replaces each occurrence with its HTML entity equivalent (&amp;).
The regular expression /&/g is used with the g flag, which means global replacement (replace all occurrences, not just the first one)

This is a common technique to prevent user input containing these characters from being interpreted as HTML and potentially causing security vulnerabilities, such as Cross-Site Scripting (XSS)