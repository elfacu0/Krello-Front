<script lang="ts">
  import Input from "./Input.svelte";
  import PasswordInput from "./PasswordInput.svelte";
  let error: string;

  let username: string;
  let email: string = "";
  let password: string = "";
  let confirmPassword: string = "";

  const handleRegister = async () => {
    const response = await fetch("http://localhost:3000/auth/register", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ username, email, password, confirmPassword }),
    });

    console.log(JSON.stringify({ username, email, password, confirmPassword }));

    const data = await response.json();
    console.log(data);
    
    if (data.statusCode !== 201) {
      error = data.message;
    } else {
      window.location.replace("/");
    }
  };
</script>

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
<form
  class="form-control card w-full bg-neutral shadow-xl p-8 flex justify-items-center justify-center"
  on:submit={(e) => {
    e.preventDefault();
    handleRegister();
  }}
>
  <Input label="Username" placeholder="Place Username" bind:value={username} />
  <Input label="Email" placeholder="Place Email" bind:value={email} />
  <PasswordInput
    label="Password"
    placeholder="Place Password"
    bind:value={password}
  />
  <PasswordInput
    label="Confirm Password"
    placeholder="Repeat Password"
    bind:value={confirmPassword}
  />
  <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
</form>
