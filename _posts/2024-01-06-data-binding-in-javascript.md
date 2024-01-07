---
layout: post
title: Data Binding in JavaScript
date: 2024-01-06 00:00:00 +0300
description: Example Description.
image: assets/img/data-binding-in-javascript.png
tags: []
published: false
---

Ill start with an example in React to show how a majority of readers come into contact with data binding.

```jsx
const myApp = () => {
  const [user, setUser] = useState({
    username: "jlangford",
    email: "mail@jlangford.com",
  });

  function onChangeEmail(e) {
    setUser({ ...user, email: e.target.value });
  }

  return (
    <div>
      <h1>{user.username}</h1>
      <input value={user.email} onChange={onChangeEmail} />
    </div>
  );
};
```

If you're familiar with React you've probably seen code like this before.

The line:

```jsx
<h1>{user.username}</h1>
```

is a representation of one-way data binding, meaning, the data we have is getting set on the page and does not change.

The line below:

```jsx
<input value={user.email} onChange={onChangeEmail} />
```

is an example of two-way data binding because we have set a value to the page element, but users can change the value, and expect the data model underneath to change as well. Also, if the value changes in our data model, all the elements referencing that value should reflect the changes.

## Vanilla

To get the same functionality without a library, getters and setters are used as a common design pattern.

Below is the full working example in HTML and JavaScript.

HTML

```html
<div>
  <h1 id="username"></h1>
  <label for="email">Email:</label>
  <input type="text" id="email" name="email" />
  <button onClick="clearEmail()">clear</button>
</div>
```

JavaScript

```javascript
const el = document.getElementById("email");

const user = {
  _username: "jlangford",
  _email: "mail@jlangford.com",

  get username() {
    return this._username;
  },

  get email() {
    return this._email;
  },

  set email(value) {
    this._email = value;
    el.value = value;
  },
};

function clearEmail() {
  user.email = "";
}

document.getElementById("username").innerHTML = user.username;

el.value = user.email;
el.addEventListener("change", (event) => {
  user.email = event.target.value;
});
```
