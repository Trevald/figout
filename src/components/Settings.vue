<template>
    <div class="box">
        <div class="settings">
            <div class="direction frame horizontal">
                <button
                    type="button"
                    class="only-icon"
                    :class="{ selected: isParentSelected('direction', 'vertical') }"
                    title="Vertical"
                    @click="setParentValue('direction', 'vertical')"
                >
                    <Icon name="arrow-down" />
                </button>
                <button
                    type="button"
                    class="only-icon"
                    title="Horizontal"
                    :class="{ selected: isParentSelected('direction', 'horizontal') }"
                    @click="setParentValue('direction', 'horizontal')"
                >
                    <Icon name="arrow-right" />
                </button>
            </div>

            <Alignment
                class="alignment"
                :direction="parent.direction"
                :distribution="parent.distribution"
                :horizontal="parent.horizontal"
                :vertical="parent.vertical"
                @changeAlignment="setAlignment"
            />

            <div class="distribution">
                <select v-model="parent.distribution" @change="emitParent">
                    <option v-for="(distribution, index) in distributions" :key="index">
                        {{ distribution }}
                    </option>
                </select>
            </div>

            <div class="child-sizes frame horizontal space-between">
                <ChildSize
                    v-for="(child, index) in children"
                    :key="index"
                    :values="child"
                    @sizeChange="
                        ($e) => {
                            sizeChange($e, index);
                        }
                    "
                />
            </div>
        </div>
    </div>
</template>

<script>
import Alignment from "./Alignment.vue";
import ChildSize from "./ChildSize.vue";
import Icon from "./Icon.vue";
export default {
    name: "Settings",

    components: {
        Alignment,
        ChildSize,
        Icon,
    },

    data() {
        return {
            parent: {
                direction: "horizontal",
                distribution: "packed",
                horizontal: "center",
                vertical: "middle",
            },
            children: [
                ["horizontal-hug-content", "vertical-hug-content"],
                ["horizontal-hug-content", "vertical-hug-container"],
                ["horizontal-hug-content", "vertical-hug-content"],
            ],
            distributions: ["space-between", "packed"],
        };
    },

    methods: {
        isParentSelected(key, value) {
            return this.parent[key] === value;
        },

        setAlignment(data) {
            this.parent.horizontal = data.horizontal;
            this.parent.vertical = data.vertical;
            this.emitParent();
        },

        setParentValue(key, value) {
            this.parent[key] = value;
            this.emitParent();
        },

        sizeChange(data, index) {
            this.children[index] = data;
            this.emitChildren();
        },

        emitParent() {
            const data = [
                "frame",
                this.parent.direction,
                this.parent.distribution,
                this.parent.horizontal,
                this.parent.vertical,
            ];

            this.$emit("parentChange", data);
        },

        emitChildren() {
            const data = this.children;

            this.$emit("childrenChange", data);
        },
    },

    mounted() {
        this.emitParent();
        this.emitChildren();
    },
};
</script>

<style>
@media (max-width: 30rem) {
    .settings {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: auto;
        grid-gap: 1rem;
        grid-template-areas:
            "alignment direction"
            "alignment distribution"
            "child-sizes child-sizes";
    }

    .direction {
        grid-area: direction;
    }

    .alignment {
        grid-area: alignment;
    }

    .distribution {
        grid-area: distribution;
    }

    .child-sizes {
        grid-area: child-sizes;
    }
}

.distribution {
    padding: 0.5rem;
}

.child-sizes {
    position: relative;
    padding: 1rem 0 0.5rem 0;
}

.child-sizes::before {
    content: "";
    position: absolute;
    top: 0;
    left: -0.5rem;
    right: -0.5rem;
    border-top: 1px solid var(--color-bg);
}
</style>
