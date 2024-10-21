<script lang="ts">
  import scrypt from "scrypt-js";
  import { Buffer } from "buffer";

  let secret = "";
  let salt = "";
  let result = "";

  function generatePassword() {
    console.time("Scrypt");

    const res = scrypt.syncScrypt(
      Buffer.from(secret),
      Buffer.from(salt),
      2 ** 16,
      8,
      1,
      16
    );

    console.timeEnd("Scrypt");

    result = btoa(
      Array.from(res)
        .map((b) => b.toString(16))
        .join("")
    );
  }
</script>

<h1>My Scrypt</h1>
<p>This Is My Scrypt To Make It Simple For Me</p>

<div class="box">
  <input placeholder="Secret" bind:value={secret} />
  <input placeholder="Salt" bind:value={salt} />
  <button on:click={generatePassword}>Generate</button>
</div>

{#if result}
  <div class="result">
    <input placeholder="Result" readonly value={result} />
  </div>
{/if}

<style>
  .box {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .result {
    display: flex;
    flex-direction: column;
    margin-top: 1rem;
  }

  input,
  button {
    height: 2.5rem;
  }
</style>
