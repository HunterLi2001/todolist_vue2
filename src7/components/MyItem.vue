<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)">
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input type="text" :value="todo.title" v-show="todo.isEdit" @blur="handleBlur(todo,$event)" ref="inputTitle">
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button class="btn btn-edit" @click="handleEdit(todo)" v-show="!todo.isEdit">编辑</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  props: ["todo"],
  methods: {
    //勾选取消勾选
    handleCheck(id) {
      //通知App组件将对应的todo对象的done值取反
      this.$bus.$emit("checkTodo", id);
    },
    //删除
    handleDelete(id) {
      if (confirm("确定要删除吗？")) {
        this.$bus.$emit("deleteTodo", id);
      }
    },
    handleEdit(todo) {
      if (todo.hasOwnProperty.call("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(() => {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo, e) {
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert("输入的值不能为空");
      this.$bus.$emit("updateTodo", todo.id, e.target.value);
    }
  }
};
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #cccccc;
}

li:hover button {
  display: block;
}
</style>