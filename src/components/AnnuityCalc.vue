<template>
  <div class="calc">
    <h2>Аннуитетный калькулятор</h2>
  <form @submit.prevent="calculateAnn">
    <div>
      <label>Сумма кредита:</label>
      <el-input v-model.number="loanAmount" />
    </div>
    <div>
      <label>Процентная ставка</label>
      <el-input v-model.number="interestRate" />
    </div>
    <div>
      <label>Срок кредита(месяцев)</label>
      <el-input v-model.number="loanTerm" />
    </div>
    <button class="btn" type="submit">Рассчитать</button>
  </form>
  <p>Ваш месячный платеж составит: {{ monthPayment.toFixed(2) }}</p>
  </div>
</template>
<script>
export default {
  name: "AnnuityCalc",
  data() {
    return {
      monthPayment :0, //Ежемесячный платёж
      loanAmount : 0, //Сумма кредита
      interestRate : 0, //Ежемесячная процентная ставка
      loanTerm :  0,//Cрок кредита
    };
  },
  methods: {
    calculateAnn() {
      this.ym = this.interestRate/100/12;
      this.monthPayment = Math.round(this.loanAmount*(this.ym+(this.ym/((1+this.ym)**this.loanTerm-1))));
    },
  },
};
</script>
<style scoped>
.btn {
  position: relative;
  left: 50%;
  transform: translate(-50%, 0);
  display: block;
  width: 200px;
  height: 36px;
  border-radius: 18px;
  background-color:#009B77;
  border: solid 1px transparent;
  color: #fff;
  font-size: 18px;
  font-weight: 300;
  cursor: pointer;
  transition: all .1s ease-in-out;
}

.calc{
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  padding: 40px;
  transform: translate(-50%, -50%);
  background: rgba(0, 0, 0, 0.883);
  box-sizing: border-box;
  box-shadow: 0 15px 25px rgba(0,0,0,.6);
  border-radius: 10px;
}

.calc h2 {
  margin: 0 0 30px;
  padding: 0;
  color: #fff;
  text-align: center;
}
.calc label {
  margin: 0 0 30px;
  padding: 0;
  color: #fff;
  text-align: center;
}
.calc p {
  margin: 0 0 30px;
  padding: 0;
  color: #fff;
  text-align: center;
}

</style>
