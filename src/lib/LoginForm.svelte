<script lang="ts">
  import Input from "./Input.svelte";
  import PasswordInput from "./PasswordInput.svelte";
  let username: string = "";
  let password: string = "";
</script>

<div class="form-control card w-full bg-neutral shadow-xl p-8 flex justify-items-center justify-center">
  <Input label="Username" placeholder="Place Username" value={username} />
  <PasswordInput label="Password" placeholder="Place Password" value={password} />
  <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
</div>
