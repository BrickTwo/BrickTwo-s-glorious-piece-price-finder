<template>
    <b-dropdown right v-if="options">
        <template v-slot:button-content>
            <span v-if="showFlags"
                ><img :src="getImgUrl(selectedLanguage)" width="20px"
            /></span>
            <span v-if="!showFlags">{{
                getLanguageName(selectedLanguage)
            }}</span>
            <span v-if="!selectedLanguage">{{ language }}</span>
        </template>
        <b-dropdown-item
            href="#"
            v-for="language in options"
            :key="language.value"
            :value="language.value"
            @click="changeLanguage(language.value)"
            ><img :src="getImgUrl(language.value)" width="20px" />
            {{ language.text }}
        </b-dropdown-item>
    </b-dropdown>
</template>

<script>
import { countryMixin } from '@/mixins/countryMixin';

export default {
    props: {
        showFlags: {
            type: Boolean,
        },
        countrySelected: {
            type: String,
        },
    },
    mixins: [countryMixin],
    data() {
        return {
            selectedLanguage: null,
            options: [],
        };
    },
    methods: {
        changeLanguage(value) {
            this.selectedLanguage = value;
            this.$store.commit('setLanguage', this.selectedLanguage);
            this.$emit('languageSelected', this.selectedLanguage);
        },
        getImgUrl(value) {
            return 'flags/' + value + '.png';
        },
    },
    watch: {
        countrySelected: function(val, oldVal) {
            this.options = [];
            this.COUNTRIES.filter(
                (country) => country.countryCode == val
            )[0].languages.forEach((language) => {
                this.options.push({
                    value: language.languageCode,
                    text: language.text,
                });
            });
            this.selectedLanguage = this.options[0].value;
            this.$store.commit('setLanguage', this.selectedLanguage);
            this.$emit('languageSelected', this.selectedLanguage);
        },
    },
    beforeMount() {
        this.selectedLanguage = this.$store.state.language;

        if (this.countrySelected) {
            //console.log(this.countrySelected);
            this.COUNTRIES.filter(
                (country) => country.countryCode == this.countrySelected
            )[0].languages.forEach((language) => {
                this.options.push({
                    value: language.languageCode,
                    text: language.text,
                });
            });
        }
    },
    computed: {
        language() {
            return browser.i18n.getMessage('selectCountry_language');
        },
    },
};
</script>
