<script>
    import Feed from './Feed.svelte';    
  
    export let points = 150; // Example initial points (Kudos balance)

    let activeTab = 'feed';
  
    const switchTab = (tab) => activeTab = tab;

    export function addPoints(newPoints) {
        points += newPoints;
        return points;
    }

    // Example shop items
    let shopItems = [
        { id: 1, name: "Teddy Bear", price: 100, image: "/bear.svg", bought: false },
        { id: 2, name: "Banner", price: 150, image: "/banner.svg", bought: false },
        { id: 3, name: "Plant", price: 50, image: "/plant.svg", bought: false }
    ];

    // Function to handle the "Buy" action
    function buyItem(item) {
        if (points >= item.price && item.bought == false) {
            item.bought = true; // Mark the item as bought
            
            points -= item.price; // Deduct the item price from points

            shopItems = [...shopItems];
        } else {
            alert(`You don't have enough Kudos to buy the ${item.name}.`);
        }
    }
</script>

<!-- Main Header at the top -->
<header>
    <h1 id="home" on:click={() => switchTab('feed')}>Complimansion</h1>
    <span style="position: fixed; right: 100px; top: 6%; transform: translateY(-50%); font-size: 14px;">
        Kudos: {points}
    </span>
    <img id="profile" src="/samplepfp.png" alt="Profile" on:click={() => switchTab('profile')} />
</header>

<!-- Conditionally render the content based on the active tab -->
<main>
    {#if activeTab === 'feed'}
        <Feed {addPoints} /> <!-- Pass addPoints to Feed component -->
    {:else if activeTab === 'profile'}
        <section>
            <h2>Profile</h2>
            <p>Welcome to your profile page!</p>

            <!-- Profile Room and Shop Items Side-by-Side -->
            <div class="profile-container">
                <!-- Profile Room Image -->
                <img src="/bedroom-01.svg" alt="bedroom" width="400" height="600">

                <!-- Shop Items Box -->
                <div class="shop-box">
                    <h3>Shop Items</h3>
                    <div class="shop-list">
                        {#each shopItems as item}
                            <div class="shop-item">
                                <img src={item.image} alt={item.name} width="100" height="100">
                                <h4>{item.name}</h4>
                                <p>Price: {item.price} Kudos</p>

                                {#if item.bought}
                                    <p style="color: green;">Purchased</p>
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

<!-- Styles -->
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
        color: black;
        text-align: center;
        padding: 1rem;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 10;
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
        gap: 2rem;
    }

    .shop-box {
        width: 300px;
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 1rem;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        text-align: center;
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
    }

    .shop-item button:hover {
        background-color: #0056b3;
    }

    h1 { 
        font-family: sans-serif;
    }

    #home {
        cursor: pointer; 
        height: 40px; 
        float: left;
    }

    #profile {
        cursor: pointer; 
        height: 40px; 
        float: right;
    }
</style>
