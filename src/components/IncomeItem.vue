<script setup>
import { ref } from 'vue';


let emit = defineEmits(['removeIncome'])
let { income } = defineProps(['income'])
let date = new Date(income.date);
let day = date.getDate();
let month = date.getMonth();
let year = date.getFullYear();
let formattedDate = ref(day + "/" + month + "/" + year);
</script>
<template>
    <div class="income-item">
        <div class="removeItem" @click="emit('removeIncome',income.id)">x</div>
        <div class="desc">
            {{ income.description }}
        </div>
        <div class="price">
            £{{ income.income }}
        </div>
        <div v-if="income.date" class="date">
            {{ formattedDate }}
        </div>
        <div v-else class="date">________</div>
    </div>
</template>

<style scoped>
.income-item {
    position: relative;
    display: flex;
    padding: 15px 15px 15px 0px;
    background-color: #FFF;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto 30px;
}

.removeItem {
    color: #EF2D2D;
    font-weight: 600;
    font-size: 20px;
    line-height: 1;
    text-align: center;
    margin: 0 15px;
    cursor: pointer;
}

.desc {
    color: #666;
    flex: 1 1 100%;
    font-size: 20px;
}

.price {
    color: #666;
    min-width: 100px;
    font-size: 20px;
    margin:0 20px ;
}

.date {
    color: #666;
    text-align: right;
    font-size: 20px;
}
</style>