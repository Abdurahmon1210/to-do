<template>
  <div class="notes">
    <div class="container">
        <div class="notes__top">
            <h2 class="notes__title">{{ notes.length > 0 ? words.infobar[lang] : words.noinfobar[lang] }}</h2>
            <button class="notes__btn" @click="grid = !grid">
                <img src="@/assets/img/grid.svg" alt="" v-if="!grid">
                <img src="@/assets/img/list.svg" alt="" v-else>
                <span>{{grid ? words.list[lang] : words.grid[lang]}}</span>
            </button>
        </div>
        <div class="notes__list" :class="{ active: !grid }">
            <NotesItem 
            v-for="note in notes" 
            :key="note.id" 
            :note="note"
            :lang="lang"
            @changeNote="$emit('changeNote', note.id)"
            @delNote="$emit('delNote', note.id)"
            />
        </div>
    </div>
  </div>
</template>

<script>
import NotesItem from '@/components/NotesItem.vue';
export default {
    components:{
        NotesItem,
    },
    props:{
        notes:Array,
        lang:String
    },
    data(){
        return{
            grid: true,
        }
    },
    inject:['words']
};
</script>

<style>

</style>