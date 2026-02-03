<script>
    import Button from "$lib/Button.svelte";

    // Task 1
    const sayHello = () => alert("Hello!");
    const sayBye = () => alert("Goodbye!");
    const surprise = () => alert("Surprise!");

    // Task 2
    const groceries = ["Milk", "Eggs", "Bread", "Butter", "Cheese", "Fruits", "Vegetables"];

    // Task 3: API Calling
    let posts = [];
    let loading = false;
    let error = "";

    async function loadPosts() {
        loading = true;
        error = "";
        posts = [];

        try {
            const res = await fetch("https://jsonplaceholder.typicode.com/posts");
            
            if (!res.ok) {
                throw new Error(`Request failed: ${res.status}`);
            }

            posts = await res.json();
        } catch (err) {
            error = err?.message ?? "Something went wrong.";
        } finally {
            loading = false;
        }
    }
    // Auto-run once when the page loads (optional but nice)
    loadPosts();    
</script>

<div class="min-h-screen flex flex-col items-center justify-center gap-6 bg-gray-100">


    <!-- Task 1 Buttons -->
    <div class="flex flex-col items-center gap-6">
        <Button
        label="Hello"
        bgColor="bg-blue-500"
        onClick={sayHello}
    />
        <Button
        label="Bye"
        bgColor="bg-red-500"
        onClick={sayBye}
    />
        <Button
        label="Surprise Me"
        bgColor="bg-green-500"
        onClick={surprise}
    />
</div>

    <!-- Task 2 Grocery List -->
     <div class="w-full max-w-md rounded-2xl bg-white p-6 shadow-md">
        <h2 class="text-xl font-semibold mb-4">Grocery List</h2>
        
        <ul class="list-disc pl-6 space-y-2">
            {#each groceries as item}
            <li class="text-gray-800">{item}</li>
            {/each}
        </ul>
    </div>

    <!-- Task 3 API Calling -->
    <div class="w-full max-w-md rounded-2xl bg-white p-6 shadow-md">
    <div class="flex items-center justify-between mb-4">
        <h2 class="text-xl font-semibold">API Posts</h2>

        <Button
        class="!px-4 !py-2 rounded-lg bg-black text-white transition
        hover:opacity-90
        focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-black
        active:scale-95"
        on:click={loadPosts}
        >
        Refresh
        </Button>   
    </div>

        {#if loading}
            <p class="text-gray-600">Loading posts...</p>
        
        {:else if error}
            <p class="text-red-600">Error: {error}</p>"
        
        {:else}
        <ul class="space-y-2">
            {#each posts as post}
                <li class="border rounded-lg p-3 bg-gray-50">
                    <p class="font-medium">{post.title}</p>
                </li>
            {/each}
        </ul>
        {/if}
        
    </div>

</div>



