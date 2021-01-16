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
      destroyMemo(idx);
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
      newMemo: this.editMemo.memo,
      idx: this.editMemo.idx,
      show: false,
    };
  },
  props: ["editMemo"],
  emits: ["update","destroy"],
  methods: {
    updateMemo() {
      if (!this.newMemo) {
        return;
      }
      this.$emit("update", this.newMemo, this.idx);
      this.newMemo = ""
    },
    destroyMemo(idx) {
      if (!this.newMemo) {
        return;
      }
      this.$emit("destroy",idx)
      this.newMemo = "";
      this.idx = null;
    }
  }
};
</script>

<style>
textarea {
  resize: none;
}
</style>
