<script>
  //@ts-nocheck
  import { Card, CardActions, CardText, Divider } from "svelte-materialify";

   export let el_mohdith =  ''
   export let el_rawi = ''
   export let grade = ''
   export let hadith = ''
   export let source = ''
   export let number_or_page = ''
  
</script>

<Card outlined style="margin-bottom:10px; padding:5px">
  <CardText >
   <p class="font-kitab-bold hadis">
      {hadith}
   </p>
  </CardText>
  <Divider />
  <CardActions style="direction:rtl">
   <div>
      <p class="font-kitab-bold mb-0">
         <small class="orange-text">{el_rawi}</small> -
         <small class="red-text">{grade}</small> -
         <small class="green-text">{el_mohdith}</small> -
         <small class="brown-text darken-1">{source}</small>
         <small class="brown-text darken-1">({number_or_page})</small>
      </p>
   </div>
  </CardActions>
</Card>

<style>
   .hadis {
      font-size: 16px;
      line-height: 25px;
   }
</style>