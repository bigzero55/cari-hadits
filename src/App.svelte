<script>
  //@ts-nocheck
  import {
    MaterialApp,
    Button,
    TextField,
    Card,
    CardText,
  } from "svelte-materialify";
  import { mdiMenu, mdiDotsVertical } from "@mdi/js";
  import { writable } from "svelte/store";
  import HaditsCard from "./components/HaditsCard.svelte";

  let datahadits = writable();

  let keys = "النيات";

  async function check(key) {
    const result = await fetch(
      `https://dorar-hadith-api.cyclic.app/api/search?value=${key}`
    );
    const data = await result.json();
    datahadits.set(data);
    console.log(data);
  }

  function CariHadits() {
    check(keys);
  }
</script>

<MaterialApp>
  <div class="header">
    <Card outlined class="">
      <CardText class="">
        <div class="text-center mb-2">
          <div class="text-h5 font-weight-black">Cari Hadits</div>
        </div>
        <div class="pl-4 pr-4 pt-3">
          <div class="ma-2">
            <TextField
              dense
              rounded
              outlined
              class="font-kitab"
              bind:value={keys}>Masukan Kata Kunci</TextField
            >
            <div class="mt-2">
              <Button on:click={CariHadits} rounded>Cari</Button>
            </div>
          </div>
        </div>
      </CardText>
    </Card>
  </div>

  <div class="pl-2 pr-2 bod">
    {#if $datahadits != undefined}
      {#each $datahadits as hadits}
        <HaditsCard {...hadits} />
      {/each}
    {/if}
  </div>
</MaterialApp>

<style>
  .header {
    width: 100%;
    position: fixed;
    z-index: 1;
  }

  .bod {
    padding-top: 200px;
    padding-bottom: 50px;
    background-color: antiquewhite;
  }
</style>
