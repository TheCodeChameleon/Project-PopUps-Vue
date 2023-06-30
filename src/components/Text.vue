<template>
  <div class="text">
    <ol>
      <li>Eu desenvolvi esse projeto utilizando Vue.js.</li>
      <li>Para a estruturação do projeto, adotei a metodologia B.E.M.</li>
      <li>Utilizei a biblioteca Font Awesome para os ícones.</li>
      <li>
        Ao submeter o formulário, você receberá uma mensagem "Cannot POST"
        porque não foi definido um caminho específico.
      </li>
      <li>
        Os pop-ups são responsivos, adaptando-se a diferentes tamanhos de tela.
      </li>
      <li>
        Todos os valores de configuração estão definidos no arquivo
        "public/popup-config.json".
      </li>
      <li>
        Criei dois layouts diferentes para cada pop-up, seguindo um design
        simples e minimalista, mas que pode ser personalizado de acordo com as
        necessidades e preferências.
      </li>
      <li>
        As imagens foram convertidas para o formato WebP a fim de otimizar o
        tempo de carregamento.
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "Text",
};
</script>

<style scoped>
.text {
  background: #fcfcfc;
  padding: 20px 30px;
  width: 80%;
  border-radius: 10px;
}

.text ol li {
  margin: 5px 0;
}
</style>
