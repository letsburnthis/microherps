<script>
	//pull up on grey bar and set toggle on bottom of screen to "output"
	
	
	import PersonProfile from "./PersonProfile.svelte"
	
	
	let howBig= 3;
	
	let microHerps;
	let howSerious="!";

	
	let data = [{alias:"sexytime partner#1", partnersNum:0, partnerHerp:0, herps:5, flareup:0, protection:0}]

	
	
	
	function addPerson(){
		console.log("tried to add a person")
		data.push({alias:"", partnersNum:0, herps:5, flareup:0, tested:0, protection:1});
		data[data.length-1].alias="sexytimepartner#"+(data.length);
		data=data;
		howBig=data.length+2;
		
	}
	
	function removePerson(place){
		data.splice(place,1);
		data=data;
		howBig=data.length+2;
	
	}
	
	
	
//calculation should basically be chance the have herpes*chance you will contract it
	//based on either a diagnosis or chance they have it
	//chance they have it would be whatever the U.S. average is if they have had the average number of sex partners?
	//chance they would transmit it (assuming they had it) is based on the chance they are shedding and the chance the //shedding isn't stopped by a barrier
	//your overall risk would be the inverse of the chance of not catching it from any partner aka if heads was getting it //and tails was not, the inverse of the chance of flipping all tails (since if any flip is a heads, you now have herpes)
	
	function calculate(){
		var risks=[];
		var p=0;
		while(p<data.length){
			var risk=0;
			if(data[p].herps==1){
				risk = 1*.3;
			}
			if(data[p].flareup==1){
				risk =1*1;
			}
			if(risk>=.3){
				console.log("had risk because of herps")
				if(data[p].protection==1){
					risks.push(1-(risk*.15));
				}
				else{
					risks.push(1-risk*.8);
				}
				p=p+1;
				continue
			}
			console.log("got past herpes");
			if(data[p].partnersNum>0){
				console.log("calculating risk");
				risk=risk+data[p].partnersNum*.05;
				console.log("risk from partners ="+risk)
			}
			if(data[p].partnerHerp==1){
				risk=risk*2;
			}
			
			if(risk>1){
				risk=1;
			}
			if(data[p].protection==1){
				risks.push(1-risk*.15*.3);
			}
			else{
				risks.push(1-risk*.8*.3);
			}
			p=p+1;

		}
		
		//calculate microherps from combined risk
		console.log("calculating")
		const reducer = (accumulator, currentValue) => accumulator * currentValue;
		
		microHerps=Math.round((1- risks.reduce(reducer))*1000000);
		
		if(microHerps<100000){
			howSerious="."
		}
		else{
			howSerious="!";
			howSerious=howSerious.repeat(Math.round(microHerps/100000))
		}
		
		
	}
	
</script>




<div class="grid-container">
{#each data as {alias, partnersNum, partnerHerp, herps, flareup, protection},i}
<div class="grid-item">
	
	
{#if data.length>1}

	<button style="background-color:pink" on:click={()=>removePerson(i)}>
		I've decided not to have sex with {data[i].alias}
	</button> 
{/if}
<PersonProfile bind:profile={data[i]} />
</div>

{/each}
</div>


<br><br><br>
<button on:click={addPerson}>
	Actually, I'm having a {howBig}-some
</button>

<br><br>

<button on:click={calculate}>
	Calculate event microHerps
</button>



<p>
	You are facing {microHerps} microHerps{howSerious}
</p>

<style>
.grid-container {
  display: inline-grid;
  grid-template-columns: auto auto auto;
  background-color: #2196F3;
  padding: 5px;
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 5px;
  font-size: 20px;
  text-align: center;
}
</style>



<p>
	Data that went into this:
	<br>
	80% of herpes shedding episodes are asymphtomatic. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4006256/
	<br>
	12% of the U.S. population has HPV-2 (genital herpes) https://www.livescience.com/61681-herpes-infections-united-states.html
	<br>
	Less than 10 percent of all those who were seropositive reported a history of genital herpes https://www.nejm.org/doi/full/10.1056/NEJM199710163371601 (not sure how accurate this info still is).
	<br>
	proper condom use prevents infection in 96% of infected-male/herpes-free-female and 65% of infected-female/herpes-free-male sexual encounters https://stdcenterny.com/articles/protected-herpes-transmission.html#condom
	<br>
	
	
</p>





