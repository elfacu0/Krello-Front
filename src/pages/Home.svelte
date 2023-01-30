<script lang="ts">
    import { onMount } from "svelte";
    import type { ITask } from "../interfaces/ITask";

    import Tasks from "../lib/Tasks.svelte";
    let data: Array<ITask> = [{content:"AAA",status:"TODO"},{content:"AAA",status:"TODO"}];

    onMount(async () => {
        const token: string = localStorage.getItem("token");
        const response = await fetch("http://localhost:3000/users/tasks", {
            method: "GET",
            headers: {
                Authorization: `Bearer ${token}`,
            },
        });

        if (response.ok) {
            data = await response.json();
        }
    });
</script>

<Tasks {data} />
