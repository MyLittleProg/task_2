<script lang="ts">

 //Первое число
 let amount = 0.00;
 
 //Конвертация ИЗ
 let convertFrom = 'USD';
 
 //Второе число
 let finalAmount = 0;

 //Конвертация В
 let convertTo = 'RUB';


 //Сюда просто добавлять код и название валюты
 let currencyList = [
 {name: "USD", desc:"US Dollar"},
 {name:"EUR", desc:"Euro"},
 {name:"RUB", desc:"Рубли"},
 {name:"INR", desc:"Indian Rupee"},
 {name:"GBP", desc:"Фунт Стерлингов"},
 ];



 
 //https://v6.exchangerate-api.com/v6/be968a8df40fe03c77ccf282/       <- api key

//Асинхронные функции с fetch запросом для доступа к курсам валют 
async function convertCurrency() {
  let curKey = convertFrom
  let url = "https://v6.exchangerate-api.com/v6/be968a8df40fe03c77ccf282/latest/" + curKey;
  await fetch(url).then(response => {
  return response.json();
  }).then(data => {
    let rate = data.conversion_rates[convertTo];
    finalAmount = rate * amount;
    
  });
 }

 async function convertCurrencyAmount() {
  let curKey = convertTo
  let url = "https://v6.exchangerate-api.com/v6/be968a8df40fe03c77ccf282/latest/" + curKey;
  await fetch(url).then(response => {
  return response.json();
  }).then(data => {
    let rate = data.conversion_rates[convertFrom];
    amount = rate * finalAmount;
    
  });
 }
</script>

<main>
  <h1>Конвертация валют</h1>
  <select name="" bind:value={convertFrom}>
    {#each currencyList as cl}
    <option value="{cl.name}">{cl.desc}</option>
    {/each}
  </select>
  <input type="number" on:change={convertCurrency} bind:value="{amount}" >
  <br>
  <br>
  <p>Равно</p>
  <br>
  
  <select name="" bind:value={convertTo}>
    {#each currencyList as cl}
    <option value="{cl.name}">{cl.desc}</option>
    {/each}
  </select>
  <input type="number" on:change={convertCurrencyAmount} bind:value="{finalAmount}">

</main>

<style>
  
</style>
