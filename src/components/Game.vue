<template>
  <div class="game" v-if="popupConfig">
    <div class="game-container">
      <div class="game-container-main">
        <div class="game-container-navbar">
          <i class="fa-regular fa-circle-xmark" @click="closeGame"></i>
        </div>
        <div class="game-container-main-niquel">
          <div class="game-container-main-niquel-text">
            <h1>
              {{ popupConfig.jogo.titulo }}
            </h1>
            <h3>{{ popupConfig.jogo.subtitulo }}</h3>
          </div>
          <div class="game-container-main-niquel-image">
            <img :src="popupConfig.jogo.imagem" alt="caça-niquel" id="niquel" />
          </div>
        </div>
        <div class="game-container-main-form">
          <h3>{{ popupConfig.jogo.subtituloForm }}</h3>
          <br />
          <form action="" method="post">
            <div
              v-for="index in Math.min(3, popupConfig.jogo.camposFormulario)"
              :key="index"
            >
              <input
                :type="getCampoTipo(index)"
                :name="getCampoNome(index)"
                :id="getCampoId(index)"
                :placeholder="getCampoPlaceholder(index)"
                required
              />
            </div>
            <select
              name=""
              id=""
              v-if="popupConfig.jogo.camposFormulario === 4"
            >
              <option value="">Selecione seu gênero</option>
              <option value="man">Homem</option>
              <option value="woman">Mulher</option>
              <option value="other">Faço parte do grupo LGBTQIA+</option>
              <option value="skip">Prefiro não dizer</option>
            </select>
            <br />
            <label v-if="popupConfig.jogo.checkboxConsentimento === true">
              <input type="checkbox" name="consentimento" required />
              <span>
                {{ popupConfig.jogo.checkboxTexto }}
              </span>
            </label>
            <br />
            <input type="submit" value="Enviar meus dados" />
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  data() {
    return {
      popupConfig: null,
    };
  },
  mounted() {
    fetch("/popup-config.json")
      .then((response) => response.json())
      .then((data) => {
        this.popupConfig = data;
      })
      .catch((error) => {
        console.error("Erro ao carregar o arquivo JSON:", error);
      });
  },
  methods: {
    getCampoTipo(index) {
      if ((index === 1) | 2) {
        return "text";
      } else if (index === 3) {
        return "number";
      } else {
        return undefined;
      }
    },
    getCampoNome(index) {
      if (index === 1) {
        return "name";
      } else if (index === 2) {
        return "email";
      } else if (index === 3) {
        return "number";
      } else {
        return null;
      }
    },
    getCampoId(index) {
      if (index === 1) {
        return "name";
      } else if (index === 2) {
        return "email";
      } else if (index === 3) {
        return "number";
      } else {
        return null;
      }
    },
    getCampoPlaceholder(index) {
      if (index === 1) {
        return "Digite seu nome completo";
      } else if (index === 2) {
        return "Digite seu email";
      } else if (index === 3) {
        return "Insira o número do seu telefone";
      } else {
        return null;
      }
    },
    closeGame() {
      this.$emit("update:propGame", false);
    },
  },
  props: {
    propGame: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
.game {
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.726);
}

.game-container {
  width: 60%;
  background: #fff;
  position: relative;
  height: 430px;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  border-radius: 5px;
  overflow: hidden;
}

.game-container-navbar {
  position: absolute;
  top: 10px;
  right: 10px;
}

.game-container-navbar i {
  color: #171612e0;
  font-size: 20px;
  cursor: pointer;
}

.game-container-main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.game-container-main-niquel {
  width: 50%;
  background: linear-gradient(#970b01da, #970b01da),
    url(../../public/img/poker.webp);
  background-size: cover;
  background-position: center;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}

.game-container-main-niquel-text {
  color: #fff;
  text-align: center;
  margin: 30px 10px;
}

.game-container-main-niquel-text h1 {
  border-left: solid 5px #ffbe0a;
  border-right: solid 5px #ffbe0a;
  margin-bottom: 5px;
}

.game-container-main-niquel-text h3 {
  font-weight: 400;
}

.game-container-main-niquel-image {
  text-align: center;
  width: 100%;
  padding: 0 0 60px;
}

.game-container-main-niquel-image img {
  max-width: 250px;
}

.game-container-main-form {
  display: flex;
  flex-direction: column;
  background: #fffffc;
  width: 50%;
  height: 100%;
  text-align: center;
  padding: 50px 10px 50px;
}

.game-container-main-form input,
.game-container-main-form label,
.game-container-main-form select {
  margin: 10px 0;
  padding: 5px 10px;
}

.game-container-main-form label span {
  font-size: 14px;
  margin-left: 5px;
}

.game-container-main-form input:not([type="checkbox"]),
.game-container-main-form select {
  width: 90%;
}

.game-container-main-form input[type="checkbox"]:checked {
  background-color: #171612;
}

.game-container-main-form input[type="submit"] {
  background: #171612;
  color: #ffbe0a;
  border: 1px solid #00000000;
  font-weight: bold;
}

.game-container-main-form input[type="submit"]:hover {
  background: #fff;
  border: 1px solid #171612;
  color: #171612;
  cursor: pointer;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@media only screen and (max-width: 964px) {
  .game-container {
    width: 70%;
    height: auto;
    overflow: auto;
  }

  .game-container-main {
    flex-direction: column;
  }

  .game-container-main-niquel,
  .game-container-main-form {
    width: 100%;
  }

  .game-container-main-niquel-text {
    margin: 10px 5px;
    padding-top: 20px;
  }

  .game-container-main-form input,
  .game-container-main-form label,
  .game-container-main-form select {
    margin: 5px 0;
  }

  .game-container-main-niquel-image {
    padding: 0 0 10px;
  }

  .game-container-main-niquel-image img {
    max-width: 200px;
  }

  .game-container-navbar i {
    color: #fffffc;
  }

  .game-container-main-form {
    padding: 10px 0;
  }

  .game-container-main-niquel-text h1 {
    font-size: 25px;
    border-left: 0;
    border-right: 0;
  }

  h3 {
    font-size: 17px;
  }
}

@media only screen and (max-width: 554px) {
  .game-container {
    width: 90%;
  }
}

@media screen and (orientation: landscape) and (max-height: 420px) {
  .game-container {
    width: 90%;
    height: 100%;
    overflow: auto;
  }

  .game-container-main {
    flex-direction: row;
  }

  .game-container-main-niquel {
    height: 100%;
    background-repeat: repeat;
  }
  .game-container-navbar i {
    color: #171612;
  }
  .game-container-main-form {
    padding: 30px 0 0;
  }
}
</style>
