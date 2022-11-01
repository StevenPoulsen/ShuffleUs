<script>
    import PlayerListPlayer from './PlayerListPlayer.svelte';
    

    export const getPlayers = () => {
        console.log(players, players.filter((player) => player.active));
        return players.filter((player) => player.active);
    }
    const addPlayer = (name) => {
        players.push({active:true, name:name});
        savePlayers();
        players = players;
    }
    const addClick = () => {
        let name = prompt("Player Name");
        if (!!name.replaceAll(" ", "")) {
            addPlayer(name);
        }
    }
    const savePlayers = () => {
        localStorage.setItem("players", JSON.stringify(players));
    }
    const loadPlayers = () => {
        let cache = localStorage.getItem("players");
        if (!cache) {
            return [];
        }
        let cachedPlayers = JSON.parse(cache);
        for (let i = 0, len = cachedPlayers.length; i < len; i++) {
            cachedPlayers[i].component = PlayerListPlayer;
        }
        return cachedPlayers;
    }
    let players = loadPlayers();
    let shown = false;
</script>

<div class="playerList {shown?'shown':''}">
    {#each players as player}
        <PlayerListPlayer name={player.name} bind:active={player.active} />
    {/each}
    <button class="add" on:click={addClick}>Add</button>
</div>
<button class="activator" on:click={()=>shown=!shown}>Players</button>

<style>
    .playerList {
        position: absolute;
        background: rgb(179, 176, 158);
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        opacity: 0;
        pointer-events: none;
        transition: opacity 500ms ease-in;
    }
    .playerList.shown {
        opacity: 1;
        pointer-events: auto;
        transform: opacity 500ms easy-out;
    }
    .activator {
        position: absolute;
        bottom: 0;
        right: 0;
        padding: 1em;
    }
    .add {
        line-height: 2em;
        font-weight: bold;
        position: relative;
        padding: 0 0 0 2.5em;
    }
    .add:before {
        position: absolute;
        content: "+";
        width: 1.5em;
        height: 1.5em;
        top: 0.25em;
        left: 0.25em;
        background: #fff;
        border-radius: 100%;
        border: 1px solid #333;
        line-height: 1.5em;
    }
</style>