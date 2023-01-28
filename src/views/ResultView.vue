<template>
    <v-app id="unscrollable">
        <v-card :href=url><v-card-title>お前らはここに行け</v-card-title>
            <v-card-subtitle>{{ name }}</v-card-subtitle>
            <iframe :src=src allowfullscreen loading="lazy"></iframe>
        </v-card>
    </v-app>
</template>
<script>
export default {
    name: 'ResultView',
    props: {
        src: {
            type: String,
            default: ""
        },
        url: {
            type: String,
            default: ""
        },
        name: {
            type: String,
            default: ""
        }
    },
}
</script>
<style>
iframe {
    width: 80%;
    aspect-ratio: 16/9;
}
</style>