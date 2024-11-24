<script>
    import { PUBLIC_STRAPI_TOKEN, PUBLIC_STRAPI_URL } from "$env/static/public";
    const headers = { Authorization: `Bearer ${PUBLIC_STRAPI_TOKEN}` };

    const getBeers = async () => { 
        const res = await fetch(
            `${PUBLIC_STRAPI_URL}/api/beers?populate=prices,happyHourPrices,image,origin&sort=rank:asc&pagination[start]=0&pagination[limit]=12`,
        {
            headers,
        })
        const data = await res.json();
        return data;
    };
    export const prerender=true
</script>

<section class="section has-text-white" style="background: #000">
<div class="container">
    {#await getBeers()}
        
    {:then data} 
        {#each data.data as beer}
            <p>{beer.attributes.title}</p>
        {/each}
    {/await}
</div>
</section>

<style>
.section {
font-family: "Josefin Sans", sans-serif;
text-align: center;
}
</style>