<template>
    <div class="history">
        <h3>History</h3>
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
.history {
    color: white;
    background: #2c2c2c;
    padding: 20px;
    border-radius: 12px;
    width: 250px;
    max-height: 400px;
    overflow-y: auto;
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
