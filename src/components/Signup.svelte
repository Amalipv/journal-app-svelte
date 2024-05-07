<body>
  <nav>
    <a href="/login">Login</a>
  </nav>
  <div class="field">
    <label class="label" for="nameField">Name</label>
    <div class="control">
      <input
        id="nameField"
        class="input"
        type="text"
        placeholder="Text input"
      />
    </div>
  </div>

  <div class="field">
    <label class="label" for="pwdField">Password</label>
    <div id="pwdField" class="control has-icons-left has-icons-right">
      <input
        class="input is-success"
        type="password"
        placeholder="Text input"
      />
    </div>
  </div>

  <div class="field">
    <label class="label" for="emailField">Email</label>
    <div class="control" id="emailField">
      <input class="input is-danger" type="email" placeholder="Email input" />
    </div>
  </div>

  <div class="field is-grouped">
    <div class="control">
      <button class="button is-link">Submit</button>
    </div>
    <div class="control">
      <button class="button is-link is-light">Cancel</button>
    </div>
  </div>
</body>
