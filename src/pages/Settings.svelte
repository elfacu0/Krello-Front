<script lang="ts">
    import Input from "../lib/Input.svelte";
    import PasswordInput from "../lib/PasswordInput.svelte";

    const token = localStorage.getItem("token");
    let error: string;
    let success: string;
    let email: string;
    let password: string;

    if (token == null) {
        window.location.replace("/");
    }

    $: handleSubmit = async () => {
        error = "";
        success = "";
        try {
            const response = await fetch("http://krello.fly.dev/users/edit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: `Bearer ${token}`,
                },
                body: JSON.stringify({ email, password }),
            });
            const data = await response.json();
            success = "Changes saved successfully";
        } catch (err) {
            error = err.message;
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
            <span>{error}</span>
        </div>
    </div>
{/if}

{#if success}
    <div class="alert alert-success shadow-lg">
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
                    d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                /></svg
            >
            <span>{success}</span>
        </div>
    </div>
{/if}

<form
    class="form-control card w-full bg-neutral shadow-xl p-8 flex
justify-items-center justify-center"
    on:submit|preventDefault={handleSubmit}
    method="POST"
>
    <Input label="Email" placeholder="Email" bind:value={email} />
    <PasswordInput
        label="Password"
        placeholder="Password"
        bind:value={password}
    />
    <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
</form>
