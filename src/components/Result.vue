<template>
    <div class="box">
        <ul class="frame" :class="parentClassList.join(' ')">
            <li :class="childrenClassLists[0].join(' ')"></li>
            <li :class="childrenClassLists[1].join(' ')"></li>
            <li :class="childrenClassLists[2].join(' ')"></li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Result",

    props: {
        parentClassList: Array,
        childrenClassLists: Array,
    },
};
</script>

<style scoped>
ul {
    flex: 1 1 auto;
    margin: 0;
    padding: 0;
    list-style: none;
}

ul > li {
    margin: 0.5rem;
    padding: 0;
    min-width: min(6vw, 5rem);
    min-height: min(6vw, 5rem);

    border-radius: 2px;
    background-color: var(--color-fg-link);
}
</style>
