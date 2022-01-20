<template>
  <ul class="todo-main">
    <transition-group name="todo" appear>
      <MyItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj"/>
    </transition-group>
  </ul>
</template>

<script>
import MyItem from "@/components/MyItem";

export default {
  name: "MyList",
  components: {MyItem},
  props: ["todos"]
};
</script>

<style scoped>
.todo-main {
  margin-left: 0;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}

.todo-enter-active {
  animation: move 0.5s linear;
}

.todo-leave-active {
  animation: move 0.5s linear reverse;
}

@keyframes move {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
</style>