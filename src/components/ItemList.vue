<template>
  <div>
    <div><strong>未完ItemList</strong></div>
    <div v-for="item in items" :key="item.name">
      <div class="item" v-if="item.state==false"><div style="padding: 10px; margin-bottom: 10px; border: 1px solid #333333;"><div class="name">名前: {{ item.name }}</div>
      <!-- <div class="price">{{ item.price }} 円</div> --><div class="state">完了しているか : {{ item.state }} </div><div class="id">id : {{ item.identifier }} </div><button @click="FinishTask(item.identifier)" >かんりょ～</button><button @click="DeleteTask(item.identifier)" >消えるぜ</button>
        <!--ここまでが各要素の記述-->
      </div>
    </div>
    </div>
    <div><strong>完了ItemList</strong></div>
    <div v-for="item in items" :key="item.name">
      <div class="item" v-if="item.state==true">
      <div style="padding: 10px; margin-bottom: 10px; border: 1px solid #333333;">
        <div class="name">名前: {{ item.name }}</div> <!-- <div class="price">{{ item.price }} 円</div> -->
        <div class="state">完了しているか : {{ item.state }} </div><div class="id">id : {{ item.identifier }} </div><button @click="DeleteTask(item.identifier)" >消えるぜ</button>
        <!--ここまでが各要素の記述-->
      </div>
    </div>
    </div>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <!--
      <label>
        価格
        <input v-model="newItemPrice" type="number" />
      </label>
      -->
      <button @click="addItem">add</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const items = ref([
      { name: "うんうん", state: false, identifier : 0 },
      { name: "ぶりぶり", state: true, identifier : 1 },
    ]);
    const maxi = ref(2);
    const newItemName = ref("");
    const newItemPrice = ref(0);

    const addItem = () => {
      items.value.push({ name: newItemName.value, state: false, identifier : maxi.value });
      maxi.value = maxi.value + 1;
    };
    const FinishTask = (id) =>{
        
        items.value.forEach((element, index) => {
            if (element.identifier == id) {
                items.value[index].state = true;
            }
        })
    };
    
    const DeleteTask = (id) =>{
        items.value.forEach((element, index) => {
            if (element.identifier == id) {
                items.value.splice(index, 1);
            }
        })
    };
    
    return { items, newItemName, newItemPrice, addItem , maxi, FinishTask, DeleteTask};
  },
};
</script>