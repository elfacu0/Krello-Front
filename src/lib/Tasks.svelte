<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import CreateCollection from "./CreateCollection.svelte";
    import CreateTask from "./CreateTask.svelte";
    import EditTask from "./EditTask.svelte";
    import ImportCollection from "./ImportCollection.svelte";
    import Task from "./Task.svelte";

    export let data: Array<ITask>;
    let currentTask: ITask;
    const setCurrentTask = (task: ITask) => {
        currentTask = task;
    };
</script>

<div class="flex">
    <div class="flex flex-col">
        <CreateTask />
        <CreateCollection />
        <ImportCollection />
    </div>
    <div id="todo" class="card shadow-xl bg-base-200">
        <h2 class="text-center">TODO</h2>
        <ul class="menu w-56 bg-accent text-secondary-content p-2 rounded-box">
            {#each data as task}
                {#if task.status == "TODO"}
                    <button on:click={() => setCurrentTask(task)}>
                        <Task {task} />
                    </button>
                {/if}
            {/each}
        </ul>
    </div>

    <div id="doing" class="card shadow-xl bg-base-200">
        <h2 class="text-center">DOING</h2>
        <ul class="menu w-56 bg-accent text-secondary-content p-2 rounded-box">
            {#each data as task}
                {#if task.status == "DOING"}
                    <button on:click={() => setCurrentTask(task)}>
                        <Task {task} />
                    </button>
                {/if}
            {/each}
        </ul>
    </div>

    <div id="completed" class="card shadow-xl bg-base-200">
        <h2 class="text-center">COMPLETED</h2>
        <ul class="menu w-56 bg-accent text-secondary-content p-2 rounded-box">
            {#each data as task}
                {#if task.status == "COMPLETED"}
                    <button on:click={() => setCurrentTask(task)}>
                        <Task {task} />
                    </button>
                {/if}
            {/each}
        </ul>
    </div>
</div>

<input type="checkbox" id="my-modal-4" class="modal-toggle" />
<label for="my-modal-4" class="modal cursor-pointer">
    <EditTask task={currentTask} />
</label>
