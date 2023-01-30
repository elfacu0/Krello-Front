<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import CreateTask from "./CreateTask.svelte";
    import Task from "./Task.svelte";

    export let data: Array<ITask>;
</script>

<div class="flex">
    <CreateTask />
    <div id="todo" class="card shadow-xl bg-base-200">
        <h2 class="text-center">TODO</h2>
        <ul
            class="menu w-56 bg-accent text-secondary-content p-2 rounded-box"
        >
            {#each data as task}
                {#if task.status == "TODO"}
                    <Task {task}></Task>
                {/if}
            {/each}
        </ul>
    </div>

    <div id="doing" class="card shadow-xl bg-base-200">
        <h2 class="text-center">DOING</h2>
        <ul
            class="menu w-56 bg-accent text-secondary-content p-2 rounded-box"
        >
            {#each data as task}
                {#if task.status == "DOING"}
                    <li class="hover:bg-blue-500 rounded-box">
                        <a href="/">{task.content}</a>
                    </li>
                {/if}
            {/each}
        </ul>
    </div>

    <div id="completed" class="card shadow-xl bg-base-200">
        <h2 class="text-center">COMPLETED</h2>
        <ul
            class="menu w-56 bg-accent text-secondary-content p-2 rounded-box"
        >
            {#each data as task}
                {#if task.status == "COMPLETED"}
                    <li class="hover:bg-blue-500 rounded-box">
                        <a href="/">{task.content}</a>
                    </li>
                {/if}
            {/each}
        </ul>
    </div>
</div>
