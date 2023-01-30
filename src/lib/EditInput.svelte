<script lang="ts">
    export let value: string;
    export let label: string;
    export let placeholder: string;
    export let editedContent: string;

    $: editedContent = value;
</script>  
     
<div class="form-control">
    <label class="label">
        <span class="label-text">{label}</span>
    </label>
    <input
        type="text"
        placeholder="{placeholder}"
        class="input input-bordered input-accent max-w-s"
        bind:value={value}
    />
</div>
