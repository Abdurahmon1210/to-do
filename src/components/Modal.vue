<template>
  <div class="modal" @click="$emit('closeModal')">
    <div class="modal__block" @click.stop>
      <h2 class="modal__title">
        {{ edit ? words.titlewindowedit[lang] : words.titlewindow[lang] }}
      </h2>
      <div class="modal__inputs">
        <label>
          <span>Title</span>
          <input v-model="title" type="text" placeholder="title" />
        </label>
        <label>
          <span>Content</span>
          <input v-model="text" type="text" placeholder="Content" />
        </label>
      </div>
      <div class="modal__buttons">
        <button class="modal__btn del" @click="$emit('closeModal')">
          {{words.closebtn[lang]}}
        </button>
        <button v-if="!edit" class="modal__btn edit" @click="addNote">
          {{words.addbtn[lang]}}
        </button>
        <button v-else class="modal__btn edit" @click="changeNote">
          {{words.editwindowbtn[lang]}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: null,
      text: null,
      id: this.currentId,
    };
  },
  props: {
    currentId: Number,
    edit: Boolean,
    editNote: Object,
    lang: String
  },
  inject:['words'],
  mounted(){
   if (this.edit) {
      this.title = this.editNote.title
      this.text = this.editNote.text
   }
  },
  methods: {
    addNote() {
      if (this.title != null && this.text != null) {
        const item = {
          id: this.id++,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", item);
        this.title = null;
        this.text = null;
      }
    },
    changeNote() {
      if (this.title != null && this.text != null) {
        const editNote = {
          id: this.editNote.id,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("changedNote", editNote);
        this.$emit("closeModal");
        this.title = null;
        this.text = null;
      }
    },
  },
};
</script>

<style>
</style>