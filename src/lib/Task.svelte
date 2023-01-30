<script lang="ts">
    import type { ITask } from "../interfaces/ITask";
    import EditTask from "./EditTask.svelte";
    export let task: ITask;
</script>

<li class="hover:bg-blue-500 rounded-box flex flex-col">
    <label for="my-modal-4" class="btn">
        <p>{task.content}</p>
    </label>
</li>

<input type="checkbox" id="my-modal-4" class="modal-toggle" />
<label for="my-modal-4" class="modal cursor-pointer">
    <label class="modal-box relative" for="">
        <EditTask {task}/>
    </label>
</label>
