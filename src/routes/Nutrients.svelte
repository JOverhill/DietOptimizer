<ul>
    <li>
        Kalorit <input type="checkbox"> <input type="number" min="0" max="9999">
    </li>
    <li>
        Hiilihydraatit <input type="checkbox"> <input type="number" min="0" max="9999">
    </li>
    <li>
        Proteiini <input type="checkbox"> <input type="number" min="0" max="9999">
    </li>
    <li>
        Rasvat <input type="checkbox"> <input type="number" min="0" max="9999">
    </li>
    <li>
        Kuitu <input type="checkbox"> <input type="number" min="0" max="9999">
    </li>
</ul>
<div class="calc-button">
    <button>Laske</button>
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