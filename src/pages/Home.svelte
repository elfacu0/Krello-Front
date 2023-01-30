<script lang="ts">
    import { onMount } from "svelte";
    import type { ITask } from "../interfaces/ITask";

    import Tasks from "../lib/Tasks.svelte";
    let data: Array<ITask> = [
        { id: 1, content: "AAA", status: "TODO" },
        { id: 2, content: "AAA", status: "TODO" },
    ];

    data = [];
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
