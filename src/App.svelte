<script>
  //@ts-nocheck
  import { MaterialApp, AppBar,Button, Icon, ListItem, Menu, TextField, Card, CardText, CardActions } from 'svelte-materialify';
  import { mdiMenu , mdiDotsVertical} from '@mdi/js'
  import { writable } from 'svelte/store'

  let datahadits = writable()
  
  let theme = 'light';
  let keys = 'النيات'

  function toggleTheme() {
    if (theme === 'light') theme = 'dark';
    else theme = 'light';
  }

  async function check (key) {
    const result = await fetch(`https://dorar-hadith-api.cyclic.app/api/search?value=${key}`)
    const data = await result.json()
    datahadits.set(data)
    console.log(data)
  }

  function CariHadits() {
    check(keys)
  }

</script>

<MaterialApp {theme}>
  <AppBar>
    <!-- <div slot="icon">
      <Button fab depressed>
        <Icon path={mdiMenu} />
      </Button>
    </div> -->
    <span slot="title">Cari Hadits</span>
    <div style="flex-grow:1" />
    <!-- <Button>Item</Button> -->
    <Menu right>
      <div slot="activator">
        <Button fab depressed>
          <Icon path={mdiDotsVertical} />
        </Button>
      </div>
      <ListItem>Item 1</ListItem>
      <ListItem>Item 2</ListItem>
      <ListItem>Item 3</ListItem>
    </Menu>
  </AppBar>

  <div class="ma-5">
    <TextField dense rounded outlined
    bind:value={keys}
    >masukan kata kunci</TextField> 
    <div class="mt-2">
      <Button on:click={CariHadits} rounded >Cari</Button>
    </div>
  </div>

  <div class="ma-2">
    {#if $datahadits != undefined}
      {#each $datahadits as hadits}
        <Card outlined >
          <div class="pl-4 pr-4 pt-3">
            <span class="text-overline font-kitab-bold">{hadits.el_mohdith}</span>
            <br />
            <span class="text-h5 mb-2 font-kitab-bold">{hadits.el_rawi}</span>
            <br />
          </div>
          <CardText class="font-kitab">
            {hadits.hadith}
          </CardText>
        </Card>
      {/each}
    {/if}
  </div>
</MaterialApp>