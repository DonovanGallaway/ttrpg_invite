<script>
    import {onMount} from 'svelte'
    import { fade } from 'svelte/transition';

    let password = '';
    const validPasswords = {
        'wildfire': 'Devlin',
        'lupine': 'Korey',
        'queerest': 'Avery',
        'powder': 'Stacy',
        'test': 'Player',
        'faechild': 'Rae',
        'piracy': 'Rue',
    }

    let accessGranted = false;
    let userName = '';
    let passwordChecked = false;
    let animateLogin = false;
    let animateInvite = false;

    function checkPassword() {
        if (validPasswords[password.toLowerCase()]) {
            userName = validPasswords[password.toLowerCase()];
            accessGranted = true;
            animateInvite = true;
        } else if (password === '') {
            passwordChecked = false;
        } else {
            passwordChecked = true;
        }
    }

    onMount(() => {
        animateLogin = true;
    });
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Caveat&family=Roboto:wght@100&family=Vujahday+Script&display=swap');
    
    :global(*){
        font-family: 'Caveat', cursive;
    }

	:global(input){
		font-family: 'Roboto', sans-serif;
        font-size: 1.5em;
	}

	:global(button){
		background-color: white;
		color: black;
		border-radius: 10px;
		border: solid 3px black;
	}

	button {
		font-size: 2em;
	}

    div {
        margin: 0 auto;
        width: 80%;
        text-align: center;
        margin-top: 50px;
    }

    img {
        display: block;
        margin-left: auto;
        margin-right: auto;
        max-width: 400px;
        padding-left: .15em;
    }
</style>

{#if accessGranted && animateInvite}
  <div>
    <div>
        <h2 in:fade={{duration:2000, delay:1000}}>Dearest {userName},</h2>
        <div>
        <p in:fade={{duration:2000, delay:3000}}>You are hereby cordially invited to attend the Hollowhaven School for Magicians.</p>
        <p in:fade={{duration: 2000, delay: 8000}}>We understand that you have many options for your choice of higher education, but circumstances have led us to believe that you may have a more...interesting life available to you than you may have otherwise dreamed.</p>
        <p in:fade={{duration: 2000, delay: 8000}}>Entrance examinations will be held in-person at my home on August 12th at 7pm. No prior education is required, though an understanding of Kids on Brooms will aid you if you so choose to read up on it. Please contact me for further details or copies of materials.</p>
        <p in:fade={{duration: 2000, delay: 8000}}>If you suspect a friend may also have an aptitude for the magical, please feel free to bring them.</p>
        <p in:fade={{duration: 2000, delay: 8000}}>Nothing is otherwise required. If you choose, you may bring a shareable snack to accommodate the mood.</p>

        <p in:fade={{duration: 2000, delay: 13000}}>Sincerely yours,</p>
        <p in:fade={{duration: 2000, delay: 13000}}>Donovan Gallaway</p>
        <p in:fade={{duration: 2000, delay: 13000}}>Admissions Officer and Game Master</p>
        <img src="/signature.png" alt="Donovan Gallaway's signature" in:fade={{duration: 2000, delay: 13000}}>

        </div>
      </div>
    </div>
{:else if animateLogin && !accessGranted}
  <div in:fade={{duration:2000, delay:1000}}>
    <h2>Enter your password</h2>
    <input type="text" bind:value={password} on:keypress={event => event.key === 'Enter' && checkPassword()}>    
    {#if password !== '' && !accessGranted && passwordChecked}
      <p>Invalid password, please try again.</p>
    {/if}
  </div>
  <div in:fade={{duration:2000, delay:1500}}>
    <button on:click={checkPassword}>Submit</button>
  </div>
{/if}
