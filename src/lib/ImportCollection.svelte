<script lang="ts">
    import InputNumber from "./InputNumber.svelte";
    export let updateTasks: () => {};

    const token = localStorage.getItem("token");
    let error: string;
    let success: string;
    let id: number = 1;

    $: handleSubmit = async () => {
        error = "";
        success = "";
        try {
            const response = await fetch(
                "http://krello.fly.dev/collections/import",
                {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        Authorization: `Bearer ${token}`,
                    },
                    body: JSON.stringify({ id }),
                }
            );
            const data = await response.json();
            if (data.statusCode && data.statusCode !== 200) {
                error = data.message;
            } else {
                success = "Collection Imported";
                updateTasks();
            }
        } catch (err) {
            error = err.message;
        }
    };
</script>

<label for="my-modal-8" class="btn">IMPORT COLLECTION</label>
<input type="checkbox" id="my-modal-8" class="modal-toggle" />
<div class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
        <h3 class="font-bold text-lg">Import Collection</h3>
        {#if error}
            <div class="alert alert-error shadow-lg">
                <div>
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="stroke-current flex-shrink-0 h-6 w-6"
                        fill="none"
                        viewBox="0 0 24 24"
                        ><path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
                        /></svg
                    >
                    <span>{error}</span>
                </div>
            </div>
        {/if}

        {#if success}
            <div class="alert alert-success shadow-lg">
                <div>
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="stroke-current flex-shrink-0 h-6 w-6"
                        fill="none"
                        viewBox="0 0 24 24"
                        ><path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                        /></svg
                    >
                    <span>{success}</span>
                </div>
            </div>
        {/if}
        <form
            class="form-control card w-full bg-neutral shadow-xl p-8 flex
        justify-items-center justify-center"
            on:submit|preventDefault={handleSubmit}
            method="POST"
        >
            <InputNumber value={id} label="Collection Id" placeholder="Id" />
            <input type="submit" value="Import" class="btn btn-primary mt-8" />
        </form>
        <div class="modal-action">
            <label for="my-modal-8" class="btn">Cancel</label>
        </div>
    </div>
</div>
