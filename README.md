# EJS (Embedded JavaScript) Documentation

## Overview

EJS is a simple templating language that lets you generate HTML markup with plain JavaScript. It works well with Node.js and allows you to embed JavaScript logic directly in your HTML.

## Table of Contents

1. [Installation](#installation)
2. [Basic Syntax](#basic-syntax)
3. [Displaying Data](#displaying-data)
4. [Variables](#variables)
5. [Comments](#comments)
6. [Control Flow (If Statements)](#control-flow-if-statements)
7. [Loops](#loops)
8. [Partials (Including Templates)](#partials-including-templates)
9. [Using External Data](#using-external-data)
10. [Custom Filters](#custom-filters)
11. [Error Handling](#error-handling)

---

## 1. Installation

To install EJS, you can use npm:

```bash
npm install ejs
```

Or, if you have an existing Node.js project, add it as a dependency:

```bash
npm install --save ejs
```

## 2. Basic Syntax

EJS syntax is similar to plain HTML but allows embedding JavaScript code using `<% %>` tags.

- `<%` - 'Scriptlet' tag for control-flow, no output.
- `<%=` - Outputs the value into the template (HTML escaped).
- `<%-` - Outputs the unescaped value into the template.
- `<%#` - Comment tag, no execution, no output.
- `<%%` - Outputs a literal `<%`.
- `%>` - Plain ending tag.

### Example

```ejs
<h1>Hello, <%= userName %>!</h1>
```

## 3. Displaying Data

You can use `<%= %>` to output data.

### Example

```ejs
<p>Your age is <%= age %> years old.</p>
```

## 4. Variables

EJS allows you to create and use variables within the template.

### Example

```ejs
<%
  const name = "John Doe";
  const age = 30;
%>

<p>Name: <%= name %></p>
<p>Age: <%= age %></p>
```

## 5. Comments

EJS provides a way to add comments within the template.

### Example

```ejs
<%# This is a comment and will not be rendered in the output %>
```

## 6. Control Flow (If Statements)

EJS allows you to use standard JavaScript if statements for conditional rendering.

### Example

```ejs
<% if (user.isAdmin) { %>
  <p>Welcome, Admin!</p>
<% } else { %>
  <p>Welcome, User!</p>
<% } %>
```

## 7. Loops

You can use loops like `for`, `while`, etc., to iterate over data and render it dynamically.

### Example (for loop)

```ejs
<ul>
  <% for (let i = 0; i < items.length; i++) { %>
    <li><%= items[i] %></li>
  <% } %>
</ul>
```

### Example (forEach)

```ejs
<ul>
  <% items.forEach(item => { %>
    <li><%= item %></li>
  <% }); %>
</ul>
```

## 8. Partials (Including Templates)

Partials allow you to include other EJS files within your template, enabling code reuse.

### Example

Create a header file `header.ejs`:

```ejs
<header>
  <h1>Site Header</h1>
</header>
```

Include it in your main file:

```ejs
<%- include('header') %>
```

## 9. Using External Data

You can pass data from your Express.js route to the EJS template.

### Example (Express.js route)

```javascript
app.get('/profile', function(req, res) {
  const user = { name: 'John', age: 30 };
  res.render('profile', { user });
});
```

### Example (EJS template)

```ejs
<h1>Name: <%= user.name %></h1>
<p>Age: <%= user.age %></p>
```

## 10. Custom Filters

EJS allows you to define custom filters for processing data before rendering.

### Example (Custom filter)

```javascript
ejs.filters.capitalize = function(str) {
  return str.charAt(0).toUpperCase() + str.slice(1);
};
```

### Example (Using custom filter)

```ejs
<p><%= capitalize(user.name) %></p>
```

## 11. Error Handling

You can handle errors in EJS by wrapping your code in try-catch blocks or by using a global error handler in your Node.js app.

### Example (try-catch)

```ejs
<% try { %>
  <p>Name: <%= user.name %></p>
<% } catch (err) { %>
  <p>Error: User name not found</p>
<% } %>
```

### Example (Global error handler in Express.js)

```javascript
app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

---