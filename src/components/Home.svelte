<script>
  import moment from "moment";

  let userid = sessionStorage.getItem("uid");
  console.log("Logged in as - ", userid);
  let formValues = {
    userid: userid,
    entrydate: "",
    entrydetails: "",
  };
  formValues.entryDate = new Date().toLocaleDateString();
  let eDate = moment(formValues.entryDate).format("yyyy-MM-DD");
  let userSelectedDate = eDate;

  let serverreponse = {
    msg: "",
    resStatus: null,
  };
  var getEntries = async () => {
    console.log("Inside getEntries");
    let response = await fetch("http://localhost:8090/getEntry", {
      method: "POST",
      body: JSON.stringify({
        userid: userid,
        EntryDate: userSelectedDate,
      }),
      headers: {
        "Content-type": "application/json;charset=UTF-8",
      },
    });
    let data = await response.json();
    formValues = data;
    console.log("server returned ", formValues, data);
  };
  async function addEntry() {
    console.log(eDate, "-", userid);
    //call the api
    let response = await fetch("http://localhost:8090/registerEntries", {
      method: "POST",
      body: JSON.stringify({
        userid: parseInt(userid),
        EntryDate: eDate,
        EntryDetails: formValues.entrydetails,
      }),
      headers: {
        "Content-type": "application/json;charset=UTF-8",
      },
    });
    let data = await response.json();
    console.log(data);
    serverreponse.msg = data.msg;
    serverreponse.resStatus = data.reqstatus;
  }
</script>

<nav>
  <a href="/logout">Logout</a>
</nav>
<body>
  <div class="section">
    <div class="container is-max-desktop is-three-fifths is-offset-one-fifth">
      <h1 class="subtitle has-text-centered">My Diary</h1>
    </div>
  </div>
  <div class="card column is-three-fifths is-offset-one-fifth">
    <header class="card-header">
      <p class="card-header-title">Today's entry - {serverreponse.msg}</p>
      <button class="card-header-icon" aria-label="more options">
        <span class="icon">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </button>
    </header>
    <div class="card-content">
      <div class="content">
        <textarea
          class="textarea"
          placeholder="10 lines of textarea"
          rows="10"
          on:load={getEntries()}
          bind:value={formValues.entrydetails}
        ></textarea>
        <br />
        <time datetime="2016-1-1"> {formValues.entrydate}</time>
      </div>
    </div>
    <footer class="card-footer">
      <!-- svelte-ignore a11y-invalid-attribute -->
      <a
        href=""
        class="card-footer-item has-text-weight-medium"
        on:click={addEntry}>Save</a
      >
    </footer>
  </div>
</body>

<style>
  body {
    background-color: #ecf0f1;
    font-family: "Noto Sans", sans-serif;
    font-optical-sizing: auto;
    font-weight: 500;
    font-style: normal;
    font-variation-settings: "wdth" 100;
  }
  .card,
  .column {
    background-color: #f7f3e3;
  }
  .card-header-title {
    color: #6f1a07;
  }
  .textarea {
    background-color: #f7f3e3;
    color: #6f1a07;
  }
</style>
