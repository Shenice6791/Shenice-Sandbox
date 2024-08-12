# Simple Instructions and Code Snippets

## 1. **Creating a Basic HTML Page**

To create a basic HTML page, use the following structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Web Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is a basic HTML page.</p>
</body>
</html>

## 2. Adding CSS Styles

You can add CSS to style your HTML page. Here’s how to include an internal stylesheet:

<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
        }
        h1 {
            color: #007BFF;
        }
        p {
            font-size: 16px;
        }
    </style>
</head>

## 3. Writing JavaScript
Here’s a simple JavaScript snippet to display an alert when a button is clicked:
<body>
    <button onclick="showAlert()">Click Me!</button>

    <script>
        function showAlert() {
            alert('Button was clicked!');
        }
    </script>
</body>

## 4. Creating a Simple Form
Here’s an example of a basic HTML form:

<form action="/submit" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <button type="submit">Submit</button>
</form>
