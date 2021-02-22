<template>
    <form class="theme-switch">
        <input
            type="radio"
            id="input-theme-light"
            name="input-theme"
            value="light"
            v-model="theme"
            @change="changeTheme"
        />
        <input
            type="radio"
            id="input-theme-dark"
            name="input-theme"
            value="dark"
            v-model="theme"
            @change="changeTheme"
        />
        <label for="input-theme-light" title="Switch to light theme">
            <span class="sr-only">Light theme</span>
            <svg
                viewBox="0 0 16 16"
                xmlns="http://www.w3.org/2000/svg"
                class="icon-light"
                aria-hidden="true"
            >
                <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M7.99998 1.60001C8.21215 1.60001 8.41563 1.68429 8.56566 1.83432C8.71569 1.98435 8.79998 2.18783 8.79998 2.40001V3.20001C8.79998 3.41218 8.71569 3.61566 8.56566 3.76569C8.41563 3.91572 8.21215 4.00001 7.99998 4.00001C7.7878 4.00001 7.58432 3.91572 7.43429 3.76569C7.28426 3.61566 7.19998 3.41218 7.19998 3.20001V2.40001C7.19998 2.18783 7.28426 1.98435 7.43429 1.83432C7.58432 1.68429 7.7878 1.60001 7.99998 1.60001ZM11.2 8.00001C11.2 8.8487 10.8628 9.66263 10.2627 10.2627C9.6626 10.8629 8.84867 11.2 7.99998 11.2C7.15128 11.2 6.33735 10.8629 5.73723 10.2627C5.13712 9.66263 4.79998 8.8487 4.79998 8.00001C4.79998 7.15131 5.13712 6.33738 5.73723 5.73726C6.33735 5.13715 7.15128 4.80001 7.99998 4.80001C8.84867 4.80001 9.6626 5.13715 10.2627 5.73726C10.8628 6.33738 11.2 7.15131 11.2 8.00001ZM10.8288 11.96L11.3944 12.5256C11.5453 12.6713 11.7473 12.752 11.9571 12.7501C12.1669 12.7483 12.3675 12.6642 12.5158 12.5159C12.6642 12.3675 12.7483 12.1669 12.7501 11.9571C12.7519 11.7474 12.6713 11.5453 12.5256 11.3944L11.96 10.8288C11.8091 10.6831 11.607 10.6024 11.3973 10.6043C11.1875 10.6061 10.9868 10.6902 10.8385 10.8386C10.6902 10.9869 10.6061 11.1875 10.6042 11.3973C10.6024 11.607 10.683 11.8091 10.8288 11.96ZM12.5248 3.47441C12.6748 3.62443 12.759 3.82787 12.759 4.04001C12.759 4.25214 12.6748 4.45558 12.5248 4.60561L11.96 5.17121C11.8862 5.24761 11.7979 5.30856 11.7003 5.35049C11.6027 5.39241 11.4977 5.41448 11.3915 5.41541C11.2853 5.41633 11.1799 5.39609 11.0816 5.35586C10.9833 5.31564 10.894 5.25624 10.8189 5.18112C10.7437 5.10601 10.6843 5.01669 10.6441 4.91837C10.6039 4.82005 10.5837 4.71471 10.5846 4.60848C10.5855 4.50226 10.6076 4.39729 10.6495 4.29968C10.6914 4.20208 10.7524 4.1138 10.8288 4.04001L11.3944 3.47441C11.5444 3.32443 11.7478 3.24018 11.96 3.24018C12.1721 3.24018 12.3756 3.32443 12.5256 3.47441H12.5248ZM13.6 8.80001C13.8121 8.80001 14.0156 8.71572 14.1657 8.56569C14.3157 8.41566 14.4 8.21218 14.4 8.00001C14.4 7.78783 14.3157 7.58435 14.1657 7.43432C14.0156 7.28429 13.8121 7.20001 13.6 7.20001H12.8C12.5878 7.20001 12.3843 7.28429 12.2343 7.43432C12.0843 7.58435 12 7.78783 12 8.00001C12 8.21218 12.0843 8.41566 12.2343 8.56569C12.3843 8.71572 12.5878 8.80001 12.8 8.80001H13.6ZM7.99998 12C8.21215 12 8.41563 12.0843 8.56566 12.2343C8.71569 12.3843 8.79998 12.5878 8.79998 12.8V13.6C8.79998 13.8122 8.71569 14.0157 8.56566 14.1657C8.41563 14.3157 8.21215 14.4 7.99998 14.4C7.7878 14.4 7.58432 14.3157 7.43429 14.1657C7.28426 14.0157 7.19998 13.8122 7.19998 13.6V12.8C7.19998 12.5878 7.28426 12.3843 7.43429 12.2343C7.58432 12.0843 7.7878 12 7.99998 12ZM4.03998 5.17121C4.11425 5.24553 4.20244 5.3045 4.29951 5.34475C4.39657 5.385 4.50061 5.40573 4.60569 5.40577C4.71077 5.40581 4.81483 5.38514 4.91192 5.34497C5.00902 5.30479 5.09725 5.24588 5.17158 5.17161C5.2459 5.09733 5.30487 5.00914 5.34512 4.91208C5.38537 4.81501 5.4061 4.71097 5.40614 4.60589C5.40617 4.50081 5.38551 4.39675 5.34534 4.29966C5.30516 4.20256 5.24625 4.11433 5.17198 4.04001L4.60558 3.47441C4.45469 3.32868 4.25261 3.24804 4.04285 3.24987C3.8331 3.25169 3.63245 3.33582 3.48412 3.48415C3.33579 3.63248 3.25166 3.83313 3.24984 4.04289C3.24801 4.25264 3.32865 4.45472 3.47438 4.60561L4.03998 5.17121ZM5.17118 11.96L4.60558 12.5256C4.45469 12.6713 4.25261 12.752 4.04285 12.7501C3.8331 12.7483 3.63245 12.6642 3.48412 12.5159C3.33579 12.3675 3.25166 12.1669 3.24984 11.9571C3.24801 11.7474 3.32865 11.5453 3.47438 11.3944L4.03998 10.8288C4.19086 10.6831 4.39294 10.6024 4.6027 10.6043C4.81245 10.6061 5.0131 10.6902 5.16143 10.8386C5.30976 10.9869 5.39389 11.1875 5.39571 11.3973C5.39754 11.607 5.3169 11.8091 5.17118 11.96ZM3.19998 8.80001C3.41215 8.80001 3.61563 8.71572 3.76566 8.56569C3.91569 8.41566 3.99998 8.21218 3.99998 8.00001C3.99998 7.78783 3.91569 7.58435 3.76566 7.43432C3.61563 7.28429 3.41215 7.20001 3.19998 7.20001H2.39998C2.1878 7.20001 1.98432 7.28429 1.83429 7.43432C1.68426 7.58435 1.59998 7.78783 1.59998 8.00001C1.59998 8.21218 1.68426 8.41566 1.83429 8.56569C1.98432 8.71572 2.1878 8.80001 2.39998 8.80001H3.19998Z"
                />
            </svg>
        </label>
        <label for="input-theme-dark" title="Switch to dark theme">
            <span class="sr-only">Dark theme</span>
            <svg
                viewBox="0 0 16 16"
                xmlns="http://www.w3.org/2000/svg"
                class="icon-dark"
                aria-hidden="true"
            >
                <path
                    d="M13.8345 10.6344C12.6493 11.1705 11.3289 11.3327 10.0492 11.0994C8.76945 10.8661 7.5912 10.2484 6.6714 9.32864C5.7516 8.40884 5.13392 7.2306 4.90064 5.9509C4.66737 4.67119 4.82958 3.35078 5.36566 2.16559C4.42211 2.592 3.59609 3.24094 2.95846 4.05676C2.32084 4.87257 1.89064 5.83089 1.70479 6.8495C1.51893 7.86811 1.58296 8.91661 1.89139 9.90503C2.19981 10.8935 2.74342 11.7923 3.47558 12.5245C4.20774 13.2566 5.10659 13.8002 6.09502 14.1087C7.08344 14.4171 8.13194 14.4811 9.15055 14.2953C10.1692 14.1094 11.1275 13.6792 11.9433 13.0416C12.7591 12.404 13.408 11.5779 13.8345 10.6344Z"
                />
            </svg>
        </label>
    </form>
</template>

<script>
export default {
    name: "ThemeSwitch",

    data() {
        return {
            theme: "dark",
        };
    },

    methods: {
        changeTheme() {
            document.documentElement.dataset.theme = this.theme;
        },
    },

    mounted() {
        this.changeTheme();
    },
};
</script>

<style>
.theme-switch {
    display: inline-block;
    position: relative;
    width: 6rem;
    height: 2rem;

    transform: translateY(-0.375rem);
}

.theme-switch svg {
    fill: currentColor;
}

.theme-switch input {
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: inset(50%);
    height: 1px;
    width: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
}

.theme-switch label {
    position: absolute;
    padding: 0.5rem 0.5rem;
    color: var(--color-fg-muted);
    transition: color 0.2s ease;
    font-size: 1px;
    line-height: 1px;
}

.theme-switch label:hover {
    color: var(--color-fg);
}

.theme-switch label svg {
    width: 1rem;
    height: auto;
}

.theme-switch label[for="input-theme-light"] {
    left: 0;
    padding-right: 1.5rem;
}

.theme-switch label[for="input-theme-dark"] {
    right: 0;
    padding-left: 1.5rem;
}

.theme-switch label[for="input-theme-light"]::before,
.theme-switch label[for="input-theme-dark"]::before {
    position: absolute;
    top: 0.5625rem;

    content: "";
    display: block;
    width: 0.75rem;
    height: 0.75rem;

    background-color: var(--color-bg-level-1);
    border: var(--border);
}

.theme-switch label[for="input-theme-light"]::before {
    right: 0;
    border-top-left-radius: 50%;
    border-bottom-left-radius: 50%;
    border-right: none;
}

.theme-switch label[for="input-theme-dark"]::before {
    left: 0;
    border-top-right-radius: 50%;
    border-bottom-right-radius: 50%;
    border-left: none;
}

.theme-switch label[for="input-theme-dark"]::after {
    position: absolute;
    top: 0.75rem;
    right: 1.625rem;
    content: "";
    display: block;
    width: 0.5rem;
    height: 0.5rem;
    border-radius: 0.5rem;
    background-color: var(--color-fg-muted);
    transition: transform 0.2s ease-out;
    transform: translateX(-1.5rem);
}

.theme-switch input[id="input-theme-dark"]:checked ~ label[for="input-theme-dark"]::after {
    transform: translateX(-0.75rem);
}

.theme-switch input[id="input-theme-dark"]:not(:checked) ~ label[for="input-theme-light"] {
    color: var(--color-fg-selected);
}

.theme-switch input[id="input-theme-dark"]:checked ~ label[for="input-theme-dark"] {
    color: var(--color-fg-selected);
}
</style>
