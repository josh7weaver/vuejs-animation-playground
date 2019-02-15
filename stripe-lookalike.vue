<template>
    <main>
        <div>
            <button
                class="btn btn-primary"
                @click="show = !show">
                Show
            </button>
        </div>
        <br><br>

        <!--
            NOT using <transition> elements... like Stripe did
            This is a little easier to debug bc you can inspect the "before"
            state where with <transition> its added dynamically so tough to see
        -->
        <div class="scene pure-css">
            <div :class="{'show':show}" class="alert alert-info">
                Howdy! How cool is VueJS ?
            </div>
        </div>

        <!--
            Use <transition> elements w/ name
        -->
        <div class="scene transition">
            <transition name="swinger">
                <div v-show="show" class="alert alert-info">
                    Howdy! How cool is VueJS ?
                </div>
            </transition>
        </div>
    </main>
</template>

<script>
export default {
    name: 'Animations',
    data() {
        return {
            show: false,
        };
    },
};
</script>

<style lang="scss" scoped>
    main{
        background-color: dodgerblue;
        height: 100vh;
    }
    .alert{
        width: 300px;
        height: 300px;
        background: white;
    }
    .scene{
        perspective: 2000px;
        margin-bottom: 2em;
    }

    /* Pure css */
    .scene.pure-css .alert{
        opacity: 0;
        transform: rotateX(-15deg);
        transform-origin: 50% -50px;
        transition-property: transform, opacity;
        transition-duration: 200ms;
        transition-timing-function: ease-out;
        &.show{
            opacity: 1;
            transform: rotateX(0);
        }
    }

    /* Using transitions */
    .scene.transition{
        .swinger-enter,
        .swinger-leave-to{
            opacity: 0;
            transform: rotateX(-15deg);
            transform-origin: 50% -50px;
        }
        .swinger-enter-active,
        .swinger-leave-active{
            transition-property: transform, opacity;
            transition-duration: 200ms;
            transition-timing-function: ease-out;
        }
    }
</style>
