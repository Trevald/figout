<template>
    <svg :class="classNames" fill="none" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path
            v-if="iconIs('chevron-up')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 15l7-7 7 7"
        ></path>

        <path
            v-if="iconIs('chevron-right')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5l7 7-7 7"
        ></path>

        <path
            v-if="iconIs('chevron-down')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 9l-7 7-7-7"
        ></path>

        <path
            v-if="iconIs('chevron-left')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
        ></path>

        <path
            v-if="iconIs('arrow-right')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M14 5l7 7m0 0l-7 7m7-7H3"
        ></path>

        <path
            v-if="iconIs('arrow-down')"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 14l-7 7m0 0l-7-7m7 7V3"
        ></path>
    </svg>
</template>

<script>
export default {
    name: "Icon",

    props: {
        size: {
            type: String,
            default: "medium",
        },
        name: {
            type: String,
        },
    },

    computed: {
        classNames() {
            return this.size;
        },
    },

    methods: {
        iconIs(name) {
            return this.name.toLowerCase() === name.toLowerCase();
        },
    },
};
</script>

<style scoped>
svg {
    width: 20px;
    height: 20px;
}

svg path {
    stroke: currentColor;
}

svg.small {
    width: 12px;
    height: 12px;
}
</style>
