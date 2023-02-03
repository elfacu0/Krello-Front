<script lang="ts">
    import { onMount } from "svelte";
    import type { ITask } from "../interfaces/ITask";
    import Tasks from "../lib/Tasks.svelte";
    let data: Array<ITask> = [];

    const updateTasks = async()=>{
        const token: string = localStorage.getItem("token");
        const response = await fetch("https://krello.fly.dev/users/tasks", {
            method: "GET",
            headers: {
                Authorization: `Bearer ${token}`,
            },
        });

        if (response.ok) {
            data = await response.json();
        }     
    }

    onMount(() => updateTasks());

</script>

<Tasks {data} {updateTasks}/>
