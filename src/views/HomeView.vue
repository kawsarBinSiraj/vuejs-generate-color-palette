<script setup>
import ColorPalate from "../components/ColorPalate.vue";
</script>

<template>
    <main id="home-page">
        <div class="container py-5">
            <div class="row">
                <div class="col-10 mx-auto">
                    <header id="header" class="mb-3">
                        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" height="80" />
                        <h2 class="mt-2 mb-0">Generate Awesome Color Palette with (Vue JS)</h2>
                        <var
                            >© Designed & Developed by
                            <a
                                href="https://kawsarbinsiraj.github.io/"
                                target="
                            "
                                class="text-primary"
                                >Kawsar Bin Siraj</a
                            >
                        </var>
                    </header>
                    <ColorPalate />
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>
.logo {
    display: block;
}
</style>
