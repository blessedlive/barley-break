<template>
    <div class="game">
        <div class="counters">
            <Panel name="Ходов" :value="moves"/>
            <Panel name="Прошло секунд" :value="seconds"/>
        </div>

        <div class="wrapper">
            <Board :state="state" ref="board"/>
        </div>

        <div class="controls">
            <span class="message" v-if="state === 2">Вы справились за {{ seconds }} сек.! Поздравляем!</span>
            <button @click="startGame">{{ (this.state === 0) ? "Начать игру" : "Рестарт" }}</button>

            <Keyboard v-if="state === 1" :onPress="makeMove" />
        </div>
    </div>
</template>

<script>
import Board from './Board';
import Panel from './Panel';
import Keyboard from './Keyboard';
import './Game.scss';

export default {
    data: () => {
        return {
            /**
             * 0 - игра ожидает начала
             * 1 - игра в процессе
             * 2 - игра завершена
             */
            state: 0,

            /** Количество ходов */
            moves: 0,

            /** Время в секундах */
            seconds: 0,
            
            /** Таймер для отсчета */
            timer: null
        }
    },

    methods: {
        /** 
         * Запускает процесс игры
         */
        startGame() {
            this.refreshCounters();

            this.timer = setInterval(() => {
                this.seconds++;
            }, 1000)

            this.state = 1;

            this.$refs.board.buildGrid();
        },

        /** 
         * Обнуляет все показатели
         */
        refreshCounters() {
            if(this.timer) {
                clearInterval(this.timer);
            }

            this.seconds = 0;
            this.moves = 0;
        },

        /** 
         * Изменяет статус игры
         * @param {number} state - статус игры
         */
        changeState(state) {
            this.state = state;

            if(state === 2 && this.timer) {
                clearInterval(this.timer);
            }
        },

        /** 
         * Прибавляет ход
         */
        addMove() {
            this.moves++;
        },

        /** 
         * Callback для нажатия по интерактивной клавиатуре
         */
        makeMove(moveIndex) {
            this.$refs.board.step(moveIndex)
        }
    },

    components: { Board, Panel, Keyboard }
}
</script>