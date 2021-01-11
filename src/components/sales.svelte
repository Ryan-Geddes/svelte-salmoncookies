<script>

  let hoursOpen = 14;
    
	let stores = [
		{
			name: 'Seattle',
			min : 23,
			max : 65,
			saleAvg : 6.3,
			hourlySales:[],
		},
		{
			name : 'Tokyo',
			min : 3,
			max : 24,
			saleAvg : 1.2,
			hourlySales:[],
		},
		{
			name: 'Dubai',
			min : 11,
			max : 38,
			saleAvg : 3.7,
			hourlySales:[],
		},
		{
			name: 'Paris',
			min : 20,
			max : 38,
			saleAvg : 2.3,
			hourlySales:[],
		},
		{
			name: 'Lima',
			min : 2,
			max : 16,
			saleAvg : 4.6,
			hourlySales:[],
		}
	]

	let showReport = 'none';
	let addNewStore = 'none';

	function toggleAddStore () {
		addNewStore = addNewStore==='none'? 'block' : 'none';
	}


	function toggleReport () {
		showReport = showReport==='none'? 'block' : 'none';
		
		showReport !== 'none' && reportGenerator(); 

	}

	function reportGenerator (){
		//1. for each store, loop 14 times;
		//for each store
				// loop 14 times...
						// randomly select a number between store.min & store.max (random)
						// Multiply that random number * store.saleAvg = sale per THAT hour.
						// append it to the table.
				//
		stores.forEach (store => {
			store.hourlySales = [];
			for (let i = 0; i < hoursOpen ; i++){
        let hourlySale = Math.floor(Math.random() * (store.max - store.min) + store.min * store.saleAvg);
        store.hourlySales = [...store.hourlySales, hourlySale];
			}
			let dailyTotal = store.hourlySales.reduce((a,b) => a+b,0);
			store.hourlySales = [...store.hourlySales, dailyTotal];
    })
                
	}
	

	let min, max, name, saleAvg;

	function handleSubmit (){
       
		stores = [...stores, {name, min, max, saleAvg, hourlySales:[]}]
	}

    

</script>


<section id=table>
	<h1>This is our starting point. We have the following 5 stores with the known sales info in the table.</h1>
	<table>
			<thead>
				<tr>
					<th>Location</th>
					<th>Min / Cust</th>
					<th>Max / Cust</th>
					<th>Avg Cookie / Sale</th>
				</tr>
			</thead>
			<tbody>
				{#each stores as store}
					<tr>
						<td>{store.name}</td>
						<td>{store.min}</td>
						<td>{store.max}</td>
						<td>{store.saleAvg}</td>
					</tr>
				{/each}

			</tbody>
		</table>
</section>    
<section id="sales">
	<br>
	<button id="report2But" on:click={toggleReport}> Click to see the sales report</button>

	<button id="formBut" on:click={toggleAddStore}>Click here to add new stores</button>
	<br>
	<form id="addStoreForm" style="display: {addNewStore};">
			<p style="font-size: 30px;">Please fill out the following form for new store info</p>
			<label>
					Store Location:
					<input type="text" name="location" bind:value={name} />
					<br>
			</label>
			<label>
					The minimum number of customers per hour: 
					<input type="text" name="minCust" bind:value={min} /><br>
			</label>
			<label>
					The maximum number of customers per hour:
					<input type="text" name="maxCust" bind:value = {max}/><br>
			</label>
			<label>
					The average number of cookies purchased per customer:
					<input type="text" name="avgSale" bind:value={saleAvg}/><br>
			</label>
			<button type="submit" id="addStoreBut" on:click|preventDefault = {handleSubmit}>Click to submit</button>

	</form>
	<br>
	<br>
	<table id="report2" style="display: {showReport};">
			<thead id = "report2Head">
					<tr>
							<th>Location</th>
							<th>6:00am:</th>
							<th>7:00am:</th>
							<th>8:00am:</th>
							<th>9:00am:</th>
							<th>10:00am:</th>
							<th>11:00am:</th>
							<th>12:00am:</th>
							<th>1:00pm:</th>
							<th>2:00pm:</th>
							<th>3:00pm:</th>
							<th>4:00pm:</th>
							<th>5:00pm:</th>
							<th>6:00pm:</th>
							<th>7:00pm:</th>
							<th>Daily Total</th>
					</tr>
			</thead>
			<tbody id=report2Body>
				{#if showReport !== 'none'}
					{#each stores as store}
            <tr>
						<td>{store.name}</td>
						{#each store.hourlySales as hour}
							<td>{hour}</td>
						{/each}
                        
						</tr>
					{/each}
				{/if}
			</tbody>
  </table>    
</section>


<style>

body {
    align-content: center;
    width: 90%;
}

ul {
    font-size: 20px;
    font-family: 'Courier New', Courier, monospace;
    color:indigo;
}
button {
    font-size: 20px;
}
#sales {
    font-size: 20px;
    line-height: 1.7em;
}

#table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
    font-size: 20px;
    
  }
 #report2 {
    overflow-x: scroll;
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
    font-size: 20px;

 } 
td, th {
    border: 3px solid gray;
    text-align: left;
    padding: 8px;
  }
  
tr:nth-child(even) {
    background-color:lightgray;
  }
thead{
    background-color:lightgray;

}
  #report {
    font-size: 15px;
}
</style>