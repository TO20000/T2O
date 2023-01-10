<template>
    <div>
        <ul>
            <li v-for="(item, index) in list" :key="item.name">
                {{ `${item.name}${item.price.toFixed(2)}元` }}&nbsp;
                <button @click="sub(index)" :disabled="item.num == 1 ? true : false">-</button>
                <input class="inp" v-model="item.num" readonly />
                <button @click="add(index)" :disabled="item.num == item.house ? true : false">+</button>&nbsp;总价: {{ sum(index) }}
            </li>
            <p>所有商品总价格: {{ allPrice }}元</p>
            <span v-if="allPrice >= 400">太贵了!! 886</span>
        </ul>
    </div>
</template>

<script setup>
import { reactive, computed } from 'vue'
let list = reactive([
    {
        name: '书包',
        price: 28,
        num: 1,
        house: 15,
    },
    {
        name: '铅笔',
        price: 4.5,
        num: 2,
        house: 40,
    },
    {
        name: '耳机',
        price: 32,
        num: 3,
        house: 10,
    },
    {
        name: '笔记本',
        price: 10,
        num: 1,
        house: 30,
    },
])
// console.log(list);

function sub(idx) {
    if (list[idx].num == 1) return
    list[idx].num--
}
function add(idx) {
    if (list[idx].num == list[idx].house) return
    list[idx].num++
}
function sum(idx) {
    return (list[idx].num * list[idx].price).toFixed(2);
}
const allPrice = computed({
    get: () => {
        let total = 0;
        list.forEach(item => {
            total += (item.price * item.num)
        })
        return total
    }
})
</script>

<style>

</style>