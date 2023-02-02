<script>
  //@ts-nocheck
  import {
    Icon,
    MaterialApp,
    Button,
    TextField,
    Card,
    CardText,
    ProgressCircular,
  } from "svelte-materialify";
  import { mdiBookSearchOutline } from "@mdi/js";
  import { writable } from "svelte/store";
  import HaditsCard from "./components/HaditsCard.svelte";
  import { Clock } from "svelte-loading-spinners";

  let datahadits = writable([]);

  let keys = "النيات";
  let load = false;
  async function check(key) {
    const result = await fetch(
      `https://dorar-hadith-api.cyclic.app/api/search?value=${key}`
    );
    const data = await result.json();
    datahadits.set(data);
    console.log(data);
  }

  function CariHadits(key) {
    load = true;
    check(key);
    console.log(key);
  }

  $: if ($datahadits.length > 0) {
    load = false;
  }
</script>

<MaterialApp>
  <div class="header">
    <Card outlined class="">
      <CardText class="">
        <div class="text-center mb-2">
          <h3 class="text-h3 font-weight-black orange-text">Cari Hadits</h3>
        </div>
        <div class="pl-4 pr-4 pt-3">
          <div class="ma-2">
            <form on:submit|preventDefault={() => CariHadits(keys)}>
              <TextField
                clearable 
                dense
                rounded
                outlined
                class="font-kitab"
                bind:value={keys}>Masukan Kata Kunci</TextField
              >
              <div class="mt-2">
                <Button type="submit" rounded class="orange white-text">
                  <Icon path={mdiBookSearchOutline} class="mr-2" />
                  Cari
                </Button>
              </div>
            </form>
          </div>
        </div>
      </CardText>
    </Card>
  </div>

  <div class="pl-2 pr-2 bod">
    {#if $datahadits != []}
      {#each $datahadits as hadits}
        <HaditsCard {...hadits} />
      {/each}
    {/if}

    {#if load}
      <div class="loading text-center">
        <ProgressCircular size={70} width={2} indeterminate color="orange" />
      </div>
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
    padding-top: 220px;
    padding-bottom: 50px;
    background-color: antiquewhite;
  }

  .loading {
    margin-top: 200px;
    width: 100%;
    align-items: center;
  }
</style>
