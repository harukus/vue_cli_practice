<template>
  <p>編集</p>
  <textarea
    placeholder="Memoを入力"
    v-model="newMemo"
    rows="10"
    cols="30"
  ></textarea>
  <br />
  <input
    type="submit"
    value="編集"
    @click="
      updateMemo();
    "
  />
  <button
    v-on:click="
      removeTodo(idx);
    "
  >
    削除する
  </button>
</template>

<script>
export default {
  data() {
    return {
      memos: [],
      newMemo: null,
      idx: null,
      show: false,
    };
  },
  props: ["currentSelectedMemo", "clickedAddMemo"],
  emits: ["update","add"],
  watch: {
    currentSelectedMemo: function () {
      this.idx = this.currentSelectedMemo.idx;
      this.newMemo = this.currentSelectedMemo.memo;
    },
    clickedAddMemo: function () {
      const content = "新規メモ";
      console.log(` clickedAddMemo:  ${this.memos}`)
      this.newMemo = content;
      this.addMemo();
    },
  },
  methods: {
    updateMemo() {
      if (!this.newMemo) {
        return;
      }
      // this.memos[this.idx] = this.newMemo;
      this.$emit("update", this.newMemo, this.idx);
      this.newMemo = ""
    },
    addMemo(){
      if (!this.newMemo) {
        return;
      }
      this.$emit("add", this.newMemo);
      this.newMemo = ""
    },
    removeTodo(idx) {
      if (!this.newMemo) {
        return;
      }
      this.memos.splice(idx, 1);
      this.saveMemos();
      this.newMemo = "";
      this.idx = null;
    },
    switchFalse() {
      this.$emit("switchFalse");
    },
  }
};
</script>

<style>
textarea {
  resize: none;
}
</style>
