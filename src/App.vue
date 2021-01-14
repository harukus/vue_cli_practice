<template>
  <div class="container">
    <div class="box">
      <div class="list">
        <MemoDetails
          v-bind:memos="memos"
          v-on:select="handleCurrentSelectedMemo"
          v-on:clickedAddMemo="handleClickedAddMemo"
        />
      </div>
      <div class="edit">
        <div v-show="show">
          <MemoForm
            v-on:update="handleUpdate"
            v-on:add="handleAdd"
            v-on:destroy="handleDestroy"
            v-bind:currentSelectedMemo="currentSelectedMemo"
            v-bind:clickedAddMemo="clickedAddMemo"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import MemoForm from "./components/MemoForm.vue";
import MemoDetails from "./components/MemoDetails.vue";
export default {
  name: "App",
  components: {
    MemoForm,
    MemoDetails,
  },
  methods: {
    handleUpdate(newMemo, idx) {
      this.memos[idx] = newMemo
      const parsed = JSON.stringify(this.memos);
      localStorage.setItem("memos", parsed);
    },
    handleAdd(newMemo){
      this.memos.push(newMemo)
      const parsed = JSON.stringify(this.memos);
      localStorage.setItem("memos", parsed)
    },
    handleDestroy(idx){
      this.memos.splice(idx, 1);
      const parsed = JSON.stringify(this.memos);
      localStorage.setItem("memos", parsed)
    },
    handleCurrentSelectedMemo(memo, idx) {
      this.currentSelectedMemo = { memo: memo, idx: idx };
    },
    handleClickedAddMemo() {
      this.clickedAddMemo += 1;
    }
  },
  data() {
    return {
      memos: [],
      currentSelectedMemo: null,
      idx: null,
      clickedAddMemo: 1,
      show: true,
    };
  },
  mounted() {
    if (localStorage.getItem("memos")) {
      try {
        this.memos = JSON.parse(localStorage.getItem("memos"));
      } catch (e) {
        localStorage.removeItem("memos");
      }
    }
  },
};
</script>
<style>
.container {
  margin: 100px auto;
}
.box {
  display: flex;
  width: 700px;
  height: 300px;
  margin: auto;
}
.list {
  background-color: #c7d8f8;
  width: 50%;
}
.edit {
  text-align: center;
  background-color: #c7d8f8;
  width: 50%;
}
</style>
