<svelte:head>
	<title>Ruuat</title>
	<meta name="description" content="Ruuat" />
</svelte:head>

<script>
	import { onMount } from "svelte";
	import { writable } from 'svelte/store';
	let foods = writable([]);

	const fetchFoods = async () => {
		try {
			const response = await fetch('http://localhost:5126/api/Foods');
			if (!response.ok) {
				throw new Error('Failed to fetch foods from the API');
			}
			const data = await response.json();
			foods.set(data);
		} catch (error) {
			console.error(error);
		}
	}

	const handleDelete = async (id) => {
        try {
            const response = await fetch(`http://localhost:5126/api/Foods/${id}`, {
                method: 'DELETE'
            });
            if (!response.ok) {
                throw new Error('Failed to delete food item');
            }
            // Remove the deleted item from the array
            foods.update(items => items.filter(item => item.id !== id));
        } catch (error) {
            console.error(error);
        }
    };

	onMount(fetchFoods);
</script>

<section>
	<h1>
		Ruuat
	</h1>
	
		<div class="titles-container">
			<p class="title">Ruoka</p>
			<p class="title">Ravinteet per 100g</p>
		</div>
		
		<!-- Table displaying food contents -->
		<table>
			<thead>
				<tr>
					<th></th> <!-- Jätetään checkbox ja nimi th tyhjäksi -->
					<th></th> <!-- Jätetään checkbox ja nimi th tyhjäksi -->
					<th style="padding-left: 10px;">Kcal</th>
					<th>Hiil</th>
					<th>Prot</th>
					<th>Rasva</th>
					<th>Kuitu</th>
				</tr>
			</thead>
			<tbody>
				{#each $foods as food}
					<tr>
						<td style="padding-right: 10px; text-align: center;"><input type="checkbox" /></td> <!-- Checkbox -->
						<td>{food.name}</td> 
						<td style="padding-left: 10px;">{food.calories}</td> 
						<td>{food.carbohydrates}</td> 
						<td>{food.protein}</td> 
						<td>{food.fat}</td> 
						<td>{food.fiber}</td>
						<td>
							<button class="delete-button" on:click={() => handleDelete(food.id)}>
								<svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
									<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" />
									<line x1="6" y1="12" x2="18" y2="12" stroke="currentColor" stroke-width="2" />
								</svg>
							</button>
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
	

	<button class="calc-button">
		<span>Lisää ruoka</span>
		<span class="plus">+</span>
	</button>
</section>
	
<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
		
	}
	

	h1 {
		width: 100%;
	}
	.titles-container {
        display: flex;
        justify-content: center;
        width: 100%;
    }

    .title {
        text-align: center;
		
    }
	.titles-container p {
		margin: 0 55px;
	}

	p {
		margin: 0 10px;
	}
	.calc-button {
		display: flex;
		justify-content: space-between;
		align-items: center;
        padding: 10px 20px;
		cursor: pointer;
        
		width: 300px;  
         
    }
	.plus {
        margin-left: auto;
    }

	.delete-button {
        background-color: transparent;
        border: none;
        cursor: pointer;
        padding: 0;
    }

    .delete-button svg {
        width: 24px;
        height: 24px;
        fill: none;
        stroke: #000;
        stroke-linecap: round;
        stroke-linejoin: round;
        stroke-width: 2;
    }
</style>

