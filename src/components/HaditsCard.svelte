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
  <CardText class="font-kitab-bold">
   {hadith}
  </CardText>
  <Divider />
  <CardActions style="direction:rtl">
   <div>
      <p class="font-kitab mb-0">
         <small>{el_rawi}</small> -
         <small>{el_mohdith}</small> -
         <small>{grade}</small> -
         <small>{source}</small> -
         <small>{number_or_page}</small>
      </p>
   </div>
  </CardActions>
</Card>
