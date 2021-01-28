<template>
  <div class="item-wrapper">
    <div class="main-wrapper">
      <div class="img-wrapper">
        <figure>
          <img v-bind:src="item.img" :alt="item.creator" />
          <figcaption>{{ item.creator }}</figcaption>
        </figure>
      </div>
      <div class="task">
        <p class="date">{{ item.date }}</p>
        <p class="" v-bind:class="{ done: item.completed }">
          {{ item.task }}
        </p>
        <!-- !!!!!!! !!!!!!!!!!!!!!!!!!!!!!!!!!-->
        <span v-show="!item.inEditMode">{{ item.task }}</span>
        <input
          v-bind:placeholder="item.task"
          v-show="item.inEditMode"
          v-model="item.task"
        />
        <!-- !!!!!!!!!!! -->
        <button
          type="button"
          class="btn btn-info"
          v-show="!item.inEditMode"
          @click="editItem(item)"
        >
          <i class="fa fa-edit"></i> Edit
        </button>
      </div>
    </div>

    <div class="btn-wrapper">
      <div class="btn-main">
        <div
          class="btn-done"
          type="checkbox"
          v-on:click="item.completed = !item.completed"
          @click="sendToEnd"
        ></div>
        <div class="btn-delete" @click="removeTask"></div>
      </div>
      <div class="btn-priority">
        <div class="btn-high-priority" @click="moveUp"></div>
        <div class="btn-low-priority" @click="moveDown"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["item"],
  methods: {
    removeTask() {
      this.$store.commit("removeToDo", this.item);
    },
    sendToEnd() {
      this.$store.commit("sendToDoToEnd", this.item);
    },
    moveUp() {
      this.$store.commit("moveUp", this.item);
    },
    moveDown() {
      this.$store.commit("moveDown", this.item);
    },
    // editItem(){
    //   this.$store.commit("editItem", this.item.inEditMode);
    // }
    editItem(item) {
      item.inEditMode = true;
    },
    editItemComplete(item) {
      item.inEditMode = false;
    },
  },
};
</script>

<style scoped>
.item-wrapper {
  border-bottom: 1px solid #b6b5b5;
  color: #524b4b;
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

.main-wrapper {
  width: 80%;
  display: flex;
  justify-content: space-between;
}

.img-wrapper {
  max-width: 50px;
}

img {
  border-radius: 50%;
  width: 100%;
}
figcaption {
  text-align: center;
  font-style: italic;
}
.date {
  font-family: "Noto Sans JP", sans-serif;
  font-size: 0.8rem;
  text-align: left;
  padding-bottom: 5px;
}
.task {
  width: 80%;
  height: 100%;
  font-weight: bold;
  text-align: center;
  align-self: center;
  font-family: "Noto Sans JP", sans-serif;
}
.btn-wrapper {
  width: 15%;
  display: flex;
  justify-content: space-between;
}
.btn-main {
  width: 50%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.btn-delete,
.btn-high-priority,
.btn-low-priority,
.btn-done {
  border-radius: 50px;
  padding: 10px;
  width: 30px;
  height: 30px;
  background-repeat: no-repeat;
  background-position: center;
  cursor: pointer;
}

.btn-delete:hover,
.btn-high-priority:hover,
.btn-low-priority:hover,
.btn-done:hover {
  background-color: #a1dffb5e;
}
.btn-done {
  background-image: url("../assets/check.svg");
}
.btn-delete {
  background-image: url("../assets/delete.svg");
}
.btn-high-priority {
  background-image: url("../assets/arrow-up.svg");
}

.btn-low-priority {
  background-image: url("../assets/arrow-down.svg");
}
input {
  width: 18px;
  height: 18px;
}
.done {
  text-decoration: line-through;
}

@media (max-width: 1000px) {
  .main-wrapper {
    width: 100%;
  }
}

@media (max-width: 1000px) {
  .main-wrapper {
    flex-direction: column;

    align-items: center;
    width: 50%;
  }
  .date {
    text-align: center;
    padding-bottom: 50px;
  }
  .btn-wrapper {
    width: 40%;
  }
  .btn-priority {
    align-self: center;
  }
}
</style>