<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import Input from "./Input.svelte";
    let content: string;
    let status: string;
    const token: string = localStorage.getItem("token");

    $: handleSubmit = async () => {
        const response = await fetch("http://localhost:3000/tasks/create", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${token}`,
            },
            body: JSON.stringify({ content, status }),
        });

        const data = await response.json();
        console.log(data);

        if (data.error === undefined) {
        }
    };
</script>

<label for="my-modal-6" class="btn">CREATE TASK</label>
<input type="checkbox" id="my-modal-6" class="modal-toggle" />
<div class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
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
