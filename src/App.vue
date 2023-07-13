<template>
  <main class="conteudo flex justify-center items-center">
    <div class="flex gap-52">
      <!-- Form para calculo -->
      <div class="flex flex-col text-white h-[24em] p-6 rounded-3xl bg-blur border" v-if="form">
        <h1 class="text-center text-2xl mb-2 font-bold ">Calculo de IMC</h1>
        <div class="flex flex-col gap-4">
          <div>
            <p class="mb-2 font-semibold border-l-4 pl-1">Nome:</p>
            <input type="text" class=" font-semibold p-1 rounded-md w-[15em] bg-transparent border-2" v-model="nome"
              placeHolder="Digite seu nome:">
          </div>
          <div>
            <p class="mb-2 font-semibold border-l-4 pl-1">Peso:</p>
            <input type="number" class=" font-semibold p-1 rounded-md w-[15em] bg-transparent border-2" v-model="peso"
              placeHolder="Digite seu peso:">
          </div>
          <div>
            <p class="mb-2 font-semibold border-l-4 pl-1">Altura:</p>
            <input type="number" class=" font-semibold p-1 rounded-md w-[15em] bg-transparent border-2" v-model="altura"
              placeHolder="Digite sua altura:">
          </div>
          <button class="text-center border rounded-3xl hover:bg-white hover:text-black transition-all"
            @click="salvar()">Enviar</button>
        </div>
      </div>
      <!-- Resultado calculado -->
      <div class="text-white h-[24em] max-w-[802px] p-4 m-2 rounded-3xl bg-blur border" v-if="resultado">
        <h1 class="font-bold text-3xl md:text-6xl">Olá, {{ nome }}!</h1>
        <p class="mb-4 mt-2 md:mt-8 md:text-lg">Lembresse que idependente do resultado, você deve cuidar do seu corpo,
          adote hábitos saudáveis de alimentação e
          pratique exercícios físicos regularmente para manter um IMC dentro da faixa recomendada. Sua saúde física é
          valiosa, cuide dela!
        </p>
        <p class="font-semibold md:text-3xl sm:text-xl">Seu IMC é igual a: <span :class="qualidadeImc">{{ imc }}</span>
        </p>
        <p class="mt-2 md:text-3xl sm:text-xl">Isso significa que você tem: <span :class="qualidadeImc">{{ classificacao
        }}</span>
        </p>
        <div class="mt-4 text-xs sm:mt-32 md:mt-12 md:text-sm flex justify-between">
          <p>Consulte um nutricionista para mais informações!</p>
          <button class="border p-1 rounded-lg hover:text-black hover:bg-white transition-all" @click="refazer()">Nova
            pesquisa</button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      nome: "",
      peso: null,
      altura: null,
      imc: null,
      classificacao: "",
      qualidadeImc: "",
      form: true,
      resultado: false,
    }
  },
  methods: {
    salvar() {
      if (this.nome == null || this.nome == "") {
        alert("Você precisar digitar seu nome para continuarmos.")
      }
      else if (this.peso == null || this.peso == "") {
        alert("Você precisar digitar seu peso para continuarmos.")
      }
      else if (this.altura == null || this.altura == "") {
        alert("Você precisar digitar sua altura para continuarmos.")
      } else {
        this.calcularImc()
        if (this.imc == null || this.imc == "" || this.imc === "NaN" || this.imc <= 0.0) {
          alert("Ocorreu um erro com o calculo do IMC. Verifique os dados digitados e tente novamente!")
        } else {
          this.classificaResultado()
          this.form = false
          this.resultado = true
        }
      }
    },
    calcularImc() {
      this.imc = this.peso / (this.altura ** 2)
      this.imc = this.imc.toFixed(1)
    },
    classificaResultado() {
      if (this.imc < 18.5) {
        this.classificacao = "Abaixo do peso"
        this.qualidadeImc = "text-bold text-red-500"
      }
      else if (this.imc >= 18.5 && this.imc <= 24.9) {
        this.classificacao = "Peso normal"
        this.qualidadeImc = "text-bold text-green-500"
      }
      else if (this.imc >= 25 && this.imc <= 29.9) {
        this.classificacao = "Sobrepeso"
        this.qualidadeImc = "text-bold text-yellow-500"
      }
      else if (this.imc >= 30 && this.imc <= 34.9) {
        this.classificacao = "Obesidade Grau I"
        this.qualidadeImc = "text-bold text-red-500"
      }
      else if (this.imc >= 35 && this.imc <= 39.9) {
        this.classificacao = "Obesidade Grau II"
        this.qualidadeImc = "text-bold text-red-500"
      }
      else if (this.imc >= 40) {
        this.classificacao = "Obesidade Grau III (Obesidade mórbida)"
        this.qualidadeImc = "text-bold text-red-500"
      }
    },
    refazer() {
      location.reload();
    },
  },
};
</script>

<style scoped>
.conteudo {
  height: 100vh;
  background-image: url("https://wallpaperaccess.com/full/686946.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
.bg-blur {
  backdrop-filter: blur(10px);
}
</style>