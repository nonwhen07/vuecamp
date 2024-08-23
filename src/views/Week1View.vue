<script setup>

import { ref } from 'vue'
import products from "../data/products.js"

const productList = ref(products);
const temp = ref({});
const selectItem = (data, id) => {
  temp.value = { ...data }
  temp.value.id = id
}
const editTitle = () => {
  productList.value[temp.value.id].title = temp.value.title
  temp.value = {}
}

</script>

<template>
  <div class="week1">

    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
        </tr>
      </thead>
      <tbody v-for="(item, id) in productList" :key="id" >
        <tr>
          <td style="width: 40%">
            <div class="d-flex align-items-center flex-wrap">
              <span>
                <button type="button" class="btn btn-outline-secondary me-2" @click="selectItem(item, id)" v-if="temp.id !== id">
                  <i class="bi bi-pencil-fill"></i>
                </button>
                {{ item.title }}
              </span>
              <div class="input-group flex-wrap" v-if="temp.id === id">
                <input type="text" class="form-control" placeholder="填寫產品名稱" v-model="temp.title"/>
                <button class="btn btn-outline-secondary" type="button" @click="temp = {}">
                  取消
                </button>
                <button class="btn btn-outline-secondary" type="button" @click="editTitle" :disabled="!temp.title">
                  確認
                </button>
              </div>
            </div>
          </td>

          <td><small>{{item.describe}}</small></td>
          <td>{{item.price}}</td>
          <td style="width: 20%">
            <div class="d-flex align-items-center">
              <button
                type="button"
                class="btn"
                :class="[item.stock === 0 ? 'btn-outline-danger' : 'btn-outline-secondary']"
                :disabled="item.stock < 1"
                @click="item.stock--"
              >
                -</button
              ><span class="mx-2">{{ item.stock }}</span
              ><button type="button" class="btn btn-outline-secondary" @click="item.stock++">
                +
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .week1 {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .stock{
    width: 40px;
    text-align: center;
  }
}
</style>