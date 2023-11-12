<script setup>
import { ref, computed, onMounted } from "vue";

const player = ref('') //玩家的值
const computer = ref('') //電腦的值
const score = ref(null) //分數用來判斷輸贏

const games = ref([{
    title: '✊',
    value: 'Stone'
}, {
    title: '🤚',
    value: 'Paper'
}, {
    title: '✌',
    value: 'Scissors'
},])

// 計算結果顯示
const showResult = computed(() => {
    switch (score.value) {
        case -1:
            return `你輸了！\n你出了${player.value}\n電腦出了${computer.value}`
        case 0:
            return `平手。\n你出了${player.value}\n電腦出了${computer.value}`
        case 1:
            return `你贏了！\n你出了${player.value}\n電腦出了${computer.value}`
    }
})

// 電腦隨機出拳
const getComputerChoice = () => {
    let getComputerChoice = ['Stone', 'Paper', 'Scissors']
    let computerValue = getComputerChoice[Math.floor(Math.random() * 3)]
    computer.value = computerValue
    // console.log(computerValue);
    // return computerValue
};

// 結果判斷
const getResult = () => {
    let scoree;
    if (player.value === computer.value) {
        scoree = 0
    } else if (player.value === 'Stone' && computer.value === 'Scissors') {
        scoree = 1
    } else if (player.value === 'Paper' && computer.value === 'Stone') {
        scoree = 1
    } else if (player.value === 'Scissors' && computer.value === 'Paper') {
        scoree = 1
    } else {
        scoree = -1
    }
    score.value = scoree
    // console.log(score);
    // return scoree
}


const play = (game) => {
    // console.log(game);
    player.value = game.value
    getComputerChoice()
    getResult()
    // console.log(comValue);
    // console.log(result);
}

const clear = () => {
    // console.log(111);
    player.value = ''
    computer.value = ''
    score.value = null
}

</script>
<template>
    <div class="wrapper">
        <h1>猜拳</h1>
        <div class="buttons">
            <button class="pssButton" :value=game.value v-for="game in games" @click="play(game)">{{ game.title }}</button>
            <!-- <button class="pssButton" value="Paper">🤚</button>
            <button class="pssButton" value="Scissors">✌</button> -->
        </div>
        <div class="resultContainer">
            <div id="player-score"></div>
            <div id="hands"></div>
            <div id="result">{{ showResult }}</div>
            <button id='endGameButton' @click="clear">🔴</button>
        </div>
    </div>
</template>
<style >
* {
    margin: 0;
    padding: 0;
    /* width: 100%; */
    /* height: 100%; */
}

.wrapper {
    background: #1c1c1c;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    /* width: 100%; */
    /* height: 100%; */
    height: 100vh;
    flex-direction: column;
}

h1 {
    margin-bottom: 50px;
}

.buttons {
    display: flex;
    gap: 20px;
}

button {
    height: 100px;
    width: 100px;
    font-size: 48px;
    border-radius: 30px;
    cursor: pointer;

}

.resultContainer {
    font-size: 2rem;
    text-align: center;
    margin-top: 20px;
}
</style>