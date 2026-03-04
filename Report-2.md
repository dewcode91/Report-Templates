# Disclosure of Hidden Admin-Panel Path via JavaScript

## Description

Relying on "security by obscurity" — such as hiding sensitive admin functionality by using a non-obvious URL — does not provide effective protection. If the obfuscated URL is referenced in client-side JavaScript, it can be easily discovered by reviewing the site’s source code.

For instance, an admin panel at:

```
https://insecure-website.com/administrator-panel-yb556
```

may appear unguessable, but if its URL appears in accessible JavaScript, all users (including unauthorized ones) can find it:

```javascript
<script>
var isAdmin = false;
if (isAdmin) {
  var adminPanelTag = document.createElement('a');
  adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
  adminPanelTag.innerText = 'Admin panel';
}
</script>
```
This snippet exposes the admin panel URL to any user inspecting the website’s source.

## Steps to Reproduce

1. Open the site homepage and view its source (`view-source:` URI prefix).
2. Search for JavaScript variables or links referencing the admin panel (e.g., `/administrator-panel-yb556`).
3. Access the exposed admin panel URL directly.

## Impact

Exposing hidden admin URLs allows low-privilege users or attackers to discover and potentially access sensitive administrative features. This undermines access controls, enabling privilege escalation and unauthorized administrative actions, which can compromise the system’s security.
