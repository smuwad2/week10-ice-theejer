<script>
export default {

    data() {
        return {
            soundEmojis: ['🔇', '🔈', '🔉', '🔊']
        }
    },
    // TODO: add code to define a necessary prop
    props: {
        soundLevel: {
            type: Number,
            default: 0
        }

    }
}
</script>

<template>
    <!-- TODO: add your template code here. Use span element. -->
    <span>{{ soundEmojis[soundLevel] }}</span>
</template>