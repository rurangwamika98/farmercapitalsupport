# Web Storage Assignment Reflection

**Names:** Mika Rurangwa, Effiong Uyo
**Date:** 19/03/2026

---

## 1. Resource Exploration Notes

After reviewing the provided resource on cookies, local storage, and session storage, We learned that all three are browser storage mechanisms used to improve user experience, remember preferences, and support faster web applications. The resource explains that cookies are small text files stored by websites, local storage keeps data in the browser for long-term use, and session storage keeps data only during the current browser session.

### Key Concepts

#### Cookies
- Cookies are small pieces of data stored in the browser.
- They are commonly used for login sessions, user preferences, personalization, and tracking.
- Cookies can be either:
  - **Session cookies**: removed when the browser closes.
  - **Persistent cookies**: remain until the expiration date.
- Cookies are sent with HTTP requests, so they can be accessed by both the browser and the server.
- Because cookies are sent with every request, they should stay small and only store necessary data.

#### Local Storage
- Local storage stores data as key-value pairs in the browser.
- It is useful for storing user preferences, cached data, and offline information.
- Data remains until it is manually removed.
- It has more storage space than cookies.
- Local storage is only available on the client side.

#### Session Storage
- Session storage also stores data as key-value pairs in the browser.
- It only keeps data during the current browser session.
- It is useful for temporary data, such as a shopping cart during one visit.
- It is also only available on the client side.

### Comparison Summary

| Storage Mechanism | Storage Limit | Data Retention | Accessibility | Common Use Cases |
|---|---:|---|---|---|
| Cookies | 4KB | Configurable | Client and server | Authentication, tracking, personalization |
| Local Storage | 5MB - 10MB | Permanent until cleared | Client only | Preferences, offline storage, caching |
| Session Storage | 5MB - 10MB | Until browser/tab closes | Client only | Temporary session data, carts |

### Security and Privacy Notes
- Cookies, local storage, and session storage can all be affected by **XSS attacks** if user input is not handled safely.
- Cookies are especially vulnerable to **CSRF attacks**, so CSRF tokens are important.
- Sensitive data like passwords or credit card details should not be stored in cookies, local storage, or session storage.
- Secure cookie flags such as **Secure** and **HttpOnly** help reduce risk.
- Expiration dates are important so data is not kept longer than needed.
- Complex objects in local storage should be saved using `JSON.stringify()` and read with `JSON.parse()`.

---

## 2. Questions Identified During Individual Review

These are the questions we identified while reviewing the resource:

1. Why are cookies still used for authentication if local storage has more space?
2. What is the difference between a session cookie and session storage?
3. Why is `HttpOnly` important for cookies?
4. Why should sensitive data not be stored in local storage or session storage?
5. What happens if local storage reaches the browser size limit?
6. Why is session storage a better choice for a temporary shopping cart?
7. How do CSRF tokens protect forms?
8. Why is `encodeURIComponent()` useful when handling user input?

---

## 3. Answers to Assignment Questions

### Task 1: User Authentication with Cookies

**Why are HttpOnly and Secure flags important for cookies?**  
`HttpOnly` helps protect cookies from JavaScript access, which reduces the risk of stolen cookies during XSS attacks. `Secure` makes sure that cookies are only sent over HTTPS, which protects them during transmission.

**How do session cookies differ from persistent cookies in this context?**  
Session cookies are deleted when the browser is closed. Persistent cookies remain in the browser until their expiration date is reached.

### Task 2: Theme Preferences with Local Storage

**What happens if local storage exceeds its size limit? How would you handle this?**  
If local storage exceeds the browser limit, the browser may throw a `QuotaExceededError`. I would handle this by using `try...catch`, saving only necessary data, and removing old or unused items.

**Why use JSON.stringify() and JSON.parse()?**  
Local storage saves data as strings. `JSON.stringify()` converts an object into a string before saving it, and `JSON.parse()` turns the string back into an object when reading it.

### Task 3: Session-Specific Shopping Cart

**Why is session storage suitable for this use case?**  
Session storage is suitable because it keeps data only for the current session. This matches a temporary shopping cart that should reset when the browser or tab closes.

### Task 4: Security Implementation

**Why sanitize input with encodeURIComponent()?**  
It helps reduce the risk of XSS by encoding special characters so they are treated as text instead of executable code.

**Why include a CSRF token in forms?**  
A CSRF token helps confirm that the request comes from the real form and not from a forged request made by another site.

**Why encrypt sensitive data in local storage?**  
If sensitive data must be stored, encryption helps reduce the risk of exposure. However, it is still better to avoid storing sensitive information in browser storage whenever possible.

### Task 5: Reflection and Comparison

**When would you use cookies over local storage?**  
Cookies are used when data needs to be sent to the server with every HTTP request. This is important for authentication systems, where cookies store session identifiers or tokens that allow the server to recognize users. In contrast, local storage is only accessible on the client side and is not automatically shared with the server.

**What are the risks of storing passwords in session storage?**  
Storing passwords in session storage isn’t safe because the data can be accessed using Javascript. It’s exposed to XXS attacks. And anyone with access to the browser could easily see stored passwords.

## 4. Final Challenge Reflection

In the final challenge, all storage mechanisms were combined into one application:

- **Cookies** were used for login authentication.
- **Local storage** was used to save the selected theme.
- **Session storage** was used to save shopping cart data during the current session.
- **Security measures** were added using input sanitization and a simulated CSRF token.

## 5. Collaborative Discussion Summary

During the collaborative discussion, we compared our notes from the resource and clarified the main differences between cookies, local storage, and session storage. We discussed why cookies are still important for authentication, even though local storage has more space. We also agreed that session storage is the best choice for a shopping cart that should reset after the session ends.

We reviewed security concerns together and concluded that:
- Cookies need Secure and HttpOnly flags for better protection.
- Browser storage should not contain sensitive information like passwords.
- CSRF tokens and encoded input are important security practices.

## 6. Final Summary

This activity helped us understand that cookies, local storage, and session storage are all useful, but each has a different purpose. Cookies are best when data must be shared with the server, local storage is best for long-term browser-based preferences, and session storage is best for temporary data during one browsing session. We also learned that security must always be considered, especially with XSS, CSRF, and sensitive data handling.
