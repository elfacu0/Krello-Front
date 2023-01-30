<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import Input from "./Input.svelte";
    export let task: ITask;
    let { content, status }: ITask = task;
    const token: string = localStorage.getItem("token");

    $: handleSubmit = async () => {
        const response = await fetch("http://localhost:3000/tasks/edit", {
            method: "PATCH",
            headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${token}`,
            },
            body: JSON.stringify({ content, status }),
        });

        const data = await response.json();

        if (data.error === undefined) {
        }
    };
</script>

<div class="modal-box">
    <h3 class="font-bold text-lg">Edit Task</h3>
    <form
        class="form-control card w-full bg-neutral shadow-xl p-8 flex
  justify-items-center justify-center"
        on:submit|preventDefault={handleSubmit}
        method="POST"
    >
        <Input label="Description" placeholder="Content" bind:value={content} />
        <select class="select select-bordered w-full" bind:value={status}>
            <option>TODO</option>
            <option>DOING</option>
            <option>COMPLETED</option>
        </select>
        <input type="submit" value="Submit" class="btn btn-secondary mt-8" />
    </form>
    <div class="modal-action">
        <label for="my-modal-4" class="btn">Cancel</label>
    </div>
</div>
