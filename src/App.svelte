<script>
  import router from "page";
  import Signup from "./components/Signup.svelte";
  import Login from "./components/Login.svelte";
  import Home from "./components/home.svelte";

  let page;
  router("/", () => (page = Signup));
  router("/login", () => (page = Login));
  router("/signup", () => (page = Signup));
  router("/home", () => (page = Home));
  router("/logout", () => (page = Login));
  router.start();
</script>

<main>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>HTML + CSS</title>
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bulma@1.0.0/css/bulma.min.css"
    />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&display=swap"
      rel="stylesheet"
    />
  </head>
  <body>
    <svelte:component this={page} />
  </body>
</main>

<style>
  body {
    font-family: "Noto Sans", sans-serif;
    font-optical-sizing: auto;
    font-weight: 500;
    font-style: normal;
    font-variation-settings: "wdth" 100;
  }
</style>
