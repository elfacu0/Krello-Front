<script lang="ts">
    import { Router, Route } from "svelte-routing";
    import Navbar from "./lib/Navbar.svelte";
    import Login from "./pages/Login.svelte";
    import Home from "./pages/Home.svelte";
    import Register from "./pages/Register.svelte";
    import Logout from "./pages/Logout.svelte";
    import Settings from "./pages/Settings.svelte";

    const { fetch: originalFetch } = window;
    window.fetch = async (...args) => {
        const [resource, config] = args;
        const response = await originalFetch(resource, config);

        if (response.status !== 200 && response.status !== 201) {
            const refreshToken = localStorage.getItem("refreshToken");
            const res = await originalFetch(
                "http://localhost:3000/auth/refresh",
                {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        Authorization: `Bearer ${refreshToken}`,
                    },
                }
            );
            const refreshTokenData = await res.json();

            if (refreshTokenData?.access_token) {
                token = refreshTokenData.access_token;
                localStorage.setItem("token", token);
                config.headers["Authorization"] = token;
            } else {
                return Promise.reject(response);
            }
        }
        return response;
    };

    let token = localStorage.getItem("token");

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
            <Route path="/settings">
                <div class="container w-1/3 h-fit">
                    <Settings />
                </div>
            </Route>
        </div>
    </Router>
</body>
