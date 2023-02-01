<script lang="ts">
  import Input from "./Input.svelte";
  import PasswordInput from "./PasswordInput.svelte";
  export let username: string = "";
  let password: string = "";
  let error: string;

  $: handleLogin = async () => {
    try {
      const response = await fetch("http://localhost:3000/auth/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ username, password }),
      });
      const data = await response.json();

      if (data.statusCode && data.statusCode == 401) {
        error = data.message;
      } else {
        localStorage.setItem("token", data.access_token);
        localStorage.setItem("refreshToken", data.refresh_token);
        window.location.replace("/");
      }
    } catch (err) {
      error = err;
    }
  };
</script>

<form
  class="form-control card w-full bg-neutral shadow-xl p-8 flex
  justify-items-center justify-center"
  on:submit|preventDefault={handleLogin}
  method="POST"
>
  {#if error}
    <div class="alert alert-error shadow-lg">
      <div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="stroke-current flex-shrink-0 h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
          /></svg
        >
        <span>Error! {error}</span>
      </div>
    </div>
  {/if}
  <Input label="Username" placeholder="Place Username" bind:value={username} />
  <PasswordInput
    label="Password"
    placeholder="Place Password"
    bind:value={password}
  />
  <input type="submit" value="Login" class="btn btn-secondary mt-8" />
</form>
