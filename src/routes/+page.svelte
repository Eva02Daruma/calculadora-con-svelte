<h1>Mi Calculadora</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<h1>Testing {name}</h1>
<button on:click={handleClick}>Click me : {count}</button>

<h1>testing calculator</h1>
<!-- lo mismo pero empezando desde la posicion 1 -->
<h3>Line :  {calcline.slice(1).join(' ')}</h3>
<h3> Resultado: {result} </h3>
<h3> Expression: {used_expression} </h3>

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
h1 {
  color: red;
  font-family: 'Comic Sans MS', cursive;
  font-size: 2em;
}


</style>
