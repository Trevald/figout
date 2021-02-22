<template>
    <div class="box">
        <pre v-html="code"></pre>
    </div>
</template>

<script>
export default {
    name: "Source",

    props: {
        parentClassList: Array,
        childrenClassLists: Array,
    },

    data() {
        return {
            parentClassListOld: [],
            childrenClassListsOld: [],
        };
    },

    computed: {
        code() {
            const parentClassList = this.addHello(
                [...this.parentClassList],
                [...this.parentClassListOld]
            );
            const childrenClassLists = this.addHelloToChildren();
            let code = `&#x3C;ul class="${parentClassList.join(" ")}"&#x3E;\n`;
            for (let i = 0; i < childrenClassLists.length; ++i) {
                code += `    &#x3C;li class="${childrenClassLists[i].join(
                    " "
                )}"&#x3E;&#x3C;/li&#x3E;\n`;
            }
            code += `&#x3C;/ul&#x3E;`;
            this.parentClassListOld = [...this.parentClassList];
            this.childrenClassListsOld = [...this.childrenClassLists];
            return code;
        },
    },

    methods: {
        addHelloToChildren() {
            if (this.childrenClassLists.length === this.childrenClassListsOld.length) {
                console.log("addHelloToChildren");
                const result = [];
                for (let i = 0; i < this.childrenClassLists.length; i++) {
                    result.push(
                        this.addHello(
                            [...this.childrenClassLists[i]],
                            [...this.childrenClassListsOld[i]]
                        )
                    );
                }

                return result;
            } else {
                return [...this.childrenClassLists];
            }
        },

        addHello(newValue, oldValue) {
            if (newValue.length === oldValue.length) {
                for (let i = 0; i < newValue.length; i++) {
                    if (newValue[i] !== oldValue[i]) {
                        newValue[i] = `<span class="hello">${newValue[i]}</span>`;
                    }
                }
            }

            return newValue;
        },
    },
};
</script>

<style>
pre {
    transition: opacity 0.1s ease;
}

.hello {
    border-radius: 2px;

    padding: 2px;
    margin: -2px;
    position: relative;
    animation-name: helloAnimation;
    animation-duration: 1s;
    transition: none;
}

@keyframes helloAnimation {
    0% {
        background-color: transparent;
    }

    60% {
        background-color: var(--color-fg-selected);
    }

    100% {
        background-color: transparent;
    }
}

.text-change-enter-active,
.text-change-leave-active {
    animation-name: blink;
    animation-duration: 1s;
    animation-iteration-count: 2;
}

@keyframes blink {
    0% {
        opacity: 1;
    }

    50% {
        opacity: 0.25;
    }

    100% {
        opacity: 1;
    }
}
</style>
