<template>
    <header class="header">
        <nav v-show="navShow" class="header__nav">

            <button class="header__nav-lang" @click="switchLang" >{{$i18n.locale}}</button>
            <h1 class="header__nav-title">{{$t('notes')}}</h1>
            <button class="header__nav-search" @click="navShow = !navShow">
                <img src="@/assets/images/search.svg" alt="">

            </button>

        </nav>
        <nav v-show="!navShow" class="header__search">
            <button @click="navShow = !navShow" class="header__search-back">
                <img src="@/assets/images/back.svg" alt="back">
            </button>
            <input type="text" class="header__search-input" :placeholder="$t('searchInput')" v-model="search" autofocus>
            <button class="header__search-clear" @click="clear">
                <img src="@/assets/images/close.svg" alt="back">
            </button>
        </nav>
    </header>
</template>

<script>
export default {
    data() {
        return {
            navShow: true,
            search: '',
        }
    },

    watch: {

        search(newVal){

            this.$emit('setSearch',newVal)

        }

    },

    methods: {
        clear() {

            this.search = ''

        },
        switchLang() {
            this.$i18n.locale === 'ru' ? this.$i18n.locale = 'eng' : this.$i18n.locale = 'ru'
            localStorage.lang = this.$i18n.locale
        }
    },
}
</script>

