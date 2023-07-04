# Project-PopUps-Vue

Este projeto foi desenvolvido utilizando Vue.js e possui como objetivo a criação de três tipos de pop-ups customizáveis: um para o jogo caça-níquel, outro para exibição de um vídeo e outro simulando um pop-up oficial da Popconvert. Os pop-ups podem ser configurados através de um arquivo JSON, permitindo a seleção do tipo de jogo, vídeo, número de campos no formulário, presença de checkbox para consentimento de dados, título e subtítulo.

## Configuração do Projeto

### Instalação das Dependências

Execute o seguinte comando para instalar as dependências necessárias:

```
npm install
```

### Compilação e Hot-Reload para Desenvolvimento

Para compilar e executar o projeto em modo de desenvolvimento com hot-reload, utilize o seguinte comando:

```
npm run serve
```

### Compilação e Minificação para Produção

Para compilar e minificar o projeto para produção, utilize o seguinte comando:

```
npm run build
```

### Personalização da Configuração

Para personalizar a configuração dos pop-ups, você pode editar o arquivo `public/popup-config.json`. Neste arquivo, você encontrará as seguintes opções de configuração:

- `camposFormulario` (número de campos no formulário, de 1 a 4 campos)
- `checkboxConsentimento` (booleano para definir se o checkbox de consentimento será exibido)
- `urlVideo` (URL do vídeo a ser exibido)
- `imagem` (imagem do caça níquel)
- `titulo` (título do pop-up)
- `subtitulo` (subtítulo do pop-up)
- `subtituloForm` (subtítulo do formulário)
- `checkboxTexto` (texto do checkbox)

## Observações

- Ao submeter o formulário, você receberá uma mensagem "Cannot POST", pois não foi definido um caminho específico para o envio dos dados. Essa mensagem serve apenas como exemplo e não interfere no funcionamento do pop-up.
- Os pop-ups são responsivos e se adaptam a diferentes tamanhos de tela.
- O projeto utiliza a metodologia B.E.M. para estruturação do código CSS.
- A biblioteca Font Awesome foi utilizada para a inclusão de ícones nos pop-ups.
- As imagens foram convertidas para o formato WebP a fim de otimizar o tempo de carregamento.

## Considerações Finais

Este projeto demonstra minhas habilidades em desenvolvimento front-end, utilizando Vue.js, metodologia B.E.M. e melhores práticas de design e responsividade. Espero que este trabalho possa ser avaliado de forma positiva. Estou à disposição para fornecer qualquer informação adicional ou realizar uma demonstração ao vivo do projeto.

Obrigado pela oportunidade e consideração!
