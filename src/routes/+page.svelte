<script>
  let name = "world";
  let count = 0;
  let calcline = [0];
  let result = 0;
  let used_expression = "";
  // functions
  function handleClick() {
    count += 1;
  }

  //add function with 1 parameter to add to array
  function add(num) {
    calcline.push(num);
    calcline = calcline;
  }

  // Function to handle operator clicks
  function handleOperator(operator) {
    // You can implement logic here to handle operators
    // For now, let's just log the operator to the console
    console.log("Operator:", operator);
    calcline.push(operator);
  }

  // Function to reset the array
  function resetArray() {
    calcline = [0];
  }

  // Function to calculate the result
  function calculateResult() {
    // Remove the first element (0) and join the rest into a string
    let expression = calcline.slice(1).join("");
    used_expression = expression
      .replace(/x/g, "*")
      .replace(/÷/g, "/")
      .toString();

    try {
      // Use the Function constructor to create a function from the expression
      // and then call that function to get the result
      result = new Function("return " + expression)();
      resetArray();

      return result;
    } catch (error) {
      alert("Error in expression");
      resetArray();
      return 0;
    }
  }

  $: if (count >= 10) {
    alert("count is dangerously high!");
    count = 0;
  }
</script>

<!--Color pallete-->

<h1>Mi Calculadora</h1>
<p>
  Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation
</p>

<h1>Testing {name}</h1>
<button class="btn btn-primary" on:click={handleClick}
  >Click me : {count}</button
>

<!-- App -->
<div class="app container py-4 px-3 mx-auto border my-3">
  <h1 class="titulo">Calculadora</h1>

  <div class="caja container p-1 m-15 border">
    <h2>Calculo : {calcline.slice(1).join(" ")}</h2>
    <h1>Resultado: {result}</h1>
    <h4>Expression: {used_expression}</h4>
  </div>

  <!-- calculadora -->
  <div class="calculadora">
    <div>
      <button on:click={() => add(1)}>1</button>
      <button on:click={() => add(2)}>2</button>
      <button on:click={() => add(3)}>3</button>
      <button on:click={() => handleOperator("+")}>+</button>
    </div>
    <div>
      <button on:click={() => add(4)}>4</button>
      <button on:click={() => add(5)}>5</button>
      <button on:click={() => add(6)}>6</button>
      <button on:click={() => handleOperator("-")}>-</button>
    </div>
    <div>
      <button on:click={() => add(7)}>7</button>
      <button on:click={() => add(8)}>8</button>
      <button on:click={() => add(9)}>9</button>
      <button on:click={() => handleOperator("*")}>*</button>
    </div>
    <div>
      <button on:click={() => add(0)}>0</button>
      <button on:click={() => add(".")}>.</button>
      <button on:click={() => handleOperator("/")}>/</button>
    </div>
    <div>
      <button on:click={resetArray}>Reset</button>
    </div>
    <button on:click={calculateResult}>Calcular</button>
  </div>
</div>

<style lang="scss">
  @import "../style/estilo.scss";
</style>
