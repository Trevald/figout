<template>
    <div class="box">
        <div class="frame horizontal">
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
            :direction="parent.direction"
            :distribution="parent.distribution"
            :horizontal="parent.horizontal"
            :vertical="parent.vertical"
            @changeAlignment="setAlignment"
        />

        <select v-model="parent.distribution" @change="emitParent">
            <option v-for="(distribution, index) in distributions" :key="index">
                {{ distribution }}
            </option>
        </select>
    </div>
</template>

<script>
import Alignment from "./Alignment.vue";
import Icon from "./Icon.vue";
export default {
    name: "Settings",

    components: {
        Alignment,
        Icon,
    },

    data() {
        return {
            parent: {
                direction: "horizontal",
                distribution: "space-between",
                horizontal: "center",
                vertical: "top",
            },
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

        emitParent() {
            const data = [
                this.parent.direction,
                this.parent.distribution,
                this.parent.horizontal,
                this.parent.vertical,
            ];

            this.$emit("parentChange", data);
        },
    },

    mounted() {
        this.emitParent();
    },
};
</script>
