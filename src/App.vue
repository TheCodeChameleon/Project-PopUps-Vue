<template>
  <div class="home">
    <div class="home-buttons">
      <button @click="showGame">Pop-Up Jogo</button>
      <Game
        v-if="propGame"
        :propGame="propGame"
        @update:propGame="propGame = $event"
      />
      <button @click="showVideo">Pop-Up Video</button>
      <Video
        v-if="propVideo"
        :propVideo="propVideo"
        @update:propVideo="propVideo = $event"
      />
      <button @click="showPop">Pop-Up PopConvert (Bônus)</button>
      <Pop
        v-if="propPop"
        :propPop="propPop"
        @update:propPop="propPop = $event"
      />
    </div>
    <div class="home-text">
      <Text />
      <Links />
      <div class="home-text-danger">
        <p>
          * É importante ressaltar que a página principal não passou por testes
          tão rigorosos quanto os pop-ups para garantir sua responsividade.
          Portanto, pode haver quebras de layout inadequadas nesta página
          específica, mas os pop-ups foram cuidadosamente desenvolvidos para
          garantir uma experiência responsiva consistente.*
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Video from "./components/Video.vue";
import Game from "./components/Game.vue";
import Text from "./components/Text.vue";
import Links from "./components/Links.vue";
import Pop from "./components/Pop.vue";

export default {
  name: "App",
  components: {
    Video,
    Game,
    Text,
    Links,
    Pop,
  },
  data() {
    return {
      propGame: false,
      propVideo: false,
      propPop: false,
    };
  },
  methods: {
    showGame() {
      return (this.propGame = !this.propGame);
    },
    showVideo() {
      return (this.propVideo = !this.propVideo);
    },
    showPop() {
      return (this.propPop = !this.propPop);
    },
  },
};
</script>

<style>
@import "~@fortawesome/fontawesome-free/css/all.min.css";
@import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
}

.home {
  width: 100%;
  height: 100%;
  background: #121212;
}

.home-buttons {
  width: 100%;
  height: 200px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.home-buttons button {
  align-items: center;
  appearance: none;
  background-color: #fcfcfd;
  border-radius: 4px;
  border-width: 0;
  box-shadow: rgba(45, 35, 66, 0.4) 0 2px 4px,
    rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #d6d6e7 0 -3px 0 inset;
  box-sizing: border-box;
  color: #36395a;
  cursor: pointer;
  display: inline-flex;
  font-family: "JetBrains Mono", monospace;
  height: 48px;
  justify-content: center;
  line-height: 1;
  list-style: none;
  overflow: hidden;
  padding-left: 16px;
  padding-right: 16px;
  position: relative;
  text-align: left;
  text-decoration: none;
  transition: box-shadow 0.15s, transform 0.15s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  white-space: nowrap;
  will-change: box-shadow, transform;
  font-size: 18px;
}

.home-buttons button:focus {
  box-shadow: #d6d6e7 0 0 0 1.5px inset, rgba(45, 35, 66, 0.4) 0 2px 4px,
    rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #d6d6e7 0 -3px 0 inset;
}

.home-buttons button:hover {
  box-shadow: rgba(45, 35, 66, 0.4) 0 4px 8px,
    rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #d6d6e7 0 -3px 0 inset;
  transform: translateY(-2px);
}

.home-buttons button:active {
  box-shadow: #d6d6e7 0 3px 7px inset;
  transform: translateY(2px);
}

.home-text {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.home-text-danger {
  color: red;
  font-style: italic;
  text-align: center;
  padding: 10px;
}

@media only screen and (max-width: 300px) {
  * {
    word-break: break-all;
  }

  .home-buttons {
    flex-direction: column;
  }

  .home-buttons button {
    width: 100%;
  }
}
</style>
