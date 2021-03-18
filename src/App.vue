<template>
  <div id="app">
    <h1>To do list</h1>
    <p>1. 在左侧输入待办事项</p>
    <p>2. 将待办事项拖拽到右侧象限</p>
    <div class="wrap">
      <div class="left-block">
        <div class="input-wrap">
          <input v-model="input" type="text" @keyup.enter="add" placeholder="请输入待办事项"/>
          <div class="add-btn" @click="add">添加</div>
        </div>
        <ul class="to-do-list">
          <draggable v-model="todolist" group="todo">
            <li
              v-for="(item, index) in todolist"
              :key="index"
              class="to-do-item"
            >
              <div class="item-name">{{ item.name }}</div>
              <div class="del-btn" @click="del(todolist, index)">删除</div>
            </li>
          </draggable>
        </ul>
      </div>
      <div class="right-block">
        <div class="flex-row">
          <div class="flex-item">
            <div>不紧急但重要</div>
            <ul class="to-do-list">
              <draggable v-model="list1" group="todo">
                <li
                  v-for="(item, index) in list1"
                  :key="index"
                  class="to-do-item"
                >
                  <div class="item-name">{{ item.name }}</div>
                  <div class="del-btn" @click="del(list1, index)">删除</div>
                </li>
              </draggable>
            </ul>
          </div>
          <div class="flex-item">
            <div>紧急且重要</div>
            <ul class="to-do-list">
              <draggable v-model="list2" group="todo">
                <li
                  v-for="(item, index) in list2"
                  :key="index"
                  class="to-do-item"
                >
                  <div class="item-name">{{ item.name }}</div>
                  <div class="del-btn" @click="del(list2, index)">删除</div>
                </li>
              </draggable>
            </ul>
          </div>
        </div>
        <div class="flex-row">
          <div class="flex-item">
            <div>不紧急不重要</div>
            <ul class="to-do-list">
              <draggable v-model="list3" group="todo">
                <li
                  v-for="(item, index) in list3"
                  :key="index"
                  class="to-do-item"
                >
                  <div class="item-name">{{ item.name }}</div>
                  <div class="del-btn" @click="del(list3, index)">删除</div>
                </li>
              </draggable>
            </ul>
          </div>
          <div class="flex-item">
            <div>紧急不重要</div>
            <ul class="to-do-list">
              <draggable v-model="list4" group="todo">
                <li
                  v-for="(item, index) in list4"
                  :key="index"
                  class="to-do-item"
                >
                  <div class="item-name">{{ item.name }}</div>
                  <div class="del-btn" @click="del(list4, index)">删除</div>
                </li>
              </draggable>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "App",
  components: {
    draggable,
  },
  data() {
    return {
      input: "",
      todolist: [],
      list1: [],
      list2: [],
      list3: [],
      list4: [],
    };
  },
  watch: {
    todolist(val) {
      localStorage.setItem("todolist", JSON.stringify(val));
    },
    list1(val) {
      localStorage.setItem("list1", JSON.stringify(val));
    },
    list2(val) {
      localStorage.setItem("list2", JSON.stringify(val));
    },
    list3(val) {
      localStorage.setItem("list3", JSON.stringify(val));
    },
    list4(val) {
      localStorage.setItem("list4", JSON.stringify(val));
    },
  },
  mounted() {
    this.todolist = JSON.parse(localStorage.getItem("todolist")) || [];
    this.list1 = JSON.parse(localStorage.getItem("list1")) || [];
    this.list2 = JSON.parse(localStorage.getItem("list2")) || [];
    this.list3 = JSON.parse(localStorage.getItem("list3")) || [];
    this.list4 = JSON.parse(localStorage.getItem("list4")) || [];
  },
  methods: {
    add() {
      if (this.input !== "") {
        this.todolist.push({ name: this.input });
        this.input = "";
      }
    },
    del(arr, index) {
      arr.splice(index, 1);
    },
  },
};
</script>

<style>
.wrap {
  display: flex;
}
.left-block {
  border: 1px solid #ccc;
  width: 300px;
  padding: 15px;
}
.input-wrap {
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.input-wrap input {
  width: 60%;
  padding: 0;
  border: none;
  height: 100%;
  outline: none;
}
.add-btn {
  padding: 5px 15px;
  border-radius: 20px;
  background: #2b6be4;
  color: #fff;
}
.to-do-list {
  padding: 0;
  list-style: none;
}
.to-do-item {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-bottom: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.item-name {
  width: 80%;
  word-break: break-all;
}
.right-block {
  width: 100%;
}
.del-btn {
  padding: 5px;
  border-radius: 10px;
  background: red;
  color: #fff;
  font-size: 14px;
}
.flex-row {
  display: flex;
  align-items: center;
}
.flex-item {
  border: 1px solid #ccc;
  flex-basis: 50%;
  min-height: 200px;
  padding: 15px;
}
</style>
