<template>
  <div class="container">
    <div class="box">
      <div class="list">
        <MemoDetails
          v-bind:memos="memos"
          v-on:editMemo="handleEditMemo"
          v-on:createMemo="handleCreateMemo"
        />
      </div>
      <div class="edit">
        <div v-if="show">
          <MemoForm
            v-on:update="handleUpdate"
            v-on:destroy="handleDestroy"
            v-bind:editMemo="editMemo"
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
      this.saveMemo()
      this.show = false
    },
    handleDestroy(idx){
      this.memos.splice(idx, 1);
      this.saveMemo()
      this.show = false
    },
    saveMemo(){
      const parsed = JSON.stringify(this.memos);
      localStorage.setItem("memos", parsed)
    },
    handleEditMemo(memo, idx) {
      this.show = true
      this.editMemo = { memo: memo, idx: idx };
    },
    handleCreateMemo() {
      this.show = true
      this.memos.push("新規メモ")
      this.saveMemo()
      this.idx = this.memos.length - 1
      this.editMemo = { memo: "新規メモ", idx: this.idx }
    }
  },
  data() {
    return {
      memos: [],
      editMemo: null,
      idx: null,
      show: false,
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
