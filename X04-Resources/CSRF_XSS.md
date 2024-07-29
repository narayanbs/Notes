Cross-Site Request Forgery (CSRF) is a type of attack where a malicious actor tricks a user's 
browser into making unwanted requests to a web application where the user is authenticated. 
This can result in unintended actions being performed on behalf of the user.

### How CSRF Works

1. **Victim Authentication**: The victim logs into a web application and has an active session 
with that application. For example, they might be logged into their online banking account.

2. **Malicious Request**: While the user is still logged in, they visit a malicious website 
(or click on a link in an email, etc.) controlled by an attacker. This malicious site contains 
a script or HTML that generates a request to the target web application.

3. **Unintended Action**: Since the user's browser is already authenticated with the target 
web application (e.g., it has valid cookies or session tokens), the malicious request is sent 
with the user's credentials, potentially performing actions like transferring money, changing 
account settings, etc., without the user's consent.

### Example Scenarios

**Scenario 1: Banking Application**

1. **Victim's Bank Account**: User A is logged into their online banking account.
2. **Malicious Website**: User A visits a site controlled by an attacker that contains the 
following HTML form:
   ```html
   <form action="https://bank.example.com/transfer" method="POST">
     <input type="hidden" name="account" value="attacker_account"/>
     <input type="hidden" name="amount" value="1000"/>
     <input type="submit" value="Click Me"/>
   </form>
   <script>
     document.forms[0].submit();
   </script>
   ```
   When the form is submitted, it sends a POST request to the bank’s server to transfer 
money from User A's account to the attacker’s account.

3. **Result**: If the user is still authenticated with their banking site, the request is 
processed, and the money is transferred without User A’s knowledge.

**Scenario 2: Changing Account Settings**

1. **Victim's Account Settings**: User B is logged into a social media account that allows 
changing their email address.

2. **Malicious Email**: User B receives an email containing a link or an HTML form designed to 
update the email address. For example:
   ```html
   <img src="https://social.example.com/change-email?email=attacker@example.com" />
   ```
   The URL causes a request to change User B's email address to `attacker@example.com`.

3. **Result**: The request is sent with User B’s authentication token (stored in cookies or 
headers), and the email address is changed without User B’s knowledge.

### Preventing CSRF

1. **Anti-CSRF Tokens**: Implement a unique token for each request that is tied to the 
user’s session. This token must be included in requests that modify data (POST, PUT, DELETE 
requests). The server verifies the token before processing the request.
   ```html
   <input type="hidden" name="csrf_token" value="unique_token_value"/>
   ```

2. **SameSite Cookies**: Set the `SameSite` attribute on cookies to `Strict` or `Lax`, which 
restricts the browser from sending cookies along with cross-site requests.
   ```http
   Set-Cookie: sessionId=abc123; SameSite=Strict
   ```

3. **Referer Header Check**: Validate the `Referer` header to ensure that the request 
originates from a trusted source.

4. **Custom Headers**: Use custom headers (e.g., `X-Requested-With: XMLHttpRequest`) that are 
not normally included in cross-site requests.

By combining these methods, you can significantly reduce the risk of CSRF attacks.

--------------------------------------------------------

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
