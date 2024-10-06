<script>
  import Feed from './Feed.svelte';
  import Button from "./lib/components/Button.svelte";
  
  let points = 0; // Initial points

  let activeTab = 'feed';
  const switchTab = (tab) => activeTab = tab;

  function addPoints(newPoints) {
        points += newPoints;
    }
</script>

<!-- Header at the top -->
<header>

    <h1>
        <img 
        src="/home.png" 
        alt="Feed" 
        on:click={() => switchTab('feed')}
        style="cursor: pointer; height: 40px; float:left;" />
        ❤️Complimansion❤️
        <img 
        src="/samplepfp.png" 
        alt="Profile" 
        on:click={() => switchTab('profile')}
        style="cursor: pointer; height: 40px; float:right;" /></h1>


    
  
  
</header>




<!-- Conditionally render the content based on the active tab -->
<main>
  {#if activeTab === 'feed'}
      <Feed/>
  {:else if activeTab === 'profile'}
      <section>
          <h2>Profile</h2>
          <p>Welcome to your profile page!</p>
          <button>class:active={activeTab}</button>
          <img src="/bedroom-01.svg" alt="bedroom" width="400" height="600">

      </section>
  {/if}
</main>

<!-- Styles -->
<style>
  /* Basic reset and layout styling */
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

  /* Header styling */
  header {
    position: fixed;
        top:0;
        left: 0;
        width: 100%;
        background-color: steelblue;
        color: white;
        text-align: center; /* Align text in the center */
        padding: 1rem;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 10; /* Ensure it's on top of other content */
  }

  header img {
        margin-right: 10px;
        height: 40px;
        cursor: pointer; /* Makes the cursor a pointer when hovering over the image */
    }

  /* Push content below header */
  main {
      margin-top: 100px; /* Adjust based on header height */
      padding: 1rem;
  }

  /* Navigation bar styling */
  nav {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 1rem;
  }

  /* Button styling */
  button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      border: none;
      cursor: pointer;
      background-color: lightgray;
      border-radius: 4px;
      transition: background-color 0.3s ease;
  }

  button.active {
      background-color: steelblue;
      color: white;
  }

  button:hover {
      background-color: darkgray;
  }

  /* Basic section styling */
  section {
      text-align: center;
      padding: 1rem;
      border: 1px solid #ccc;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  h1{font-family: Courier New, monospace;}
</style>
