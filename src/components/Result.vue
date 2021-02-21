<template>
    <div class="box">
        <ul :class="parentClassNames">
            <li
                v-for="(childClassNames, index) in childrenClassLists"
                :key="index"
                :class="getChildClassNames(index)"
            ></li>
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

    computed: {
        parentClassNames() {
            return this.parentClassList ? this.parentClassList.join(" ") : "";
        },
    },

    methods: {
        getChildClassNames(index) {
            return this.childrenClassLists[index];
        },
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
    margin: 0.25rem;
    padding: 0;
    min-width: min(3vw, 5rem);
    min-height: min(6vw, 5rem);

    border-radius: 2px;
    background-color: var(--color-fg-link);
}
@media (min-width: 30rem) {
    ul > li {
        margin: 0.5rem;
    }
}

.horizontal li:nth-child(1) {
    min-height: min(7vw, 6rem);
}

.horizontal li:nth-child(2) {
    min-height: min(11vw, 8rem);
}

.horizontal li:nth-child(3) {
    min-height: min(5vw, 4rem);
}

.vertical li:nth-child(1) {
    min-width: min(7vw, 6rem);
}

.vertical li:nth-child(2) {
    min-width: min(11vw, 8rem);
}

.vertical li:nth-child(3) {
    min-width: min(5vw, 4rem);
}
</style>
