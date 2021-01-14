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
      addMemo();
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
  emits: ["update"],
  watch: {
    currentSelectedMemo: function () {
      this.idx = this.currentSelectedMemo.idx;
      this.newMemo = this.currentSelectedMemo.memo;
    },
    clickedAddMemo: function () {
      const content = "新規メモ";
      this.newMemo = content;
      this.idx = this.memos.length;
      this.addMemo();
      this.newMemo = content;
    },
  },
  methods: {
    addMemo() {
      if (!this.newMemo) {
        return;
      }
      this.memos[this.idx] = this.newMemo;
      this.saveMemos();
      this.$emit("update", this.memos);
    },
    saveMemos() {
      const parsed = JSON.stringify(this.memos);
      localStorage.setItem("memos", parsed);
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
