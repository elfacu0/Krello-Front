<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import EditInput from "./EditInput.svelte";
    export let task: ITask = { id: 0, status: null, content: null };
    let error: string;
    let success: string;
    $: ({ id, content, status } = task);
    let editedContent = content;

    let editedStatus = status;
    const token: string = localStorage.getItem("token");

    $: editedStatus = status;

    $: handleSubmit = async () => {
        try {
            const response = await fetch("http://localhost:3000/tasks/edit", {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: `Bearer ${token}`,
                },
                body: JSON.stringify({
                    id,
                    content: editedContent,
                    status: editedStatus,
                }),
            });

            const data = await response.json();

            if (data.statusCode && data.statusCode !== 201) {
                error = data.message;
            } else {
                success = "Task Edited Successfully";
            }
        } catch (err) {
            error = err;
        }
    };

    const deleteTask = async () => {
        try {
            const response = await fetch("http://localhost:3000/tasks/delete", {
                method: "DELETE",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: `Bearer ${token}`,
                },
                body: JSON.stringify({ id }),
            });

            const data = await response.json();

            if (data.statusCode && data.statusCode !== 201) {
                error = data.message;
            } else {
                success = "Task Deleted Successfully";
            }
        } catch (err) {
            error = err;
        }
    };
</script>

<div class="modal-box">
    <h3 class="font-bold text-lg">Edit Task</h3>
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
        <EditInput
            label="Description"
            placeholder="Content"
            value={content}
            bind:editedContent
        />
        <select class="select select-bordered w-full" bind:value={editedStatus}>
            <option>TODO</option>
            <option>DOING</option>
            <option>COMPLETED</option>
        </select>
        <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
    </form>
    <div class="modal-action">
        <label for="my-modal-4" class="btn">Cancel</label>
    </div>
    <button class="btn btn-error" on:click={deleteTask}>Delete</button>
</div>
