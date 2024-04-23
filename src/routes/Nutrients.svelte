<script>
    import { onMount } from 'svelte';

    let formData = {
        calories: 0,
        protein: 0,
        carbohydrates: 0,
        fat: 0,
        fiber: 0
    };

     // Function to handle checkbox change event
     function handleCheckboxChange(event) {
        const { name, checked } = event.target;
        formData[name] = checked ? 1 : 0;
    }

    // Function to handle number input change event
    function handleInputChange(event) {
        const { name, value } = event.target;
        formData[name] = parseFloat(value) || 0; // Convert input value to a number, default to 0 if NaN
    }

    // Function to handle form submission
    async function handleSubmit() {
        try {
            const response = await fetch('http://localhost:5126/api/Calculate', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(formData)
            });
            if (response.ok) {
                // Handle successful response
                console.log('Calculation successful');
            } else {
                // Handle error response
                console.error('Calculation failed:', response.statusText);
            }
        } catch (error) {
            // Handle network error
            console.error('Network error:', error);
        }
    }


</script>

<ul>
    <li>
        Kalorit <input type="checkbox" name="calories" on:change={handleCheckboxChange}> <input type="number" name="calories" min="0" max="9999" on:input={handleInputChange}>
    </li>
    <li>
        Hiilihydraatit <input type="checkbox" name="carbohydrates" on:change={handleCheckboxChange}> <input type="number" name="carbohydrates" min="0" max="9999" on:input={handleInputChange}>
    </li>
    <li>
        Proteiini <input type="checkbox" name="protein" on:change={handleCheckboxChange}> <input type="number" name="protein" min="0" max="9999" on:input={handleInputChange}>
    </li>
    <li>
        Rasvat <input type="checkbox" name="fat" on:change={handleCheckboxChange}> <input type="number" name="fat" min="0" max="9999" on:input={handleInputChange}>
    </li>
    <li>
        Kuitu <input type="checkbox" name="fiber" on:change={handleCheckboxChange}> <input type="number" name="fiber" min="0" max="9999" on:input={handleInputChange}>
    </li>
</ul>
<div class="calc-button">
    <button on:click={handleSubmit}>Laske</button>
</div>

<style>
    ul {
		padding: 0;
		margin: 0;
		list-style: none;
	}
    li {
		position: relative;
		height: 100%;
        font-size: 24px;
        padding-right: 300px;
	}
    input[type="checkbox"] {
        position:absolute;
        top: 20%;
        right: 150px; /* Checkbox distance from the right side of <li> */
        transform: translateY(-20%);
        width: 24px;
        height: 24px;
    }
    input[type="number"] {
      position: absolute;
      top: 20%;
      right: 0px;
      transform: translateY(-20%);
      width: 64px;
      height: 24px;  
    }
    input[type=number]::-webkit-inner-spin-button {
        -webkit-appearance: none; /* To Hide the up/arrow buttons from the number input box */
    }
    .calc-button {
        margin-top: 40px;
        text-align: center;  
         
    }
    
    button {
        width: 120px; 
        height: 40px; 
        font-size: 18px; 
    }
</style>