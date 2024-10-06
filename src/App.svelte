<script async>
    import Feed from './Feed.svelte';    
  
    export let points = 150; // Example initial points (Kudos balance)

    let activeTab = 'feed';
  
    const switchTab = (tab) => activeTab = tab;

    export function addPoints(newPoints) {
        points += newPoints;
        return points;
    }

    let shopItems = [
        { id: 1, name: "Teddy Bear", price: 100, image: "/bear.svg", bought: false},
        { id: 2, name: "Banner", price: 150, image: "/banner.svg", bought: false},
        { id: 3, name: "Plant", price: 50, image: "/plant.svg", bought: false}
    ];

    // Function to handle the "Buy" action
    function buyItem(item) {
        if (points >= item.price && item.bought == false) {

            document.addEventListener('click', placeItem);
            item.bought = true; // Mark the item as bought
            
            points -= item.price; // Deduct the item price from points

            shopItems = [...shopItems];
        } else {
            alert(`You don't have enough Kudos to buy the ${item.name}.`);
        }
    }

    function placeItem(event){
        var i = document.getElementById("1");
        addEventListener('click', function(event){
            i.style.visibility="visible";
            i.style.left = event.clientX + 'px';
            i.style.top = event.clientY + 'px';
        })
    }



</script>


<header>
    <h1 id="home" on:click={() => switchTab('feed')}>compliment</h1>
    <img id="profile" src="/profile.gif" alt="Profile" on:click={() => switchTab('profile')} />
    <span id ="kudos">
        Kudos: {points}
    </span>
</header>

<main>
    {#if activeTab === 'feed'}
        <Feed {addPoints} /> 
    {:else if activeTab === 'profile'}
        <section id = "pf">
            <div id="profile-head">
                <h2 id="title">Profile</h2>
                <p id="goon">Decorate your Room!</p>
            </div>
            <div class="profile-container">

                <div id="bedroom">
                    <img src="/bedroom-01.svg" alt="bedroom" width="400" height="600">
                </div>
                <div class="shop-box">
                    <h3>Shop Items</h3>
                    <div class="shop-list">
                        {#each shopItems as item}
                            <div class="shop-item">
                                <img src={item.image} alt={item.name}>
                                <h4>{item.name}</h4>
                                <p>Price: {item.price} Kudos</p>

                                {#if item.bought}
                                    <p style="color: green;">Purchased</p>
                                    {#if item.id == 1}
                                    <img src="/bear.svg" alt="bear" id="bear">
                                    {/if}
                                    {#if item.id == 2}
                                    <img src="/banner.svg" alt="banner" id='banner'>
                                    {/if}
                                    {#if item.id == 3}
                                    <img src="/plant.svg" alt="plant" id="plant">
                                    {/if}
                                {:else}
                                    <button on:click={() => buyItem(item)}>Buy</button>
                                    
                                {/if}
                            </div>
                        {/each}
                    </div>
                </div>
            </div>
        </section>
    {/if}
</main>


<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    header {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        background-color: white;
        color:black;
        text-align: center;
        padding: 1rem;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 10;
        font-family: sans-serif;
        text-shadow: 3px 3px 2px rgba(128, 57, 57, 1);
        
    }

    header img {
        margin-right: 10px;
        height: 40px;
        cursor: pointer;
    }

    main {
        margin-top: 100px;
        padding: 1rem;
    }

    section {
        text-align: center;
        padding: 1rem;
        border: 1px solid #ccc;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .profile-container {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        gap: 4rem;
    }

    .shop-box {
        width: 300px;
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 1rem;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        text-align: center;
        margin-top: 2rem;
    }

    .shop-box h3 {
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }

    .shop-list {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
    }

    .shop-item {
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 1rem;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        text-align: center;
    }

    .shop-item img {
        margin-bottom: 1rem;
    }

   /* .shop-item img:hover {}*/

    .shop-item h4 {
        font-size: 1.2rem;
        margin-bottom: 0.5rem;
    }

    .shop-item p {
        font-size: 1rem;
        margin-bottom: 1rem;
    }

    .shop-item button {
        padding: 0.5rem 1rem;
        font-size: 1rem;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: background-color 0.3s;
        font-family: sans-serif;
        transform: scale(1.3);
    }

    .shop-item button:hover {
        background-color: #0056b3;
    }

    h1 { 
        font-family: sans-serif;
    }

    #bedroom{
        max-width: fit-content;
        margin-left: auto;
        margin-right: auto;
        padding-left: 3em;
    }

    #home {
        cursor: pointer; 
        height: 40px; 
        float: left;
    }
    #home:hover{
        transform: scale(1.05);
    }

    #profile {
        cursor: pointer; 
        height: 40px; 
        float: right;
        border-radius: 20px;
        transform: scale(1.5);
    }
    #profile:hover{
        transform: scale(1.7);
    }

    #kudos{
        text-shadow:none;
        float:right;
        font-size: 25px;
        padding-right: 1.2rem;
    }
    #kudos:hover{

        transform: scale(1.1);
    }

    #bear{
        position: absolute; 
        top: 600px; 
        left: 600px; 
        width: 100px; 
        height: 100px
    }

    #banner{
        position: absolute; 
        top: 350px; 
        left: 400px; 
        width: 100px; 
        height: 100px; 
        transform: scale(2.0);
    }

    #plant{
        position: absolute;
        top: 600px;
        left: 400px; 
        width: 100px; 
        height: 100px; 
    }

    #pf{
        background-color: rgba(0, 0, 0, 0.755);
    }

    #title{
        text-shadow: 3px 3px 2px rgba(128, 57, 57, 1);
        font-size:30px;
        float: left;
    }

    #goon{
        padding-right: 1em;
        float: right;
    }

    #profile-head{
        padding: 1.2em;
    }
</style>
