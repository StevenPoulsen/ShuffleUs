<script>
    export let active = true;
    export let name = "";
    const toggle = () => {
        active = !active;
    }
</script>

<div class="player {active?'active':''}" on:click={toggle}>
    {name}
</div>

<style>
    .player {
        line-height: 2em;
        font-weight: bold;
        position: relative;
        padding: 0 0 0 2.5em;
    }
    .player:before {
        display: block;
        content: "";
        position: absolute;
        top:0.25em;
        left:0.25em;
        height: 1.5em;
        width: 1.5em;
        background: #333;
    }
    .player.active:after {
        display: block;
        content: "";
        position: absolute;
        top: 0.5em;
        left: 0.5em;
        height: 1em;
        width: 1em;
        background: #9c9;
    }
</style>