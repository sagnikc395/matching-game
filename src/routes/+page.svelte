<script lang="ts">
    import {emoji} from './emoji'

    type State = 'start' | 'playing' | 'paused' | 'won' | 'lost'

    //game state
    let state: State = 'start';
    //size of the grid 
    let size = 20;


    
    const createGrid = () => {
        //unique cards 
        let cards = new Set<string>();
        //hald because we duplicate the cards 
        let maxSize = size / 2 ;

        while (cards.size < maxSize) {
            //pick random emoji 
            const randomIdx = Math.floor(Math.random() * emoji.length);
            cards.add(emoji[randomIdx]);
        }

        //duplicate and shuffle the cards 
        return shuffle([...cards,...cards]);
    }

    const shuffle = (array: Items[]) => {
        return array.sort(() => Math.random() - 0.5);
    }

    //game grid 
    let grid = createGrid();
    //used to check if game is over 
    let maxMatches = grid.length / 2 ;

    //selected cards 
    let selected: number[] = [];
    //matched cards 
    let matches: string[] = [];

</script>

{#if state === "start"}
    <h1>Matching Game</h1>
    <button on:click={() => state = 'playing'}>
        Play
    </button>
{/if}

{#if state === 'playing'}
    <div class="cards">
        {#each grid as card,cardIdx}
            <button class="card">
                <div>{card}</div>
            </button>
        {/each}
    </div>
{/if}

{#if state  === "lost"}
    <h1>You have lost !</h1>
    <button on:click={() => state = 'playing'}>Play again</button>
{/if}

{#if state === "won"}
    <h1>You have won!</h1>
    <button on:click={() => state = 'playing'}>
        Play again
    </button>
{/if}

<style>
    .cards {
        display: grid;
        grid-template: repeat(5,1fr);
        gap:0.4rem;
    }

    .card {
        height: 140px;
		width: 140px;
		font-size: 4rem;
		background-color: var(--bg-2);

		&.selected {
			border: 4px solid var(--border);
		}
    }
</style>