<template>
    <div class="history">
        <div class="wrapper">
            <h3>History</h3>
            <button class="clear-btn" @click="$emit('clear')">Clear</button>
        </div>
        <ul>
            <li v-for="(item, index) in items" :key="index">
                {{ item }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'History',
    props: {
        items: {
        type: Array,
        required: true
        }
    }
};
</script>

<style scoped>
.wrapper {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 20px;
}

.history {
    color: white;
    background: #2c2c2c;
    padding: 20px;
    border-radius: 12px;
    width: 250px;
    max-height: 400px;
    overflow-y: auto;
}

.clear-btn {
    background: #ff5c5c;
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 6px;
    cursor: pointer;
}

.clear-btn:hover {
    background: #e04848;
}

.history h3 {
    margin-top: 0;
    margin-bottom: 10px;
}

.history ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.history li {
    padding: 5px 0;
    border-bottom: 1px solid #444;
}
</style>
