<template>
    <div class="hero" :class="{dark: dark, left:left, textBlack:textBlack}" v-bind:style='{backgroundImage: "url(" + imgUrl(image) + ")", "backgroundPositionY": top }'>
        <h2 v-if="title">{{title}}</h2>
    </div>
</template>

<script>
var images = require.context('../assets/', false, /\.jpg$/)

export default {
    name: 'hero',
    methods: {
        imgUrl: function (path) {
            return images('./' + path)
        }
    },
    props: [
        'title',
        'image',
        'dark',
        'left',
        'textBlack',
        'top'
    ]
}
</script>

<style lang="scss">
@import "../styles/colors.scss";

.hero {
    display: flex;
    position: relative;
    height: 25em;

    justify-content: center;
    align-items: center;

    overflow: hidden;

    background: no-repeat center top fixed;
    background-size: cover;

    h2 {
        text-align: center;
        font-size: 3em;
    }

    &:after {
        content: " ";
        position: absolute;
        width: 150%;
        height: 8em;
        left: -25%;
        bottom: -4em;

        background-color: $background-light;

        transform: rotate(-3deg);
    }

    // Use the dark theme
    &.dark:after {
        background-color: $background-dark;
    }

    // Use the left corner
    &.left:after {
        transform: rotate(3deg);
    }

    // Use black text
    &.textBlack {
        color: $background-dark;
    }
}
</style>
