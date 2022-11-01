<script>
  import { group_outros } from 'svelte/internal';
import PlayerList from './lib/PlayerList.svelte';

  let groupCount = 4;
  let groups = [];
  let playerList;

  let shulffleUs = () => {
    groups = [];
    let players = [...playerList.getPlayers()];
    console.log(players);
    for (let i = 0; i < groupCount; i++) {
      groups.push({id:i,players:[]});
    }
    while (players.length > 0) {
      for (let i = 0; i < groupCount; i++) {
        if (players.length) {
          let player = players.splice(Math.random() * players.length, 1)[0];
          groups[i].players.push(player);
        }
      }
    }
    groups = groups; // trigger update
  }


</script>

<main>
  
  <h1>Shuffle Us</h1>

  <PlayerList bind:this={playerList} />

  <section>
    <label>Groups: <input type="number" bind:value={groupCount}/></label>
    <div><button on:click={shulffleUs}>Shuffle Us!</button></div>
  </section>

  <section>
    {#each groups as group, idx}
        <div>
          <h3>Group {idx+1}</h3>
          <ul>
            {#each group.players as player}
              <li>{player.name}</li>
            {/each}
          </ul>
        </div>
    {/each}
  </section>
</main>

<style>
</style>
