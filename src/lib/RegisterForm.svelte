<script lang="ts">
  import Input from "./Input.svelte";
  import PasswordInput from "./PasswordInput.svelte";
  let username: string;
  let email: string = "";
  let password: string = "";
  let confirmPassword: string = "";

  const handleRegister = async () => {
    const response = await fetch("http://localhost:3000/auth/register", {
      method: "POST",
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({ username, email, password, confirmPassword }),
    });

    console.log(JSON.stringify({ username, email, password, confirmPassword }));
    
    const data = await response.json();

    if (data.error) {
      console.log(data.message);
    } else {
      console.log(data);
    }
  };
</script>

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
