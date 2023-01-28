<script lang="ts">
    import { Router, Route } from "svelte-routing";
    import Navbar from "./lib/Navbar.svelte";
    import Login from "./pages/+Login.svelte";
    import Home from "./pages/Home.svelte";
    import Register from "./pages/+Register.svelte";
    export let isLoggedIn: Boolean = false;
</script>

<body class="h-screen">
    <Navbar {isLoggedIn} />

    <Router>
        <div class="flex justify-items-center justify-center items-center h-full">
            <div class="container w-1/3 h-fit">
                <Route component={Home} />
                <Route path="/login">
                    <Login />
                </Route>
                <Route path="/register">
                    <Register />
                </Route>
            </div>
        </div>
    </Router>
</body>
