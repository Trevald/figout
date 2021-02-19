<template>
    <div class="alignment">
        <div class="selector" :class="classList">
            <button
                type="button"
                v-for="(option, index) in options"
                :key="index"
                @click="setAlignment(option)"
                title="getLabel(option)"
            >
                <span class="sr-only">{{ getLabel(option) }}</span>
                <AlignmentIcon
                    :direction="direction"
                    :distribution="distribution"
                    :is-selected="isSelected(option)"
                />
            </button>
        </div>
    </div>
</template>

<script>
import AlignmentIcon from "./AlignmentIcon.vue";

export default {
    name: "Alignment",

    props: {
        direction: String,
        distribution: String,
        horizontal: String,
        vertical: String,
    },

    components: {
        AlignmentIcon,
    },

    computed: {
        classList() {
            const direction = this.direction === "horizontal" ? "vertical" : "horizontal";
            const classList = [`is-${this.distribution}`, this.direction];
            return classList;
        },

        horizontalPositions() {
            return ["left", "center", "right"];
        },

        verticalPositions() {
            return ["top", "middle", "bottom"];
        },

        options() {
            if (this.isSpaceBetween()) {
                return [
                    ["left", "top"],
                    ["center", "middle"],
                    ["right", "bottom"],
                ];
            } else {
                return [
                    ["left", "top"],
                    ["center", "top"],
                    ["right", "top"],
                    ["left", "middle"],
                    ["center", "middle"],
                    ["right", "middle"],
                    ["left", "bottom"],
                    ["center", "bottom"],
                    ["right", "bottom"],
                ];
            }
        },
    },

    methods: {
        getLabel(option) {
            return `${(option[0], option[1])}`;
        },

        isSelected(option) {
            const { horizontal, vertical } = getAlignmentsFromOption(option);
            if (this.isSpaceBetween() && this.direction === "horizontal") {
                return vertical === this.vertical;
            } else if (this.isSpaceBetween() && this.direction === "vertical") {
                return horizontal === this.horizontal;
            } else {
                return horizontal === this.horizontal && vertical === this.vertical;
            }
        },

        setAlignment(option) {
            const { horizontal, vertical } = getAlignmentsFromOption(option);
            if (this.isSpaceBetween()) {
                switch (this.direction) {
                    case "horizontal":
                        this.emitAlignment({ vertical });
                        break;
                    case "vertical":
                        this.emitAlignment({ horizontal });
                        break;
                }
            } else {
                this.emitAlignment({ horizontal, vertical });
            }
        },

        emitAlignment(data) {
            const horizontal = data.horizontal || this.horizontal;
            const vertical = data.vertical || this.vertical;

            console.log(horizontal, vertical);
            this.$emit("changeAlignment", { horizontal, vertical });
        },

        isSpaceBetween() {
            return this.distribution === "space-between";
        },
    },
};

const getAlignmentsFromOption = (option) => {
    return {
        horizontal: option[0],
        vertical: option[1],
    };
};
</script>

<style>
.alignment {
    padding: 0.5rem;
}

.alignment > .selector {
    aspect-ratio: 1 / 1;
    background-color: var(--color-bg-level-2);
    border: 1px solid var(--color-border);
    border-radius: 2px;
}

.alignment .selector {
    display: grid;
    grid-template-columns: auto;
    grid-template-rows: auto;
}

.alignment .selector.is-space-between.vertical {
    grid-template-columns: repeat(3, 1fr);
}

.alignment .selector.is-space-between.horizontal {
    grid-template-rows: repeat(3, 1fr);
}

.alignment button {
    appearance: none;
    display: flex;
    flex: 1 1 auto;
    justify-content: stretch;
    align-items: stretch;
    width: 100%;

    margin: 0;
    padding: 0;
    box-shadow: none;
    background: transparent;
    border: none;
    border-radius: 0;

    transition: opacity 0.2s ease;
}

.alignment .selector.is-space-between.horizontal button {
    align-items: center;
}

.alignment .selector.is-space-between.horizontal button:first-child {
    align-items: flex-start;
}

.alignment .selector.is-space-between.horizontal button:last-child {
    align-items: flex-end;
}

.alignment .selector.is-space-between.horizontal .icon {
    flex: 1 1 auto;
}

.alignment .selector.is-space-between.vertical button {
    justify-content: center;
}

.alignment .selector.is-space-between.vertical button:first-child {
    justify-content: flex-start;
}

.alignment .selector.is-space-between.vertical button:last-child {
    justify-content: flex-end;
}

.alignment .selector.is-space-between.vertical .icon {
    flex: 0 0 auto;
}

.alignment .selector.is-packed {
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
}

/* 
    Icon
*/

.alignment .icon {
    display: flex;
    opacity: 0;
    transition: none;
}

.alignment button:hover .icon {
    opacity: 0.5;
}

.alignment .icon.selected {
    opacity: 1;
}

.alignment .icon span {
    display: block;
    margin: 0.25rem;
    width: 0.75rem;
    height: 0.75rem;
    background-color: var(--color-fg-selected);
}

/* 
    Icon : Space between
*/

.selector.is-space-between button:nth-child(2) .icon {
    align-items: center;
}

.selector.is-space-between.vertical button:nth-child(3) .icon {
    align-items: flex-end;
}

.selector.is-space-between.vertical .icon span:nth-child(1) {
    width: 1rem;
}

.selector.is-space-between.vertical .icon span:nth-child(2) {
    width: 1.5rem;
}

.selector.is-space-between.horizontal .icon span:nth-child(1) {
    height: 1rem;
}

.selector.is-space-between.horizontal .icon span:nth-child(2) {
    height: 1.5rem;
}

/* 
    Icon : Packed
*/

.selector.is-packed.horizontal button:nth-child(2),
.selector.is-packed.horizontal button:nth-child(5),
.selector.is-packed.horizontal button:nth-child(8) {
    justify-content: center;
}

.selector.is-packed.horizontal button:nth-child(3),
.selector.is-packed.horizontal button:nth-child(6),
.selector.is-packed.horizontal button:nth-child(9) {
    justify-content: flex-end;
}

.selector.is-packed.horizontal button:nth-child(4) .icon,
.selector.is-packed.horizontal button:nth-child(5) .icon,
.selector.is-packed.horizontal button:nth-child(6) .icon {
    align-items: center;
}

.selector.is-packed.horizontal button:nth-child(7) .icon,
.selector.is-packed.horizontal button:nth-child(8) .icon,
.selector.is-packed.horizontal button:nth-child(9) .icon {
    align-items: flex-end;
}

.selector.is-packed.vertical button:nth-child(2),
.selector.is-packed.vertical button:nth-child(5),
.selector.is-packed.vertical button:nth-child(8) {
    justify-content: center;
}

.selector.is-packed.vertical button:nth-child(4),
.selector.is-packed.vertical button:nth-child(5),
.selector.is-packed.vertical button:nth-child(6) {
    align-items: center;
}

.selector.is-packed.vertical button:nth-child(7),
.selector.is-packed.vertical button:nth-child(8),
.selector.is-packed.vertical button:nth-child(9) {
    align-items: flex-end;
}

.selector.is-packed.vertical button:nth-child(2) .icon,
.selector.is-packed.vertical button:nth-child(5) .icon,
.selector.is-packed.vertical button:nth-child(8) .icon {
    align-items: center;
}

.selector.is-packed.vertical button:nth-child(3),
.selector.is-packed.vertical button:nth-child(6),
.selector.is-packed.vertical button:nth-child(9) {
    justify-content: flex-end;
}

.selector.is-packed.vertical button:nth-child(3) .icon,
.selector.is-packed.vertical button:nth-child(6) .icon,
.selector.is-packed.vertical button:nth-child(9) .icon {
    align-items: flex-end;
}

.selector.is-packed.vertical .icon span:nth-child(1) {
    width: 1.25rem;
}

.selector.is-packed.vertical .icon span:nth-child(2) {
    width: 2rem;
}

.selector.is-packed.vertical .icon span:nth-child(3) {
    width: 1rem;
}

.selector.is-packed.horizontal .icon span:nth-child(1) {
    height: 1.25rem;
}

.selector.is-packed.horizontal .icon span:nth-child(2) {
    height: 2rem;
}

.selector.is-packed.horizontal .icon span:nth-child(3) {
    height: 1rem;
}
</style>
