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
            let code = `<ul class="${this.parentClassList.join(" ")}">\n\r`;
            for (let i = 0; i < this.childrenClassLists.length; ++i) {
                code += `    <li class="${this.childrenClassLists[i].join(" ")}"></li>\n\r`;
            }
            code += `</ul>`;
            return code;
        },
    },
};
</script>
