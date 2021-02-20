<template>
    <div :class="classList">
        <span class="a"></span>
        <span class="b"></span>
        <span class="c"></span>
    </div>
</template>

<script>
export default {
    name: "AlignmentIcon",

    props: {
        direction: String,
        distribution: String,
        isSelected: Boolean,
    },

    computed: {
        classList() {
            const classList = ["icon", "frame", this.direction, this.distribution];
            if (this.isSelected) {
                classList.push("selected");
            }
            return classList.join(" ");
        },
    },
};
</script>

<style></style>
