### What is XSS?

Cross-Site Scripting (XSS) is a vulnerability in web applications where an attacker can 
inject malicious scripts into content that other users will view. This can occur when 
user input is not properly sanitized and is then rendered by a web application. XSS can 
be used to steal session cookies, redirect users, or perform other malicious actions.

### Types of XSS

There are three main types of XSS attacks:

1. **Stored XSS**:
   - **Definition**: Malicious script is stored on the server (e.g., in a database) and 
is served to users who request the affected resource.
   - **Example**: A user comments on a blog post with a script that, when viewed by other 
users, executes and steals their session cookies.

2. **Reflected XSS**:
   - **Definition**: The malicious script is reflected off a web server, typically via 
URL parameters, and immediately executed.
   - **Example**: A malicious user tricks another user into clicking on a URL with a 
script in a query parameter, which gets executed and potentially steals data.

3. **DOM-based XSS**:
   - **Definition**: The vulnerability occurs in the client-side code, usually 
JavaScript, and the attack relies on manipulating the DOM (Document Object Model) in the 
browser.
   - **Example**: A script on the page reads data from the URL and inserts it into the 
page without proper sanitization, allowing an attacker to inject malicious code.

### Examples of XSS Attacks

#### 1. **Stored XSS Example**

**Scenario**: A web application allows users to submit comments on a blog post.

**Malicious Comment**:
```html
<script>alert('You have been hacked!');</script>
```

**Effect**: When other users view the blog post, the script executes in their browsers, 
showing an alert box.

**Mitigation**: Sanitize user input by escaping special characters and validating input 
on both client and server sides.

#### 2. **Reflected XSS Example**

**Scenario**: A search engine on a website reflects search terms in the search results 
page.

**Malicious URL**:
```
http://example.com/search?query=<script>alert('XSS');</script>
```

**Effect**: When the user clicks on this URL, the script executes in their browser, 
displaying an alert box.

**Mitigation**: Encode output, particularly any data that comes from URL parameters, 
before rendering it in the HTML.

#### 3. **DOM-based XSS Example**

**Scenario**: A web application takes user input from the URL and inserts it into the DOM 
without sanitizing it.

**JavaScript Code**:
```javascript
// Assume user input is passed as a URL parameter
var userInput = new URLSearchParams(window.location.search).get('userInput');
document.getElementById('display').innerHTML = userInput;
```

**Malicious URL**:
```
http://example.com/page?userInput=<img src=x onerror=alert('XSS')>
```

**Effect**: The `onerror` event handler triggers when the image fails to load, executing 
the script and showing an alert.

**Mitigation**: Avoid using `innerHTML` to insert user input. Use safer methods such as 
`textContent` or proper escaping.

### How to Prevent XSS

1. **Input Validation**: Always validate and sanitize user inputs. Ensure that inputs 
conform to expected formats and reject anything suspicious.

2. **Output Encoding**: Encode data before rendering it in HTML, JavaScript, or other 
contexts. For instance, use HTML entity encoding to prevent script injection.

3. **Content Security Policy (CSP)**: Implement CSP headers to restrict sources from 
which scripts can be loaded and executed.

4. **Use Libraries**: Utilize frameworks and libraries that provide built-in protection 
against XSS vulnerabilities. For example, React and Angular have mechanisms for safely 
handling user input.

5. **Sanitize User Input**: Ensure that user-generated content is sanitized both on the 
client side and server side. Use libraries or functions designed for this purpose.

### Summary

XSS is a critical security vulnerability that can have severe consequences if not 
properly addressed. Understanding its types and implementing robust defenses are 
essential for maintaining web application security.
