+++
title = 'Javascript'
date = 2024-12-08T23:50:08+05:30
draft = false
+++

## Colors in Javascript console [^1]

adding `%c` before text will print the text with css rules that are defined in next string argument in `console.log` invocation.
Works in Chrome 24+ and Firefox +31

```javascript
console.log('%c Oh my heavens! ', 'background: #222; color: #bada55', 'more text');
```

# References

[^1]:[google chrome - Colors in JavaScript console - Stack Overflow](https://stackoverflow.com/questions/7505623/colors-in-javascript-console)
