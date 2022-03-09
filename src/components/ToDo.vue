<template>
  <main>
    <section>
      <h1>{{ title }}</h1>
      <div class="second-title">
        <div v-if="test">
          <p>{{ para }}</p>
        </div>
        <div v-else>
          <p>{{ wrong }}</p>
        </div>
      </div>
      <div class="input-container">
        <input v-model="toDoItem" maxlength="15" />
        <button @click="addItem"><img src="../assets/add.png" /></button>
      </div>
      <div class="list">
        <ul>
          <li  v-for="item in items" :key="item.id" >
            {{ item.id }}. {{ item.name }}
            <button @click="removeItem">
              <img src="../assets/delete-button.png" />
            </button>
          </li>
        </ul>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      test: true,
      title: "To do list",
      para: "Add yout first item",
      items: [],
      toDoItem: "",
      wrong: "Can not be empty",
      count: 1
    };
  },
  methods: {
    addItem() {
      if (this.toDoItem === "") {
        this.test = false;
      } else if (this.toDoItem !== "") {
        this.items.push({id: this.count++, name: this.toDoItem });
        this.para = "This is your list";
        this.test = true;
        console.log(this.items)
      }
      this.toDoItem = "";
    },
    removeItem() {
      this.items.pop({ id: this.count--, name: this.toDoItem });
      if (this.items.length === 0) {
        this.para = "Add yout first item";
      }
    },
  },
};
</script>

<style scoped>
main {
  background: #ecf0f1;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 10px;
}
section {
  display: flex;
  align-items: center;
  flex-direction: column;
  background: white;
  border: 2px solid black;
  border-radius: 5px;
  padding: 20px;
  max-width: 375px;
  width: 100%;
}
section h1 {
  padding: 10px;
}
.second-title {
  padding: 10px 0 10px 0;
}
.input-container {
  display: flex;
}
.input-container input {
  padding: 5px;
  margin: 0 5px 5px 0;
  outline: none;
  transition: all 0.2s;
  border-radius: 5px;
}
.input-container input:hover {
  background: black;
  color: white;
}
.input-container input:focus {
  background: black;
  color: white;
}
.input-container button {
  border: none;
  background: white;
}
.input-container img {
  width: 30px;
  border-radius: 5px;
  cursor: pointer;
}
.list {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 10px;
}
.list img {
  width: 30px;
  border-radius: 5px;
  cursor: pointer;
  border: none;
}
.list ul button {
  background: white;
  border: none;
  padding-left: 3px;
  position: absolute;
  right: 5px;
  display: flex;
}
.list ul {
  display: flex;
  flex-direction: column;
  min-height: 200px;
  align-items: flex-start;
  width: 200px;
  padding-bottom: 10px;
}
.list ul li {
  border: 1px solid black;
  list-style: none;
  display: flex;
  align-items: center;
  width: 100%;
  position: relative;
  margin: 2px 0;
  border-radius: 5px;
  padding: 10px;
}
</style>