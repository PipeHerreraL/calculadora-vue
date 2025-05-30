<template>
    <div class="wrapper">
        <div class="calculator">
            <input type="text" v-model="display" disabled />
            <div class="buttons">
                <button v-for="btn in buttons" :key="btn" @click="press(btn)">
                {{ btn }}
                </button>
                <button @click="calculate()">=</button>
                <button @click="clear()">C</button>
            </div>
        </div>
        
        <History :items="history" @clear="history = []" />
    </div>
</template>

<script>
import History from './History.vue';

export default {
    components: {
        History
    },
    data() {
        return {
            display: '',
            buttons: ['7','8','9','/','4','5','6','*','1','2','3','-','0','.','+'],
            history: []
        };
    },
    mounted() {
        window.addEventListener('keydown', this.handleKey);
    },
    beforeUnmount() {
        window.removeEventListener('keydown', this.handleKey);
    },
    methods: {
        press(value) {
            this.display += value;
        },
        clear() {
            this.display = '';
        },
        calculate() {
            try {
                const result = eval(this.display);
                if (typeof result === 'number' && isFinite(result)) {
                    this.history.unshift(`${this.display} = ${result}`);
                    this.display = result.toString();
                } else {
                    this.display = 'Error';
                }
            } catch {
                this.display = 'Error';
            }
        },
        handleKey(event) {
            const key = event.key;
            if (this.buttons.includes(key)) {
                this.press(key);
            } else if (key === 'Enter') {
                this.calculate();
            } else if (key === 'Backspace') {
                this.display = this.display.slice(0, -1);
            } else if (key === 'Escape') {
                this.clear();
            }
        }
    }
};
</script>

<style scoped>
.wrapper {
    display: flex;
    gap: 30px;
    justify-content: center;
    align-items: flex-start;
    margin-top: 50px;
}

.calculator {
    background: #1e1e1e;
    padding: 20px;
    border-radius: 12px;
    width: 300px;
    margin: auto;
    box-shadow: 0 0 10px #000;
}
input {
    width: 100%;
    font-size: 2rem;
    margin-bottom: 10px;
    padding: 10px;
    text-align: right;
    border-radius: 6px;
    color: #333;
}
.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}
button {
    font-size: 1.5rem;
    padding: 15px;
    border-radius: 6px;
    background: #333;
    color: white;
}
button:hover {
    background: #444;
}
</style>
