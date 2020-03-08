<template>
  <div>
    <div>
      <h1>TodoList</h1>
    </div>

    <div>
      <h2>終了済みタスク</h2>
    </div>
    <div v-for="item in items" :key="item.name">
      <template v-if="item.state==true">
        <div class="item">
          <div class="name">タスク名: {{ item.name }}</div>
          <div class="date">期日： {{ item.month }}月{{ item.date }}日</div>
          <!--<div class="name">残り時間{{ item.date }}秒</div>
          <input type="checkbox" v-model="checked" />
          <label for="checkbox">{{ checked }}</label>-->
          <button @click="item.state = false">終わってなかった</button>
        </div>
      </template>
    </div>
    <div>
      <h2>未だ終了せざるタスク</h2>
    </div>
    <div v-for="item in items" :key="item.name">
      <template v-if="item.state==false">
        <div class="item" :class="{po: item.month > 12}">
          <div class="name">タスク名: {{ item.name }}</div>
          <div class="date">期日： {{ item.month }}月{{ item.date }}日</div>
          <button @click="item.state = true">タスク完了</button>
        </div>
      </template>
    </div>

    <div>
      <label>
        名前
        <input type="text" v-model="newItemName" />
      </label>
      <label>
        月
        <input type="number" v-model="newItemMonth" />
      </label>
      <label>
        日
        <input type="number" v-model="newItemDate" />
      </label>
      <button @click="addItem">add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ItemList",
  data() {
    return {
      items: [
        { name: "xxpoxx", month: 4, date: 100, state: true },
        { name: "poxxpo", month: 2, date: 200, state: false }
      ],
      newItemName: "",
      newItemMonth: 1,
      newItemDate: 1,
      newItemState: false
    };
  },
  methods: {
    addItem() {
      if (this.newItemName != "") {
        this.items.push({
          name: this.newItemName,
          month: this.newItemMonth,
          date: this.newItemDate,
          state: this.newItemState
        });
        this.newItemName = "";
        this.newItemMonth = 1;
        this.newItemDate = 1;
      }
    }
  }
};
</script>

<style>
.po {
  color: red;
}
</style>
