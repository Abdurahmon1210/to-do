<template>
  <button class="add__btn" @click="$emit('openModal')">
    <img src="@/assets/img/pen.svg" alt="" />
  </button>
</template>

<script>
export default {};
</script>

<style lang="scss">
.add__btn {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 16px;
  width: 56px;
  height: 56px;
  position: fixed;
  bottom: 30px;
  right: 30px;
  border: none;
  cursor: pointer;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15);
}
</style>