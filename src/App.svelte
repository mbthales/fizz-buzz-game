<script>
  import Countdown from "./Components/Countdown.svelte";

  let numsAndMsgs = [];
  let record = JSON.parse(localStorage.getItem("record")) || 0;
  let count = 0;
  let start = false;
  let loser = false;

  const fillArrayWithNumsAndMsgs = () => {
    for (let i = 1; i <= 100; i++) {
      if (i % 15 === 0) {
        numsAndMsgs.push({
          num: i,
          msg: "FizzBuzz",
        });
      } else if (i % 3 === 0) {
        numsAndMsgs.push({
          num: i,
          msg: "Fizz",
        });
      } else if (i % 5 === 0) {
        numsAndMsgs.push({
          num: i,
          msg: "Buzz",
        });
      } else {
        numsAndMsgs.push({
          num: i,
          msg: i.toString(),
        });
      }
    }
  };

  const handleWithBtns = (e) => {
    if (!loser) {
      if (e.target.innerHTML === numsAndMsgs[count].msg) {
        count++;
      } else {
        loser = true;
        checkIfUserBeatHisRecord();
      }
    }
  };

  const checkIfUserBeatHisRecord = () => {
    if (numsAndMsgs[count].num > JSON.parse(localStorage.getItem("record"))) {
      localStorage.setItem("record", JSON.stringify(numsAndMsgs[count].num));
      record = numsAndMsgs[count].num;
    }
  };

  const restartGame = () => {
    count = 0;
    loser = false;
  };

  fillArrayWithNumsAndMsgs();
</script>

<main>
  {#if !start}
    <h1>Fizz Buzz Game</h1>
    <p>
      Aperte "Fizz" quando o número for dívisivel por 3, "Buzz" quando for por 5
      e "FizzBuzz" quando for por 15. Se o número não se enquadrar em nenhuma
      opção anterior, clique no botão do próprio número. Vamos começar?
    </p>
    <button on:click={() => (start = true)}>Start</button>
  {:else}
    <Countdown />
    <p>{numsAndMsgs[count].num}</p>
    <div on:click={(e) => handleWithBtns(e)}>
      <button>Fizz</button>
      <button>Buzz</button>
      <button>FizzBuzz</button>
      <button>{numsAndMsgs[count].num}</button>
    </div>
    {#if loser}
      <p>Your record: {record}</p>
      <p>You Lost!</p>
      <button on:click={restartGame}>Restart</button>
    {/if}
  {/if}
</main>
