<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    export let task: ITask;
</script>

<li class="hover:bg-blue-500 rounded-box flex flex-col">
    <label for="my-modal-4" class="btn">
        <p>{task.content}</p>
    </label>
</li>
