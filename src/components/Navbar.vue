<template>
  <header class="header">
    <Transition name="notes">
      <div class="header__notes" v-show="header">
        <button @click="changeLang" class="header__lang" v-if="lang == 'uz'">RU</button>
        <button @click="changeLang" class="header__lang" v-else>UZ</button>
        <h1 class="header__title">{{ words.appbartitle[lang] }}</h1>
        <button class="header__search" @click="header = !header">                    
          <img src="@/assets/img/search.svg" alt="" />           
        </button>
      </div>
    </Transition>
    <Transition name="form">
      <div class="header__form" v-show="!header">
        <button
          class="header__back"
          @click="(header = !header), (search = null)"
        >
          <img src="@/assets/img/back.svg" alt="" />
        </button>
        <input
          type="text"
          class="header__input"
          :placeholder="words.appbarsearch[lang]"
          v-model="search"
        />
        <button class="header__close" @click="search = null">
          <img src="@/assets/img/close.svg" alt="" />
        </button>
      </div>
    </Transition>
  </header>
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: null,
    };
  },
  watch:{
    search(value){
      this.$emit('searchValue', value)
    }
  },
  props:{
    lang:String
  },
  methods:{
    changeLang(){
      this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru')
    }
  },
  inject:['words']
};
</script>

<style>
</style>