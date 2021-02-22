<template>
    <div class="child-size-wrapper">
        <div class="child-size">
            <button
                v-for="(button, index) in buttons"
                :key="index"
                type="button"
                class="no-style"
                @click="handleClick(button)"
                @mouseover="setActive(button)"
                @mouseout="setInactive(button)"
                :class="getButtonClassNames(button)"
                :name="button"
            >
                <Icon size="small" :name="button" />
            </button>
            <div class="box-size" :class="getBoxClassNames"></div>
        </div>
    </div>
</template>

<script>
import Icon from "./Icon.vue";

export default {
    name: "ChildSize",

    components: {
        Icon,
    },

    props: {
        values: Array,
    },

    data() {
        return {
            activeButtons: [],
            buttons: ["chevron-up", "chevron-right", "chevron-down", "chevron-left"],
            horizontalButtons: ["chevron-right", "chevron-left"],
            verticalButtons: ["chevron-up", "chevron-down"],
        };
    },

    computed: {
        getBoxClassNames() {
            const classNames = [this.values[0], this.values[1]];
            if (this.activeButtons.length > 0) {
                classNames.push("active");
            }
            return classNames;
        },

        horizontal() {
            return this.values[0];
        },
        vertical() {
            return this.values[1];
        },
    },

    methods: {
        handleClick(name) {
            const direction = this.getDirection(name);
            switch (direction) {
                case "horizontal":
                    this.emitSizeChange([this.toggleValue(direction), this.vertical]);
                    break;
                case "vertical":
                    this.emitSizeChange([this.horizontal, this.toggleValue(direction)]);
                    break;
            }
        },

        toggleValue(direction) {
            return this[direction] === `${direction}-hug-content`
                ? `${direction}-fill-container`
                : `${direction}-hug-content`;
        },

        emitSizeChange(data) {
            this.$emit("sizeChange", data);
        },

        isActive(name) {
            return this.activeButtons.includes(name);
        },

        setActive(name) {
            if (this.isHorizontal(name)) {
                this.activeButtons.push(this.horizontalButtons[0]);
                this.activeButtons.push(this.horizontalButtons[1]);
            } else {
                this.activeButtons.push(this.verticalButtons[0]);
                this.activeButtons.push(this.verticalButtons[1]);
            }
        },

        getDirection(name) {
            return this.isHorizontal(name) ? "horizontal" : "vertical";
        },

        isHorizontal(name) {
            return this.horizontalButtons.includes(name);
        },

        isVertical(name) {
            return this.verticalButtons.includes(name);
        },

        setInactive(name) {
            this.activeButtons.length = 0;
        },

        getButtonClassNames(name) {
            const classList = [];
            if (this.isActive(name)) {
                classList.push("active");
            }
            return classList;
        },
    },
};
</script>

<style scoped>
.child-size-wrapper {
    position: relative;
    padding-bottom: 30%;
    width: 30%;
}

.child-size {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.box-size {
    flex: 0 0 45%;
    min-width: 45%;
    padding-bottom: 45%;
    border: var(--border);
    background-color: var(--color-bg-level-2);
}

.box-size.vertical-fill-container {
    padding-bottom: calc(100% - 2px);
}

.box-size.horizontal-fill-container {
    flex-basis: 100%;
    min-width: 100%;
}

.box-size.active {
    border-color: var(--color-fg-selected);
}

button {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 12px;
    min-width: 12px;
    color: var(--color-fg-muted);
}

button.active {
    color: var(--color-fg-selected);
    background-color: var(--color-border);
}

button[name="chevron-up"],
button[name="chevron-down"] {
    width: 40%;
    height: 20%;
    left: 50%;
    transform: translateX(-50%);
}

button[name="chevron-right"],
button[name="chevron-left"] {
    width: 20%;
    height: 40%;
    top: 50%;
    transform: translateY(-50%);
}

button[name="chevron-up"] {
    top: 1px;
}

button[name="chevron-right"] {
    right: 1px;
}

button[name="chevron-down"] {
    bottom: 1px;
}

button[name="chevron-left"] {
    left: 1px;
}
</style>
