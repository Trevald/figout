<template>
    <div class="box">
        <pre>{{ code }}</pre>
    </div>
</template>

<script>
export default {
    name: "Source",

    props: {
        parentClassList: Array,
        childrenClassLists: Array,
    },

    computed: {
        code() {
            return `<ul class="${this.parentClassList.join(" ")}">
    <li class="${this.childrenClassLists[0].join(" ")}"></li>
    <li class="${this.childrenClassLists[1].join(" ")}"></li>
    <li class="${this.childrenClassLists[2].join(" ")}"></li>
</ul>`;
        },
    },
};
</script>
