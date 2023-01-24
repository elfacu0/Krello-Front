<script lang="ts">
    export let isLoggedIn: Boolean;
</script>

<div class="navbar bg-base-300">
    <div class="flex-1">
        <a class="btn btn-ghost normal-case text-xl" href="/">Krelo</a>
    </div>
    {#if isLoggedIn}
        <div class="flex-none gap-2">
            <div class="dropdown dropdown-end">
                <label tabindex="-1" class="btn btn-ghost btn-circle avatar">
                    <div class="w-10 rounded-full">
                        <img src="https://placeimg.com/80/80/people" />
                    </div>
                </label>
                <ul
                    tabindex="-1"
                    class="mt-3 p-2 shadow menu menu-compact dropdown-content bg-base-100 rounded-box w-52"
                >
                    <li><a href="/settings">Settings</a></li>
                    <li><a href="/logout">Logout</a></li>
                </ul>
            </div>
        </div>
    {/if}
    {#if isLoggedIn == false}
        <div class="flex-none gap-2">
            <a class="btn" href="/register">Register</a>
            <a class="btn" href="/login">Login</a>
        </div>
    {/if}
</div>
