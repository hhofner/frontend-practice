<template>
  <div class="container">
    <div class="todo">
      <input type="checkbox" class="checkbox" v-model="isDone" />
      <input type="text" v-model="todoTitle" placeholder="Write something" />
      <div class="tags">
        <TransitionGroup name="list">
          <div v-for="tag in tags" :key="tag" class="tag">
            {{ tag }}
          </div>
        </TransitionGroup>
        <input type="text" v-model="newTag" @keypress.enter="handleNewTag" />
      </div>
    </div>
  </div>
</template>

<script setup>
const tags = ref(new Set(["home"]));
const newTag = ref("");
const isDone = ref(false);
const todoTitle = ref("");

const handleNewTag = () => {
  const filteredTag = newTag.value.toLowerCase();
  tags.value = tags.value.add(filteredTag);
  newTag.value = "";
};
</script>

<style>
* {
  font-family: sans-serif;
  font-size: 18px;
  --my-gap: 10px;
}

input {
  border: none;
}

input:focus {
  outline: none;
}

.checkbox {
  width: 30px;
}

.container {
  display: flex;
  justify-content: center;
  padding: 25px;
}

.todo {
  border: 5px solid seagreen;
  padding: 15px;
  border-radius: 25px;
  gap: var(--my-gap);
  display: flex;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: var(--my-gap);
}

.tag {
  display: flex;
  align-items: center;
}

.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: scale(0.01);
}

.list-leave-active {
  position: absolute;
}
</style>
