# Registration-form
<!-- index.html -->
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Registration Form</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 24px; background:#f7f7f7; }
    .container { max-width:420px; margin: 30px auto; background:#fff; padding:20px; border-radius:8px; box-shadow:0 6px 18px rgba(0,0,0,0.08); }
    label { display:block; margin-top:12px; }
    input[type="text"], input[type="password"] { width:100%; padding:10px; margin-top:6px; box-sizing:border-box; border:1px solid #ccc; border-radius:4px; }
    .error { color:#b00020; font-size:0.9rem; margin-top:8px; }
    .success { color:green; font-size:0.95rem; margin-top:8px; }
    button { margin-top:18px; padding:10px 16px; border:none; background:#007bff; color:#fff; border-radius:6px; cursor:pointer; }
    button:disabled { background:#9bc1ff; cursor:not-allowed; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Register</h2>
    <form id="regForm" novalidate>
      <label for="username">Username</label>
      <input id="username" name="username" type="text" required minlength="3" placeholder="Choose a username" />

      <label for="password">Password</label>
      <input id="password" name="password" type="password" required minlength="6" placeholder="Enter password" />

      <label for="confirmPassword">Confirm Password</label>
      <input id="confirmPassword" name="confirmPassword" type="password" required minlength="6" placeholder="Re-enter password" />

      <div id="message" class=""></div>

      <button id="submitBtn" type="submit">Create account</button>
    </form>
  </div>

  <script>
    const form = document.getElementById('regForm');
    const username = document.getElementById('username');
    const password = document.getElementById('password');
    const confirmPassword = document.getElementById('confirmPassword');
    const msg = document.getElementById('message');
    const submitBtn = document.getElementById('submitBtn');

    function showError(text) {
      msg.className = 'error';
      msg.textContent = text;
    }
    function showSuccess(text) {
      msg.className = 'success';
      msg.textContent = text;
    }

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      msg.textContent = '';

      if (!username.value.trim()) {
        showError('Username is required.');
        return;
      }
      if (username.value.trim().length < 3) {
        showError('Username must be at least 3 characters.');
        return;
      }
      if (password.value.length < 6) {
        showError('Password must be at least 6 characters.');
        return;
      }
      if (password.value !== confirmPassword.value) {
        showError('Passwords do not match.');
        return;
      }

      // If you had a backend, you would send form data via fetch() here.
      // For now just show success message:
      showSuccess('Account created successfully (demo).');
      form.reset();
    });

    // Optional: disable submit until fields valid (basic)
    [username, password, confirmPassword].forEach(el => {
      el.addEventListener('input', () => {
        const ok = username.value.trim().length >= 3 &&
                   password.value.length >= 6 &&
                   password.value === confirmPassword.value;
        submitBtn.disabled = !ok;
      });
    });
    // initially disabled
    submitBtn.disabled = true;
  </script>
</body>
</html>
