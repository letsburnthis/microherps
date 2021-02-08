<script>



export let profile = {alias:"", partnersNum:0, partnerHerp:0, herps:5, flareup:0, tested:0, protection:1}
//sets flareup to zero if input on whether partner has herpes is changed to no
$: if(profile.herps==0){
	profile.flareup=0;
}
	

</script>

 <form>
  <label for="alias">alias:</label>
  <input bind:value ={profile.alias} type="text" id="alias" name="alias">

	 
  <label for="partners">How many sexual partners have they had since last testing negative?</label>
  <input bind:value={profile.partnersNum} type="number" id="partners" name="partners">

	{#if profile.partnersNum >0}
		<label  for="partnerHerps">Did any of these partners had Herpes?</label>
		<label  for="yes">Yes</label>
 		<input bind:group={profile.partnerHerp} type="radio" id="partnerHerpYes" name="partnerHerp" value=1>
		<label for="no">No</label>
		<input  bind:group={profile.partnerHerp}  type="radio" id="partnerHerpNo" name="partnerHerp" value=0>
		
	{/if} 
	 
	 
	<label  for="herps">Do you already know {profile.alias} has Herps (that's for life)?</label>
	<label  for="yes">Yes</label>
 	<input bind:group={profile.herps}  type="radio" id="herpsYes" name="herps" value=1>
	<label for="no">No</label>
	<input bind:group={profile.herps}  type="radio" id="herpsNo" name="herps" value=0>
	 
	 

	
	 
	{#if profile.herps == 1}
		<label  for="herps">Are they having a flare up?</label>
		<label  for="yes">Yes</label>
 		<input bind:group={profile.flareup} type="radio" id="flareupYes" name="flareup" value=1>
		<label for="no">No</label>
		<input bind:group={profile.flareup}  type="radio" id="flareupNo" name="flareup" value=0>
		
	{/if}
	 
	 
	 
	<label for="protection">Are you going to use protection?</label>
	<label for="yes">Yes</label>
 	<input bind:group={profile.protection} type="radio" id="protectionYes" name="protection" value=1>
	<label for="no">No</label>
	<input bind:group={profile.protection} type="radio" id="protectinNo" name="protection" value=0>

	 
	 
</form> 





