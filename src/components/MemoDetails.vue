<template>
  <p>一覧</p>
  <nav class="menu">
    <ul>
      <li v-for="(memo, idx) in memos" v-bind:key="memo">
        <a
          href="#"
          v-on:click="
            select(memo, idx);
          "
          >{{ memo.split("\n")[0] }}</a
        >
      </li>
    </ul>
  </nav>
  <button
    v-on:click="
      handleClickedAddMemo();
    "
  >
    +
  </button>
</template>
<script>
export default {
  props: ["memos"],
  emits: ["update", "clickedAddMemo"],
  methods: {
    select(memo, idx) {
      this.$emit("update", memo, idx);
    },
    handleClickedAddMemo() {
      this.$emit("clickedAddMemo");
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
