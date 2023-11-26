<h1>Mi Calculadora</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<h1>Testing {name}</h1>
<button class="btn btn-primary " on:click={handleClick}>Click me : {count}</button>

<div class="container py-4 px-3 mx-auto">
    <h1 class="titulo">Calculadora</h1>
<!-- lo mismo pero empezando desde la posicion 1 -->

<div class="caja">
    <h2>Calculo :  {calcline.slice(1).join(' ')}</h2>
    <h1> Resultado: {result} </h1>
    <h4> Expression: {used_expression} </h4>
</div>



<div class="calculadora">
    <div>
        <button on:click={() => add(1)}>1</button>
        <button on:click={() => add(2)}>2</button>
        <button on:click={() => add(3)}>3</button>
        <button on:click={() => handleOperator('+')}>+</button>
      </div>
      <div>
        <button on:click={() => add(4)}>4</button>
        <button on:click={() => add(5)}>5</button>
        <button on:click={() => add(6)}>6</button>
        <button on:click={() => handleOperator('-')}>-</button>
      </div>
      <div>
        <button on:click={() => add(7)}>7</button>
        <button on:click={() => add(8)}>8</button>
        <button on:click={() => add(9)}>9</button>
        <button on:click={() => handleOperator('*')}>*</button>
      </div>
      <div>
        <button on:click={() => add(0)}>0</button>
        <button on:click={() => add('.')}>.</button>
        <button on:click={() => handleOperator('/')}>/</button>
      </div>
      <div>
        <button on:click={resetArray}>Reset</button>
      </div>
      <button on:click={calculateResult}>Calcular</button>
</div>

</div>


<script> 
let name = 'world';
let count = 0;
let calcline = [0];
let result = 0;
let used_expression = '';
// functions
function handleClick() {
  count += 1;
}

//add function with 1 parameter to add to array
function add(num){
    calcline.push(num);
    calcline = calcline;
}

  // Function to handle operator clicks
  function handleOperator(operator) {
    // You can implement logic here to handle operators
    // For now, let's just log the operator to the console
    console.log('Operator:', operator);
    calcline.push(operator);
  }


  // Function to reset the array
  function resetArray() {
    calcline = [0];
  }


// Function to calculate the result
function calculateResult() {
    // Remove the first element (0) and join the rest into a string
    let expression = calcline.slice(1).join('');
    used_expression = expression.replace(/x/g, '*').replace(/÷/g, '/').toString();

    try {
      // Use the Function constructor to create a function from the expression
      // and then call that function to get the result
      result = new Function('return ' + expression)();
      alert(result);
      resetArray();

      return result;
    } catch (error) {
      alert('Error in expression');
      resetArray();
      return 0;
    }
  }



$: if (count >= 10){
		alert('count is dangerously high!');
		count = 0;
	}

</script>

<style>
/* estilo titulo */
.titulo {
  text-align: center;
  color: #0A66C2;
}
/* estilo caja */


 /* estilo calculadora */

.calculadora {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.calculadora button {
    /* https://getcssscan.com/css-buttons-examples */
  align-items: center;
  background-color: #0A66C2;
  border: 0;
  border-radius: 100px;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-flex;
  font-family: -apple-system, system-ui, system-ui, "Segoe UI", Roboto, "Helvetica Neue", "Fira Sans", Ubuntu, Oxygen, "Oxygen Sans", Cantarell, "Droid Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Lucida Grande", Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 600;
  justify-content: center;
  line-height: 20px;
  max-width: 480px;
  min-height: 40px;
  min-width: 0px;
  overflow: hidden;
  padding: 0px;
  padding-left: 20px;
  padding-right: 20px;
  text-align: center;
  touch-action: manipulation;
  transition: background-color 0.167s cubic-bezier(0.4, 0, 0.2, 1) 0s, box-shadow 0.167s cubic-bezier(0.4, 0, 0.2, 1) 0s, color 0.167s cubic-bezier(0.4, 0, 0.2, 1) 0s;
  user-select: none;
  -webkit-user-select: none;
  vertical-align: middle;
}

.calculadora button:hover {
    background-color: #16437E;
    color: #ffffff;
}

</style>
