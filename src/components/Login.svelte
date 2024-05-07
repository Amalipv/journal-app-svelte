<script>
  let userValues = {
    userEmail: "",
    userPwd: "",
  };
  function gotoHome() {
    window.location.href = "/home";
  }
  let loggedIn = false;

  async function callLoginApi(e) {
    console.log("Inside callLoginApi");
    let response = await fetch("http://localhost:8090/login", {
      method: "POST",
      body: JSON.stringify({
        useremail: userValues.userEmail,
        userpassword: userValues.userPwd,
      }),
      headers: {
        "Content-type": "application/json;charset=UTF-8",
      },
    });
    let data = await response.json();

    console.log(data);
    if (data.loginstatus === 200) {
      console.log("Insider");
      sessionStorage.setItem("uid", data.userid);
      console.log("uid - ", sessionStorage.getItem("uid"));
      loggedIn = true;
      window.location.pathname = "/home";
    }
  }
</script>

<body>
  <nav>
    <a href="/signup">Sign up</a>
  </nav>
  <form on:submit|preventDefault={callLoginApi}>
    <div class="field">
      <label class="label" for="emailField">Email</label>
      <div class="control">
        <input
          id="emailField"
          class="input is-success"
          type="email"
          placeholder="Enter your email"
          bind:value={userValues.userEmail}
        />
      </div>
    </div>

    <div class="field">
      <label class="label" for="pwdField">Password</label>
      <div class="control has-icons-left has-icons-right">
        <input
          id="pwdField"
          class="input is-success"
          type="password"
          placeholder="Text input"
          bind:value={userValues.userPwd}
        />
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
  </form>
</body>
