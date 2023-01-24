<script lang="ts">
  import Input from "./Input.svelte";
  import PasswordInput from "./PasswordInput.svelte";
  let username: string = "";
  let password: string = "";
  let confirmPassword: string = "";
</script>

<div class="form-control card w-full bg-neutral shadow-xl p-8 flex justify-items-center justify-center">
  <Input label="Username" placeholder="Place Username" value={username} />
  <PasswordInput label="Password" placeholder="Place Password" value={password} />
  <PasswordInput label="Confirm Password" placeholder="Repeat Password" value={confirmPassword} />
  <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
</div>
