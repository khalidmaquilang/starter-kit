<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Link } from '@inertiajs/vue3'

const showNavbar = ref(true)
const lastScrollPosition = ref(0)

const menus = [
    { name: 'Dashboard', url: route('dashboard'), active: route().current('dashboard') }
]

onMounted(() => {
    window.addEventListener('scroll', onScroll)
})
onUnmounted(() => {
    window.removeEventListener('scroll', onScroll)
})

const onScroll = () => {
    const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop
    if (currentScrollPosition < 0) {
        return
    }

    // Stop executing this function if the difference between
    // current scroll position and last scroll position is less than some offset
    if (Math.abs(currentScrollPosition - lastScrollPosition.value) < 40) {
        return
    }

    // Here we determine whether we need to show or hide the navbar
    showNavbar.value = currentScrollPosition < lastScrollPosition.value
    // Set the current scroll position as the last scroll position
    lastScrollPosition.value = currentScrollPosition
}
</script>

<template>
    <div>
        <div class="min-h-screen bg-base-200 pl-4 pr-4">
            <nav
                class="sticky nav-transition navbar bg-base-100 rounded-box shadow-lg"
                :class="showNavbar ? 'top-4' : 'navbar--hidden top-0'"
            >
                <div class="navbar-start">
                    <div class="dropdown">
                        <label tabindex="0" class="btn btn-ghost lg:hidden">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h8m-8 6h16" /></svg>
                        </label>
                        <ul tabindex="0" class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
                            <li v-for="menu in menus" :key="menu.name">
                                <Link class="normal-case"
                                      :class="{'btn-active': menu.active}"
                                      :href="menu.url"
                                >
                                    {{ menu.name }}
                                </Link>
                            </li>
                        </ul>
                    </div>

                    <Link class="btn btn-ghost normal-case text-xl hidden lg:flex" href="/">Starter Kit</Link>
                    <div class="ml-2 hidden lg:flex">
                        <Link v-for="menu in menus" :key="menu.name"
                              class="btn btn-ghost normal-case"
                              :class="{'btn-active': menu.active}"
                              :href="menu.url"
                        >
                            {{ menu.name }}
                        </Link>
                    </div>
                </div>
                <div class="navbar-center lg:hidden">
                    <Link class="btn btn-ghost normal-case text-xl" href="/">Starter Kit</Link>
                </div>

                <div class="navbar-end">
                    <div class="dropdown dropdown-end">
                        <label tabindex="0" class="btn btn-ghost avatar">
                            {{ $page.props.auth.user.name }}
                        </label>
                        <ul tabindex="0" class="mt-3 z-[1] p-2 shadow menu menu-sm dropdown-content bg-base-100 rounded-box w-52">
                            <li>
                                <Link
                                    :href="route('profile.edit')"
                                    class="justify-between"
                                    :class="{'btn-active': route().current('profile.edit')}"
                                >
                                    Profile
                                </Link>
                            </li>
                            <li>
                                <Link :href="route('logout')" method="post" as="button">
                                    Logout
                                </Link>
                            </li>
                        </ul>
                    </div>
                </div>
            </nav>
            <div class="mt-6">
                <main>
                    <slot />
                </main>
            </div>
        </div>
    </div>
</template>

<style scoped>
.nav-transition {
    transform: translate3d(0, 0, 0);
    transition: 0.1s all ease-out;
}

.nav-transition.navbar--hidden {
    box-shadow: none;
    transform: translate3d(0, -100%, 0);
}
</style>
