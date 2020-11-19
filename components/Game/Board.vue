<template>
    <transition-group class="board" :class="{'disabled': state !== 1}">
        <Cell v-for="cell in cells" :index="cell" :key="cell"/>
    </transition-group>
</template>

<script>
import Cell from './Cell';

export default {
    data: () => {
        return {
            cells: []
        }
    },

    mounted() {
        window.addEventListener("keydown", e => {
            if(this.state !== 1) return;

            if(e.keyCode === 37) {  
                this.step(1)
            }
            if(e.keyCode === 38) {  
                this.step(4)
            }
            if(e.keyCode === 39) {  
                this.step(-1)
            }
            if(e.keyCode === 40) {  
                this.step(-4)
            }
        });
    },

    methods: {
        /** 
         * Строит сетку из 16 ячеек
         */
        buildGrid() {
            this.cells = Array.from({length: 15}, (_, i) => i + 1).sort(() => Math.random() - 0.5);
            this.cells.push(0);
        },

        /**
         * Процесс хода
         * @param {number} moveIndex - индекс смещения в сетке
         */
        step(moveIndex) {
            const hole = this.cells.indexOf(0);
            const index = hole + moveIndex;

            if (!this.cells[index]) return false;

            if (moveIndex === -1 || moveIndex === 1) {
                if (Math.floor(hole/4) !== Math.floor(index/4)) {
                    return false;
                }
            }
            
            this.swap(index, hole);

            this.$parent.addMove();

            if(this.checkWin()) {
                this.$parent.changeState(2);
            }
        },

        /**
         * Меняет местами элементы в массиве по индексу
         * @param {number} a - индекс первого элемента
         * @param {number} b - индекс второго элемента
         */
        swap(a, b) {
            let v = this.cells[a];
            this.$set(this.cells, a, this.cells[b]);
            this.$set(this.cells, b, v);
        },

        /** 
         * Проверяет статус выигрыша
         */
        checkWin() {
            const winArray = Array.from({length: 15}, (_, i) => i + 1);
            winArray.push(0);
            
            return this.cells.toString() === winArray.toString();
        }
    },

    components: { Cell },

    props: {
        state: Number
    }
}
</script>