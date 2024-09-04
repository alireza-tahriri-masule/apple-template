<script>
export default {
    data() {
        return {
            imgWidth: '18px',
            imgHeight: '18px',
            appleIcon: "/assets/images/apple.svg",
            bagIcon: "/assets/images/bag.svg",
            searchIcon: "/assets/images/search.svg",
            navItems: ['Phones', 'Macbooks', 'Tablets', 'Watches'],
        };
    }
};
</script>

<template>
    <header class="w-full py-5 sm:px-10 px-5 flex justify-between items-center">
        <nav class="flex w-full screen-max-width">
            <img :src="appleIcon" alt="Apple" :width="imgWidth" :height="imgHeight"/>

            <ul class="flex flex-1 justify-center max-sm:hidden">
                <li v-for="item in navItems" v-text="item" class="px-6 text-sm cursor-pointer text-gray hover:text-white transition-all"></li>
            </ul>

            <div class="flex items-baseline gap-7 max-sm:justify-end max-sm:flex-1">
                <img :src="searchIcon" alt="Search" :width="imgWidth" :height="imgHeight"/>
                <img :src="bagIcon" alt="Bag" :width="imgWidth" :height="imgHeight"/>
            </div>
        </nav>
    </header>
</template>
