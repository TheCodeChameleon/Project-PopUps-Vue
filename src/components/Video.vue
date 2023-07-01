<template>
  <div class="video" v-if="popupConfig">
    <div class="video-container">
      <div class="video-container-navbar">
        <i class="fa-regular fa-circle-xmark" @click="closeVideo"></i>
      </div>
      <div class="video-container-text">
        <h1>{{ popupConfig.video.titulo }}</h1>
        <h3>{{ popupConfig.video.subtitulo }}</h3>
      </div>
      <div class="video-container-main">
        <div class="video-container-main-play">
          <video
            :src="popupConfig.video.urlVideo"
            controls
            :poster="popupConfig.video.poster"
          ></video>
        </div>
        <div class="video-container-main-bar"></div>
        <div class="video-container-main-form">
          <h3>{{ popupConfig.video.subtituloForm }}</h3>
          <br />
          <form action="" method="">
            <div
              v-for="index in Math.min(3, popupConfig.video.camposFormulario)"
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
              v-if="popupConfig.video.camposFormulario === 4"
            >
              <option value="">Selecione seu gênero</option>
              <option value="man">Homem</option>
              <option value="woman">Mulher</option>
              <option value="other">Faço parte do grupo LGBTQIA+</option>
              <option value="skip">Prefiro não dizer</option>
            </select>
            <br />
            <label v-if="popupConfig.video.checkboxConsentimento === true">
              <input type="checkbox" name="consentimento" required />
              <span>
                {{ popupConfig.video.checkboxTexto }}
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
  name: "Video",
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
    closeVideo() {
      this.$emit("update:propVideo", false);
    },
  },
  props: {
    propVideo: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
.video {
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

.video-container {
  width: 60%;
  background: #034078;
  color: #fefcfb;
  position: relative;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  border-radius: 7px;
}

.video-container-navbar {
  position: absolute;
  top: 10px;
  right: 10px;
}

.video-container-navbar i {
  font-size: 20px;
  cursor: pointer;
}

.video-container-main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.video-container-main-play {
  width: 50%;
  background: #034078;
  background-size: cover;
  background-position: center;
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.video-container-text {
  text-align: center;
  margin: 30px 10px;
}

.video-container-text h1 {
  margin-bottom: 5px;
}

.video-container-text h3 {
  font-weight: 400;
}

.video-container-main-play {
  width: 50%;
  padding: 0 0 80px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.video-container-main-play video {
  width: 90%;
  max-width: 90%;
  border-radius: 7px;
}

.video-container-main-form {
  display: flex;
  flex-direction: column;
  background: #034078;
  width: 50%;
  height: 100%;
  text-align: center;
  padding: 0 30px 20px;
  margin-bottom: 10px;
}

.video-container-main-form input,
.video-container-main-form label,
.video-container-main-form select {
  margin: 10px 0;
  padding: 5px 10px;
}
.video-container-main-form label span {
  font-size: 14px;
  margin-left: 5px;
}

.video-container-main-form h3 {
  text-align: center;
}

.video-container-main-form input:not([type="checkbox"]),
.video-container-main-form select {
  width: 90%;
}

.video-container-main-form input[type="checkbox"]:checked {
  background-color: #171612;
}

.video-container-main-form input[type="submit"] {
  background: #171612;
  color: #fffffc;
  border: 1px solid #00000000;
  font-weight: bold;
}

.video-container-main-form input[type="submit"]:hover {
  background: transparent;
  border: 1px solid #fffffc;
  color: #fffffc;
  cursor: pointer;
}

.video-container-main-bar {
  width: 2px;
  height: 320px;
  background: #fffffc;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@media only screen and (max-width: 970px) {
  .video-container {
    width: 70%;
    height: auto;
    overflow: auto;
  }

  .video-container-main {
    flex-direction: column;
  }

  .video-container-main-play,
  .video-container-main-form {
    width: 100%;
  }

  .video-container-text {
    margin: 10px 5px;
    padding-top: 20px;
  }

  .video-container-main-form input,
  .video-container-main-form label,
  .video-container-main-form select {
    margin: 5px 0;
  }

  .video-container-main-play {
    padding: 0 0 10px;
  }

  .video-container-main-play video {
    max-width: 60%;
  }

  .video-container-navbar i {
    color: #fffffc;
  }

  .video-container-main-form {
    padding: 10px 0;
  }

  .video-container-text h1 {
    font-size: 25px;
    border-left: 0;
    border-right: 0;
  }

  h3 {
    font-size: 17px;
  }

  .video-container-main-bar {
    width: 0;
    height: 0;
  }
}

@media only screen and (max-width: 800px) {
  .video-container-main-play video {
    max-width: 80%;
  }
}

@media only screen and (max-width: 554px) {
  .video-container {
    width: 90%;
  }
}

@media screen and (orientation: landscape) and (max-height: 640px) {
  .video-container {
    width: 90%;
    height: 100%;
    overflow: auto;
  }

  .video-container-main {
    flex-direction: row;
    height: auto;
  }

  .video-container-main-play {
    padding: 0;
  }
  .video-container-main-form {
    padding: 0 20px;
    margin: 0;
    justify-content: center;
    align-items: center;
  }
}
</style>
