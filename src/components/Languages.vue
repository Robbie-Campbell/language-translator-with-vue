<template>
    <div class="p-2 border-bottom">
        <h5>Convert phrase {{name}}:</h5>
        <select name="countries" :key="name" @change="newValue($event)">
            <option v-for="(language, key) in languages" :value="key" :key="key">{{language}}</option>
        </select>
    </div>
</template>

<script>
export default {
    props: ["name"],
    data() {
        return {
            languages: {"en": "English", "es": "Spanish",
             "fr": "French", "de": "Germany", "el": "Greek",
             "it": "Italy"},
        }
    },
    methods: {
        newValue(event) {
            console.log(event.target.value);
            this.$emit('new-selected', event.target.value, this.name)
        }
    }
}
</script>