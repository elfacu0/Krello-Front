<script lang="ts">
    export let value: number;
    export let label: string;
    export let placeholder: string;

</script>
     
<div class="form-control">
    <label class="label">
        <span class="label-text">{label}</span>
    </label>
    <input
        type="number"
        inputmode="numeric"
        min="1"
        placeholder="{placeholder}"
        class="input input-bordered input-accent max-w-s"
        bind:value={value}
    />
</div>
