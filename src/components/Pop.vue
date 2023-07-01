<template>
  <div class="pop" v-if="popupConfig">
    <div class="pop-container">
      <div class="pop-container-navbar">
        <i class="fa-regular fa-circle-xmark" @click="closePop"></i>
      </div>
      <div class="pop-container-title">
        <h1>
          {{ popupConfig.pop.titulo }}
        </h1>
        <h2>{{ popupConfig.pop.subtitulo }}</h2>
      </div>
      <div class="pop-container-form">
        <form action="" method="post">
          <div
            v-for="index in Math.min(3, popupConfig.pop.camposFormulario)"
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
          <select name="" id="" v-if="popupConfig.pop.camposFormulario === 4">
            <option value="">Selecione seu gênero</option>
            <option value="man">Homem</option>
            <option value="woman">Mulher</option>
            <option value="other">Faço parte do grupo LGBTQIA+</option>
            <option value="skip">Prefiro não dizer</option>
          </select>
          <br />
          <label v-if="popupConfig.pop.checkboxConsentimento === true">
            <input type="checkbox" name="consentimento" required />
            <span>
              {{ popupConfig.pop.checkboxTexto }}
            </span>
          </label>
          <br />
          <input type="submit" value="Enviar meus dados" />
        </form>
      </div>
      <div class="pop-container-footer">
        <img :src="popupConfig.pop.imagemFooter" alt="" />
      </div>
      <div class="pop-container-wheel">
        <img :src="popupConfig.pop.imagemRoda" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pop",
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
    closePop() {
      this.$emit("update:propPop", false);
    },
  },
  props: {
    propPop: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
.pop {
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.61);
}

.pop-container {
  width: 40%;
  background-image: url(../../public/img/fundo.webp);
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: #6748a8;
  position: relative;
  overflow: hidden;
}

.pop-container-wheel {
  position: absolute;
  bottom: -400px;
  left: -450px;
  z-index: 1;
}

.pop-container-navbar {
  width: 100%;
  font-size: 30px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 20px 20px 10px;
}

.pop-container-navbar i {
  cursor: pointer;
}

.pop-container-footer,
.pop-container-form,
.pop-container-title {
  z-index: 10;
}

.pop-container-wheel img {
  opacity: 0.5;
  animation: rotate 10s linear infinite;
  max-width: 800px;
}

.pop-container-title {
  text-align: center;
  flex-direction: column;
  margin: 10px auto 10px;
  padding: 0 10px;
}

.pop-container-title h1 {
  font-weight: 900;
  text-transform: uppercase;
  font-size: 25px;
}

.pop-container-title h2 {
  font-weight: 400;
  font-size: 20px;
}

.pop-container-form {
  margin: 10px auto;
  width: 100%;
  padding: 0 60px;
  text-align: center;
}

.pop-container-form input,
.pop-container-form select {
  margin: 10px auto;
  width: 100%;
}

.pop-container-form input,
.pop-container-form select {
  padding: 10px 5px;
}

.pop-container-form input[type="submit"] {
  width: 70%;
  background: #6748a8;
  border: 0;
  color: #fcfcfc;
  font-size: 20px;
  font-weight: 600;
  cursor: pointer;
  border: 3px solid #fcfcfc;
  transition: border 0.2s;
}

.pop-container-form input[type="submit"]:hover {
  border: 3px solid #6748a8;
}

.pop-container-form label input,
.pop-container-form label span {
  padding: 0;
  margin: 10px 0;
  width: auto;
  color: #19112b;
}

.pop-container-form label span {
  margin-left: 5px;
}

.pop-container-footer {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  margin-top: 10px;
  padding: 0 10px 10px;
}

.pop-container-footer img {
  max-width: 250px;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@media only screen and (max-width: 1020px) {
  .pop-container {
    width: 60%;
  }

  .pop-container-title {
    margin: 0;
  }

  .pop-container-title h1 {
    font-size: 20px;
  }
  .pop-container-title h2 {
    font-size: 17px;
  }
  .pop-container-form {
    padding: 0 30px;
  }
  .pop-container-form input[type="submit"] {
    font-size: 15px;
  }
  @media only screen and (max-width: 510px) {
    .pop-container {
      width: 80%;
    }
  }
}
</style>
