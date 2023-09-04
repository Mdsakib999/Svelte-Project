<script>
    import Nav from "../../components/nav.svelte";
    import Chart from "../../components/chart.svelte";

    import { onMount } from 'svelte';
  
    let countries = [];
  
    onMount(async () => {
      try {
        const response = await fetch('https://restcountries.com/v3.1/all');
        if (response.ok) {
          countries = await response.json();
          countries = countries.slice(0, 12);
        //   console.log(countries);
        } else {
          console.error('Failed to fetch data');
        }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    });
</script>

<Nav></Nav>

<h1 class="mt-4 mb-6 text-center text-3xl font-bold">List of Countries</h1>

  
  <table>
    <thead>
      <tr>
        <th>Flag</th>
        <th>Name</th>
        <th>Population</th>
        <th>CIOC</th>
        <th>Region</th>
        <th>Area</th>
      </tr>
    </thead>
    <tbody>
      {#each countries as country (country.cca2)}
        <tr>
          <td><img src={country.flags.png} alt="Flag" width="30" /></td>
          <td>{country.name.common}</td>
          <td>{country.population}</td>
          <td>{country.cioc}</td>
          <td>{country.region}</td>
          <td>
            {country.area}
          </td>
         
        </tr>
      {/each}
    </tbody>
  </table>

  <Chart></Chart>
  

  <style>
    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
    }
  
    th, td {
      padding: 10px;
      text-align: center;
      border-bottom: 1px solid #ddd;
    }
  
    th {
      background-color: #f2f2f2;
    }
  
    img {
      display: block;
      margin: 0 auto;
    }
  </style>
