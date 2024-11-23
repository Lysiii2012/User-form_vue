<template>
  <div class="list-content new_links">
    <h4>{{ name }}</h4>
    <ul class="item">
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
        <span class="delete" @click="deleteItem(index)" v-if="!disabled"
          >X</span
        >
      </li>
    </ul>
    <input
      type="text"
      v-model="newItem"
      placeholder="Add item..."
      v-if="!disabled"
    />
    <div
      class="button_add_item"
      @click="addItem"
      :class="{ disabled: disabled || !newItem }"
    >
      +
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      items: [],
      newItem: "",
    };
  },
  created() {
    const savedItems = JSON.parse(localStorage.getItem(this.name));
    if (savedItems) {
      this.items = savedItems;
    }
  },
  methods: {
    addItem() {
      if (this.newItem.trim()) {
        this.items.push(this.newItem.trim());
        this.newItem = "";
        // this.saveToLocalStorage();
      }
    },
    deleteItem(index) {
      this.items.splice(index, 1);
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem(this.name, JSON.stringify(this.items));
    },
    getItems() {
      return this.items;
    },
  },
};
</script>

<style scoped>
.new_links input {
  padding: 10px 0;
  background: transparent;
  border: none;
  border-bottom: 1.41px solid #00000061;
  width: 100%;
  height: auto;
  margin: 0;
  max-width: 150px;
}
.button_add_item.disabled {
  pointer-events: none;
  cursor: not-allowed;
}
.button_add_item {
  cursor: pointer;
}
.new_links {
  display: flex;
  gap: 5px 16px;
  align-items: center;
  margin: 0 0 32px;
  flex-wrap: wrap;
  gap: 16px;
}
.new_links input:focus {
  outline: none;
}
.button_add_item {
  font-size: 30px;
  color: #3888e7;
  line-height: 0.5;
  padding: 0;
  margin: 0 0 0 7px;
}
.item {
  display: flex;
  font-size: 18px;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  flex-wrap: wrap;
}
.item img {
  width: 20px;
}
li {
  padding: 5px 16px;
  font-family: Roboto;
  font-size: 24px;
  font-weight: 400;
  line-height: 1;
  color: #49535c;
  border: 1px solid #49535c;
  border-radius: 100px;
  width: max-content;
  position: relative;
}
.delete {
  position: absolute;
  top: -4px;
  font-weight: 800;
  width: 20px;
  font-size: 12px;
  height: 20px;
  background: #49535c;
  color: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  right: -6px;
  cursor: pointer;
  transition: all 0.3s linear;
}
</style>
