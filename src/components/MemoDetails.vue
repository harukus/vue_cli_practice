<template>
  <p>一覧</p>
  <nav class="menu">
    <ul>
      <li v-for="(memo, idx) in memos" v-bind:key="idx">
        <a
          href="#"
          v-on:click="
            handleEditMemo(memo, idx);
          "
          >{{ memo.split("\n")[0] }}</a
        >
      </li>
    </ul>
  </nav>
  <button
    v-on:click="
      handleCreateMemo();
    "
  >
    +
  </button>
</template>
<script>
export default {
  props: ["memos"],
  emits: ["editMemo", "createMemo"],
  methods: {
    handleEditMemo(memo, idx) {
      this.$emit("editMemo", memo, idx);
    },
    handleCreateMemo() {
      this.$emit("createMemo");
    }
  },
};
</script>
<style>
p {
  text-align: center;
}
.menu {
  margin-left: 20px;
  width: 90%;
  height: 55%;
  overflow: scroll;
  border-color: rgb(92, 119, 241);
  border-width: 1px;
  border-style: outset;
  background-color: rgb(219, 223, 241);
}
</style>
