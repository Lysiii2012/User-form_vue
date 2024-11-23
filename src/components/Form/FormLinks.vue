<template>
  <div class="list-content new_links">
    <h4>{{ name }}</h4>
    <ul class="new_items">
      <li v-for="(item, index) in links" :key="index" class="new_item">
        <span>{{ item.name }} : </span>
        <a :href="item.link" target="_blank">{{ item.link }}</a>
        <span v-if="!disabled" class="delete" @click="deleteItem(index)">
          <img :src="btnDelete" alt="delete" />
        </span>
      </li>
    </ul>

    <div class="add_new_links">
      <div class="input_links" v-if="!disabled">
        <input type="text" v-model="NameLink" placeholder="Site name" />
        <input type="text" v-model="link" placeholder="Link" />
      </div>
      <div
        class="button_add_item"
        @click="addItem"
        :class="{ disabled: disabled || !NameLink || !link }"
      >
        +
      </div>
    </div>
  </div>
</template>

<script>
import Delete from "../../assets/media/delete.svg";

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
      btnDelete: Delete,
      links: [],
      NameLink: "",
      link: "",
    };
  },
  created() {
    const savedLinks = JSON.parse(localStorage.getItem(this.name));
    if (savedLinks) {
      this.links = savedLinks;
    }
  },
  methods: {
    addItem() {
      if (this.NameLink.trim() && this.link.trim()) {
        this.links.push({ name: this.NameLink.trim(), link: this.link.trim() });
        this.NameLink = "";
        this.link = "";
        this.saveToLocalStorage();
      } else {
        alert("Please fill out both fields before adding.");
      }
    },
    deleteItem(index) {
      this.links.splice(index, 1);
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem(this.name, JSON.stringify(this.links));
    },
    getItems() {
      return this.links;
    },
  },
};
</script>

<style scoped>
.new_item {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 10px;
}
.new_items a {
  color: #3888e7;
}
.new_links input:focus {
  outline: none;
}
.new_links {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  flex-direction: column;
}
input {
  padding: 10px 0;
  background: transparent;
  border: none;
  border-bottom: 1.41px solid #00000061;
  width: 100%;
  height: auto;
  margin: 0;
  font-size: 24px;
  display: block;
}
.add_new_links {
  display: flex;
  gap: 16px;
  align-items: center;
}
.new_item span {
  font-size: 20px;
  color: #49535c;
  text-transform: capitalize;
}
.add_new_links > div {
  display: flex;
  gap: 16px;
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
  gap: 30px;
  margin: 0 0 10px;
}
.button_add_item.disabled {
  pointer-events: none;
  cursor: not-allowed;
}
.button_add_item {
  cursor: pointer;
}
.delete img {
  width: 34px;
  display: block;
}
</style>
