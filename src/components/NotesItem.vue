<template>
  <div class="notes__item">
    <div class="notes__item-top">
        <h3 class="notes__item-title">{{note.title}}</h3>
        <p class="notes__item-data">{{note.date}}</p>
    </div>
    <p class="notes__item-text">
        {{note.text}}
    </p>
    <div class="notes__item-buttons">
        <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
            <img src="@/assets/img/pen.svg" alt="">
            <span>{{ words.editbtn[lang] }}</span>
        </button>
        <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
            <img src="@/assets/img/del.svg" alt="">
            <span>{{ words.deledit[lang] }}</span>
        </button>
    </div>
  </div>
</template>

<script>
export default {
    props:{
        note:Object,
        lang:String
    },
    inject:['words']
};
</script>

<style>

</style>