<script lang="ts">
    import {emoji} from './emoji'

    type State = 'start' | 'playing' | 'paused' | 'won' | 'lost'

    let state: State = 'start';
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

    let grid = createGrid();

</script>