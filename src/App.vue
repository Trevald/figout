<template>
    <div class="container">
        <h1>
            <svg viewBox="0 0 168 56" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M0.0823866 44H9.92614V27.6335H26.1136V19.6193H9.92614V11.267H27.8835V3.27273H0.0823866V44ZM31.7202 44H41.4446V13.4545H31.7202V44ZM36.5924 9.89489C39.3566 9.89489 41.5838 7.80682 41.5838 5.24148C41.5838 2.67613 39.3566 0.607952 36.5924 0.607952C33.848 0.607952 31.6009 2.67613 31.6009 5.24148C31.6009 7.80682 33.848 9.89489 36.5924 9.89489ZM60.7529 55.8324C69.9603 55.8324 76.2444 51.6364 76.2444 44.1193V13.4545H66.5597V18.6847H66.2813C65.108 15.8807 62.4432 13.0568 57.6307 13.0568C51.2472 13.0568 45.4603 17.9688 45.4603 28.6875C45.4603 39.0682 50.9688 43.5824 57.6705 43.5824C62.1648 43.5824 65.1677 41.4943 66.3211 38.6705H66.6591V44.0398C66.6591 47.6989 64.2728 49.0909 61.0114 49.0909C57.8893 49.0909 56.0199 47.8977 55.5029 46.267L46.2955 46.7841C47.0114 51.875 52.0427 55.8324 60.7529 55.8324ZM61.0512 36.5028C57.4518 36.5028 55.4432 33.5795 55.4432 28.6875C55.4432 23.8153 57.4319 20.6534 61.0512 20.6534C64.6109 20.6534 66.679 23.7358 66.679 28.6875C66.679 33.5994 64.591 36.5028 61.0512 36.5028ZM95.5825 44.5767C105.188 44.5767 111.014 38.233 111.014 28.8267C111.014 19.4006 105.188 13.0568 95.5825 13.0568C85.9774 13.0568 80.1507 19.4006 80.1507 28.8267C80.1507 38.233 85.9774 44.5767 95.5825 44.5767ZM95.6421 37.2386C92.0427 37.2386 90.0541 33.8182 90.0541 28.767C90.0541 23.696 92.0427 20.2557 95.6421 20.2557C99.1222 20.2557 101.111 23.696 101.111 28.767C101.111 33.8182 99.1222 37.2386 95.6421 37.2386ZM134.583 30.8153C134.583 34.375 132.316 36.3636 129.433 36.3636C126.45 36.3636 124.62 34.3352 124.6 31.0142V13.4545H114.876V32.9233C114.896 39.8239 119.092 44.3977 125.376 44.3977C129.95 44.3977 133.35 42.0511 134.703 38.3125H135.021V44H144.288V13.4545H134.583V30.8153ZM166.599 13.4545H161.09V6.13636H151.366V13.4545H147.329V20.6136H151.366V35.4688C151.306 41.6534 155.323 44.7557 162.184 44.4375C164.531 44.3182 166.221 43.8409 167.156 43.5625L165.684 36.5426C165.266 36.642 164.292 36.8409 163.556 36.8409C161.985 36.8409 161.09 36.2045 161.09 34.3949V20.6136H166.599V13.4545Z"
                />
            </svg>
        </h1>
        <p>
            Human friendly layout helper. Inspired by
            <a href="https://figma.com" target="figma">Figmas</a> auto-layout.
            <a href="./figout.css" download>Download CSS</a>
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
    <GitHubBanner />
</template>

<script>
import GitHubBanner from "./components/GitHubBanner.vue";
import Result from "./components/Result.vue";
import Settings from "./components/Settings.vue";
import Source from "./components/Source.vue";

export default {
    components: {
        GitHubBanner,
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
h1 svg {
    width: 168px;
    height: auto;
    fill: currentColor;
}

.sandbox {
    margin-top: 3rem;
    width: 100%;
    display: grid;
    grid-template-areas:
        "result settings"
        "source source";
    grid-gap: 0.5rem;
    grid-template-columns: 1fr 15rem;
    grid-template-rows: minmax(400px, auto) auto;
}

@media (min-width: 30rem) {
    .sandbox {
        grid-gap: 1.5rem;
    }
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
