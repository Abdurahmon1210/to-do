<template>
    <Navbar 
    @searchValue="this.search = $event" 
    :lang="lang"
    @changeLang="changeLang"
    />
    <Notes 
    :lang="lang"
    :notes="filterNotes" 
    @delNote="deleteNote"  
    @changeNote="changeNote"
    />
    <AddButton @openModal="modalOpen = true"/>
    <Modal 
    v-if="modalOpen" 
    @closeModal="closeModal" 
    :currentId="currentId"
    @addNote="addNote"
    :edit="edit"
    :lang="lang"
    :editNote="editNote"
    @changedNote="changedNote"
    />
    
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import AddButton from "@/components/AddButton.vue";
import Modal from "@/components/Modal.vue";
import Lang from "@/lang.js";
export default {
  components: {
    Navbar,
    Notes,
    AddButton,
    Modal,
   },
   data(){
    return{
      currentId:1,
      modalOpen:false,
      notes: [],
      search: "",
      edit:false,
      editNote:{},
      lang:'ru',
      langwords:{}
    };
   },
   methods:{
    changeLang(val){
      this.lang = localStorage.lang = val
    },
    closeModal(){
      this.modalOpen = false
      this.edit = false
    },
    addNote(item){
      this.notes.push(item);
      this.modalOpen = false;
    },
    deleteNote(id){
      let index = this.notes.findIndex(note => note.id == id)
      this.notes.splice(index, 1)
    },
    getNotes(){
      const localNotes = localStorage.getItem('notes')
      if (localNotes) {
        this.notes = JSON.parse(localNotes);
        this.currentId = this.notes.length - 1
      }
    },
    changeNote(){
      this.edit = this.modalOpen = true
      let pickedNote = this.notes.find(note=>note.id == id)
      this.editNote = pickedNote 
    },
    changedNote(editedNote){
      this.notes.forEach(note=>{
        if (note.id == editedNote.id) {
          note.title = editedNote.title
          note.text = editedNote.text
          note.date = editedNote.date
        }
      })
    }
  },
  computed:{
    filterNotes(){
      return this.search ? this.notes.filter(note=> note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes
    }
  },
  created(){
    this.getNotes(); 

    localStorage.lang = localStorage.lang || 'ru';
    this.lang = localStorage.lang || 'ru'
    this.langwords = Lang
    localStorage.words = JSON.stringify(this.langwords)
  },
  provide(){
    return{
      words: localStorage.words ? JSON.parse(localStorage.words) : Lang
    }
  },
   watch:{
    notes:{
      handler(newValue){
        localStorage.setItem('notes', JSON.stringify(this.notes))
      },
      deep:true,
    },
   },
};
</script>

<style>
</style>