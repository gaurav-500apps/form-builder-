<script setup>

</script>

<template>
    <header class="shadow-sm bg-white">
        <nav class="container mx-auto p-4 flex justify-between">
                <ul class="flex gap-4">
                    <li><NuxtLink to="/">Home</NuxtLink></li>
                    <li><NuxtLink to="/employee">Employee</NuxtLink></li>
                </ul>
        </nav>
    </header>
    <!-- Output the page content -->

    <div class="container mx-auto">
        <slot />
    </div>
</template> 


<style scoped>
.navbar {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}

.router-link-exact-active {
    color: teal;
}</style>