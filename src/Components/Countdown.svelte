<script>
  const startTime = Date.now();
  let teste = "";

  const timer = setInterval(function () {
    let time = Date.now();
    let diff = time - startTime;
    let minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
    let seconds = Math.floor((diff % (1000 * 60)) / 1000);
    let milliseconds = Math.floor((diff % (1000 * 60))) % 1000;

    teste = `${minutes}:${seconds}:${milliseconds}`;
  }, 10);

</script>

<p>
  {teste}
</p>