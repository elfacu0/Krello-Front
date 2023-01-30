<script lang="ts">
    import { Router, Route } from "svelte-routing";
    import Navbar from "./lib/Navbar.svelte";
    import Login from "./pages/Login.svelte";
    import Home from "./pages/Home.svelte";
    import Register from "./pages/Register.svelte";
    import Logout from "./pages/Logout.svelte";

    let token = localStorage.getItem("leagueTable");
    let isLoggedIn: Boolean = token !== null;

    $: isLoggedIn = token !== null;
</script>

<body class="h-screen">
    <Navbar {isLoggedIn} />

    <Router>
        <div
            class="flex justify-items-center justify-center items-center h-full"
        >
            <Route component={Home} />
            <Route path="/login">
                <div class="container w-1/3 h-fit">
                    <Login />
                </div>
            </Route>
            <Route path="/register">
                <div class="container w-1/3 h-fit">
                    <Register />
                </div>
            </Route>
            <Route path="/logout">
                <Logout />
            </Route>
        </div>
    </Router>
</body>
