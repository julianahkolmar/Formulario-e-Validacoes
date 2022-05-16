<template>
  <div class id="app">
    <div style="margin-right: auto;
    margin-left: auto;" class="cabecalho">
      <a class="setaEsquerda" href="#" type="image">
        <img style="display: flex;" src="https://img.icons8.com/ios-glyphs/30/ffffff/arrow-pointing-left--v2.png" />
      </a>
      <div style="margin-left: 60%; margin-right: auto">FORMULÁRIO</div>
    </div>
    <div>
      <div class="container">
        <div class="Loading"></div>
      </div>
    </div>
    <h1>Seja bem-vindo</h1>
    <form action="/action_page.php">
      <label for="dados">Dados do contato:</label>
      <p style="font-weight: 600px font-size: 14px; margin-bottom: 5%;">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        <br />
        Orci, volutpat in iaculis nec nibh nisl tellus.
      </p>
      <div></div>
      <div class id="forms">
        <div class id="full-box">
          <label class id="label-style" for="nomeCompleto">NOME COMPLETO</label>
          <input placeholder="Insira seu nome" type="text" pattern="([aA-zZ]+)" ref="nome" v-model="nome" id="nome"
            name="nome" required @blur="validarNome" />
          <p v-if="nomeError" class="textError">Nome não pode ser vazio</p>
          <p v-if="nomeLengthError" class="textError">
            Nome deve possuir, no mínimo, 3 caracteres
          </p>
        </div>
        <div class id="half-box">
          <div class="input-container">
            <label for="cadastrarEmail">EMAIL</label>
            <input placeholder="Insira seu email" type="email" v-model="email" ref="email" required id="email"
              name="email" @blur="validarEmail" />
          </div>
          <p v-if="emailError" class="textError">Email não pode ser vazio</p>
        </div>
        <div class id="half-box">
          <label class id="label-style" for="confirmarEmail">CONFIRMAR EMAIL</label>
          <input placeholder="Confirme seu email" type="email" ref="confemail" required v-model="cemail" id="confemail"
            name="confemail" @blur="validarConfemail" />
          <p v-if="cemailError" class="textError">Email não corresponde</p>
        </div>
        <div class id="half-box">
          <label class id="label-style" for="digitarCPF">CPF</label>
          <input placeholder="Digite seu CPF" type="text" v-mask="'###.###.###-##'" id="cpf" name="cpf" v-model="cpf"
            ref="cpf" required maxlength="14" minlength="11" @blur="validarCPF" />
          <p v-if="cpfError" class="textError">CPF não pode ser vazio</p>
          <p v-if="cpfLengthError" class="textError">CPF inválido</p>
          <p v-if="cpfOk" class="textValidate">CPF válido</p>
        </div>
        <div class id="half-box">
          <label class id="label-style" for="digitarCelular">CELULAR</label>
          <input required placeholder="(99) 99999-9999" type="tel" v-mask="'(##) #####-####'" ref="tel"
            v-model="celular" id="tel" name="tel" @blur="validarCelular" />
          <p v-if="celularError" class="textError">
            Número de celular não pode ser vazio
          </p>
          <p v-if="celularLengthError" class="textError">Celular inválido</p>
        </div>
        <div>
          <label class id="style-nasc" for="dataNasc" max="2004-05-10">DATA DE NASCIMENTO</label>
          <input id="nasc" type="date" ref="datanasc" v-model="nasc" placeholder="Digite sua data de nascimento"
            name="celular" class="form-control" @blur="validarNasc" />
          <p v-if="nascError" class="textError">
            Data de nascimento não pode ser vazia
          </p>
        </div>
      </div>
      <p style="font-size: 14px; font-weight: 600px">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
      <p style="font-size: 14px; margin-bottom: 5%; font-weight: 600px">Mattis semper odio pretium vestibulum nulla.</p>
    </form>
    <form>
      <div class="emailSms">
        <input type="checkbox" id="text" name="Email e SMS" />
        <label for="EmailSMS">Email e SMS</label>
      </div>
      <div class="whatsApp">
        <input type="checkbox" id="text1" name="WhatsApp" />
        <label for="WhatsApp">WhatsApp</label>
      </div>
    </form>
    <p style="font-weight: 600pxfont-size: 14px; margin-top: 5%;">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Orci, volutpat in
      iaculis nec nibh nisl tellus.
      Amet tellus nunc dolor magna aliquet risus. Habitant neque, id risus diam.
    </p>
    <a href="#">
      Continuar
      <div class="arrow-wrapper">
        <div class="arrow"></div>
      </div>
    </a>
    <footer></footer>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      nome: "",
      email: "",
      cemail: "",
      cpf: "",
      celular: "",
      nasc: "",
      nomeError: false,
      nomeLengthError: false,
      emailError: false,
      cemailError: false,
      cpfError: false,
      cpfLengthError: false,
      celularError: false,
      celularLengthError: false,
      nascError: false,
    };
  },
  methods: {
    validarNome() {
      this.nomeError = this.nome === "";
      this.nomeLengthError = this.nome.length < 3 && this.nome.length > 0;
    },
    validarEmail() {
      this.emailError = this.email === "";
    },
    validarConfemail() {
      this.cemailError = this.cemail !== this.email;
    },
     validarCPF() {
      this.cpfSemMascara = this.cpf.replace(/[^0-9]/g, '')
      this.cpfError = this.cpfSemMascara === "";
      this.cpfLengthError = this.cpfSemMascara.length !== 11 && this.cpfSemMascara.length > 0;

      if (
        ["00000000000",
          "11111111111",
          "22222222222",
          "33333333333",
          "44444444444",
          "55555555555",
          "66666666666",
          "77777777777",
          "88888888888",
          "99999999999",
        ].indexOf(this.cpfSemMascara) !== -1
      )
        this.cpfLengthError = true

      this.soma = 0;
      this.resto;
      this.i;
      for (let i = 1; i <= 9; i++)
        this.soma =
          this.soma + parseInt(this.cpfSemMascara.substring(i - 1, i)) * (11 - i);
      this.resto = (this.soma * 10) % 11;
      if (this.resto == 10 || this.resto == 11) this.resto = 0;
      if (this.resto != parseInt(this.cpfSemMascara.substring(9, 10)))
        this.cpfLengthError = true;
      this.soma = 0;

      for (let i = 1; i <= 10; i++)
        this.soma =
          this.soma + parseInt(this.cpfSemMascara.substring(i - 1, i)) * (12 - i);

      this.resto = (this.soma * 10) % 11;

      if (this.resto == 10 || this.resto == 11) this.resto = 0;

      if (this.resto != parseInt(this.cpfSemMascara.substring(10, 11)))
        this.cpfLengthError = true
    },
    validarCelular() {
      this.celularError = this.celular === "";
      this.celularLengthError =
        this.celular.length < 11 && this.celular.length > 0;
    },
    validarNasc() {
      this.nascError = this.nascError === "";
    },
  },
};
</script>

<style>
#app {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 200;
  font-display: swap;
  font-weight: 600;
  position: relative;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #1f1c1c;
  margin-top: 3%;
  margin-bottom: -5%;
  text-align: justify;
  background-color: white;
  margin-right: 35%;
  margin-left: -7px;
  padding: 15%;
}

#label-style {
  float: left;
}

#style-nasc {
  display: flex;
}

body {
  background-color: #e82c54;

}

#forms {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  background-color: white;
  font-size: 12px;
  font-weight:700px;
}

#full-box {
  flex: 1 1 100%;
  position: relative;
}

footer {
  margin-bottom: -20%;
}

#half-box {
  flex: 1 1 45%;
  position: relative;
  margin-right: 2.5%;
}

#forms input {
  width: 100%;
  padding: 10px 10px;
  margin: 8px 0;
  border-color: 0.5px solid rgb(209, 200, 200);
  border-radius: 5px;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 600px;
  font-display: swap;
  box-sizing: border-box;
  transition: 500ms ease-in-out;
}

input:hover {
  border: 2px solid #e82c54;
  transition: 500ms ease-in-out;
}

a {
  --primary-color: #e82c54;
  --secondary-color: #fff;
  --hover-color: #111;
  --arrow-width: 10px;
  --arrow-stroke: 2px;
  box-sizing: border-box;
  text-decoration: none;
  font-family: 'Inter';
  font-style: normal;
  border: 0;
  border-radius: 20px;
  color: var(--secondary-color);
  padding: 1em 1.4em;
  background: var(--primary-color);
  display: flex;
  transition: 0.2s background;
  align-items: center;
  gap: 0.6em;
  width: 130px;
  height: 40px;
  font-weight: bold;
}

a .arrow-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

a .arrow {
  margin-top: 1px;
  width: var(--arrow-width);
  background: var(--primary-color);
  height: var(--arrow-stroke);
  position: relative;
  transition: 0.2s;
}

a .arrow::before {
  content: "";
  box-sizing: border-box;
  position: absolute;
  border: solid var(--secondary-color);
  border-width: 0 var(--arrow-stroke) var(--arrow-stroke) 0;
  display: inline-block;
  top: -3px;
  right: 3px;
  transition: 0.2s;
  padding: 3px;
  transform: rotate(-45deg);
}

a:hover .arrow {
  background: var(--secondary-color);
}

a:hover .arrow:before {
  right: 0;
}

@font-face {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 200;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/inter/v11/UcC73FwrK3iLTeHuS_fvQtMwCp50KnMa1ZL7.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}

.cabecalho {
  display: flex;
  justify-content: center;
  width: 200%;
  padding: 2%;
  color: white;
  font-family: 'Inter';
  font-display: swap;
  font-size: 15px;
  margin-top: -50%;

}

.textError {
  color: red;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 600px;
  font-display: swap;
  font-size: 10px;
  margin-top: -1%;
}

.textValidate {
  color: yellowgreen;
  font-size: 10px;
  margin-top: -1%;
}

.whatsApp {
  flex: 1 1 100%;
  position: relative;
  font-size: 14px;
}

.emailSms {
  flex: 1 1 100%;
  position: relative;
  font-size: 14px;
}


.container {
  position: relative;
  width: 120%;
  margin-top: 10%;
  margin-left: -9%;
  margin-bottom: 10%;
  padding: 10px 50px;
  border-radius: 4px;
  box-sizing: border-box;
  background: #fff;

}

.Loading {
  position: relative;
  display: inline-block;
  width: 100%;
  height: 10px;
  background: #f1f1f1;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, .2);
  border-radius: 4px;
  overflow: hidden;
}

.Loading:after {
  content: '';
  position: absolute;
  left: 0;
  width: 0;
  height: 100%;
  border-radius: 4px;
  box-shadow: 0 0 5px rgba(0, 0, 0, .2);
  animation: load 2s ease-in-out;
  animation-fill-mode: forwards;
}

@keyframes load {
  from {
    width: 0%;
    background: #ee4b6e;
  }

  to {
    width: 50%;
    background: #ee4b6e;
  }

}

/*50% {
    width: 50%;
    background: #e82c54;
  }
  
 /* 75% {
    width: 75%;
    background: #d0bdf4;
  }
  
  100% {
    width: 100%;
    background: #494d5f;
  }*/

@keyframes pulse {
  0% {
    background: #a28089;
  }

  25% {
    background: #a0d2eb;
  }

  50% {
    background: #ffa8b6;
  }

  75% {
    background: #d0bdf4;
  }

  100% {
    background: #494d5f;
  }
}

.image {}

.setaEsquerda {
  margin-left: -22%;
  width: 20px;
  height: 20px;
  margin-top: -0.5%;
}

.emailSMS input,
.whatsApp input {
  margin-top: 4%;
}

h1 {
  margin-top: -5%;
  margin-bottom: 5%;
  font-size: 43px;
  font-family: Century Gothic, CenturyGothic, AppleGothic, sans-serif;
  font-style: normal;
  font-variant: normal;

}
</style>