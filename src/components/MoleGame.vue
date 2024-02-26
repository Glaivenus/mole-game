<template>
    <div class="game" v-if="gameStarted">
      <div v-for="(item, index) in gameItems" :key="index" class="game-item" @click="checkItem(item)">
        <img :src="`./assets/${item.image}`" alt="Game Item" />
      </div>
    </div>
    <button v-else @click="startGame">开始游戏</button>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const gameStarted = ref(false);
      const gameItems = ref([]);
  
      const startGame = () => {
        gameStarted.value = true;
        // 初始化游戏元素
        gameItems.value = [...Array(9)].map(() => {
          return Math.random() < 0.66
            ? { type: 'mole', image: `${Math.floor(Math.random() * 6) + 1}.png` }
            : { type: 'bomb', image: `${Math.floor(Math.random() * 3) + 7}.png` };
        });
      };
  
      const checkItem = (item) => {
        if (item.type === 'bomb') {
          alert('游戏结束！');
          gameStarted.value = false;
          gameItems.value = [];
        }
        // 添加逻辑以处理点击地鼠的情况
      };
  
      return { gameStarted, gameItems, startGame, checkItem };
    },
  };
  </script>
  
  <style scoped>
  .game {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    max-width: 600px; /* 或根据需要调整 */
    margin: auto;
  }
  .game-item {
    flex: 1 0 33%;
    padding: 10px;
  }
  .game-item img {
    width: 100%;
    height: auto;
  }
  button {
    display: block;
    margin: auto;
  }

  @media (max-width: 600px) {
  .game-item {
    flex: 1 0 50%; /* 在小屏幕上每行显示两个游戏元素 */
  }
}

  </style>
  