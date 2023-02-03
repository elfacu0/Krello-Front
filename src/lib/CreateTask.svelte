<script lang="ts">
    import Input from "./Input.svelte";
    let error: string;
    let success: string;
    let content: string;
    let status: string;
    const token: string = localStorage.getItem("token");
    export let updateTasks: () => {};

    $: handleSubmit = async () => {
        try {
            const response = await fetch("http://krello.fly.dev/tasks/create", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: `Bearer ${token}`,
                },
                body: JSON.stringify({ content, status }),
            });

            const data = await response.json();
            if (data.statusCode && data.statusCode !== 201) {
                error = data.message;
            } else {
                success = "Task created successfully";
                updateTasks();
            }
        } catch (err) {
            error = err;
        }
    };
</script>

<label for="my-modal-6" class="btn">CREATE TASK</label>
<input type="checkbox" id="my-modal-6" class="modal-toggle" />
<div class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
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
        <h3 class="font-bold text-lg">Create Task</h3>
        <form
            class="form-control card w-full bg-neutral shadow-xl p-8 flex
  justify-items-center justify-center"
            on:submit|preventDefault={handleSubmit}
            method="POST"
        >
            <Input
                label="Description"
                placeholder="Content"
                bind:value={content}
            />
            <select class="select select-bordered w-full" bind:value={status}>
                <option>TODO</option>
                <option>DOING</option>
                <option>COMPLETED</option>
            </select>
            <input
                type="submit"
                value="Submit"
                class="btn btn-secondary mt-8"
            />
        </form>
        <div class="modal-action">
            <label for="my-modal-6" class="btn">Cancel</label>
        </div>
    </div>
</div>
