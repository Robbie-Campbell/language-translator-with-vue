<template>
    <div class="container h-100">
        <div class="text-center justify-content-center my-auto p-3 bg-light border">
            <h1 class="text-center">Language Translator!</h1>
            <form @submit.prevent="translateWord">
                <Languages name="from" @new-selected="updateLanguage"/>
                <Languages name="to" @new-selected="updateLanguage" />
                <h3>Insert Phrase to translate:</h3>
                <textarea v-model="word" type="text" placeholder="Input a sentence to translate!" />
                <p>Your original phrase was: {{untranslatedPhrase}}</p>
                <p :class="translation == 'not found' ? 'text-danger' : ''">The translation was: {{ translation }}</p>
                <button class="btn btn-success border">Translate the phrase or word</button>
            </form>
        </div>
    </div>
</template>
<script>
    import translate from "translate";
    import Languages from "./Languages.vue";
    export default {
        components: {
            Languages
        },
        data() {
            return {
                word: '',
                untranslatedPhrase: 'None',
                languageFrom: 'en',
                languageTo: 'en',
                translation: 'None',
            }
        },
        methods: {
            async translateWord() {
                translate.engine = "google";
                translate.key = process.env.VUE_APP_KEY;
                translate.from = this.languageFrom;
                const returnText = await translate(this.word, this.languageTo);
                this.untranslatedPhrase = this.word;
                await this.word == returnText ? this.translation = "not found" : this.translation = returnText;
                this.word = "";
            },
            updateLanguage(event, direction) {
                direction == "to" ? this.languageTo = event : this.languageFrom = event;
            },
        },
    }
</script>

<style scoped>
    .container {
        margin-top: 10%;
    }
</style>