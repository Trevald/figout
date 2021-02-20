<template>
    <div class="container">
        <h1>Figlout</h1>
        <p>
            Human friendly layout helper. Inspired by
            <a href="#" target="figma">Figmas</a> auto-layout.
        </p>

        <div class="sandbox">
            <Result
                :parentClassList="parentClassList"
                :childrenClassLists="childrenClassLists"
            />
            <Settings @parentChange="parentChange" @childrenChange="childrenChange" />
            <Source
                :parentClassList="parentClassList"
                :childrenClassLists="childrenClassLists"
            />
        </div>
    </div>
</template>

<script>
import Result from "./components/Result.vue";
import Settings from "./components/Settings.vue";
import Source from "./components/Source.vue";

export default {
    components: {
        Result,
        Settings,
        Source,
    },
    data() {
        return {
            parentClassList: [],
            childrenClassLists: [],
        };
    },

    methods: {
        parentChange(data) {
            this.parentClassList = data;
        },

        childrenChange(data) {
            this.childrenClassLists = data;
        },
    },
};
</script>

<style scoped>
.sandbox {
    margin-top: 3rem;
    width: 100%;
    display: grid;
    grid-template-areas:
        "result settings"
        "source source";
    grid-gap: 1.5rem;
    grid-template-columns: 1fr 15rem;
    grid-template-rows: minmax(400px, auto) auto;
}

.sandbox *:nth-child(1) {
    grid-area: result;
}

.sandbox *:nth-child(2) {
    grid-area: settings;
}

.sandbox *:nth-child(3) {
    grid-area: source;
}
</style>
