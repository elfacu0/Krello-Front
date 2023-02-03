<script lang="ts">
    const token = localStorage.getItem("token");
    let error: string;
    let success: string;

    $: handleSubmit = async () => {
        error = "";
        success = "";
        try {
            const response = await fetch(
                "https://krello.fly.dev/collections/export",
                {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        Authorization: `Bearer ${token}`,
                    },
                }
            );
            const data = await response.json();
            if (data.statusCode && data.statusCode !== 201) {
                error = data.message;
            } else {
                success = "Collection created" + "\n ID = " + data.id;
            }
        } catch (err) {
            error = err.message;
        }
    };
</script>

<button on:click={handleSubmit}>
    <label for="my-modal-7" class="btn">CREATE COLLECTION</label>
</button>
<input type="checkbox" id="my-modal-7" class="modal-toggle" />
<div class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
        <h3 class="font-bold text-lg">Create Collection</h3>
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
        <div class="modal-action">
            <label for="my-modal-7" class="btn">Cancel</label>
        </div>
    </div>
</div>
