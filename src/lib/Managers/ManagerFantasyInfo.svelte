<script>
    import { goto } from "$app/navigation";


    export let viewManager, players;

    const gotoRival = (rival) => {
        if(!rival) {
            goto(`/managers`);
        }
        goto(`/managers?manager=${rival}`);
    }
</script>

<style>
    .fantasyInfos {
        display: flex;
        justify-content: space-around;
        align-items: flex-start;
        flex-wrap: wrap;
        padding: 0 0 2em;
        margin: 3em 0 4em;
        border-bottom: 1px solid #aaa;
        border-top: 1px solid #aaa;
        box-shadow: 0 0 8px 4px #ccc;
    }

    .infoSlot {
        text-align: center;
        margin: 2em 1em 0;
    }

    .infoIcon {
        display: inline-flex;
        height: 70px;
        width: 70px;
        justify-content: center;
        align-items: center;
        border-radius: 100%;
        border: 1px solid #ccc;
        overflow: hidden;
        background-color: #fff;
		transition: box-shadow 0.4s;
    }

    .playerIcon {
        align-items:flex-end;
    }

    .infoLabel {
        font-size: 0.7em;
        color: #00316b;
        font-weight: 700;
        margin-bottom: 1em;
        height: 30px;
        width: 90px;
        text-align: center;
        line-height: 1.2em;
    }

    .infoAnswer {
        font-size: 0.8em;
        color: #777;
        margin-top: 1em;
        width: 90px;
        text-align: center;
        line-height: 1.2em;
    }

    .tradingScale {
        line-height: 70px;
        font-size: 55px;
        color: #00316b;
    }

    .rookiesOrVets {
        height: 65px;
        opacity: 0.5;
        vertical-align: middle;
    }

    .infoRival {
        cursor: pointer;
    }

    .infoRival:hover .infoIcon {
        box-shadow: 0 0 6px 4px #aaa;
        border: 1px solid #aaa;
    }

    .rival {
        height: 100%;
    }

    .rebuildOrWin {
        height: 70px;
    }

    .valuePosition {
        line-height: 70px;
        font-size: 25px;
        color: #fff;
    }

    .QB {
        background-color: #ff2a6d;
    }

    .WR {
        background-color: #58a7ff;
    }

    .RB {
        background-color: #00ceb8;
    }

    .TE {
        background-color: #ffae58;
    }

    .Picks {
        background: #73b647;
    }
    .K {
        background-color: #bd66ff;
    }

    .DEF {
        background-color: #fff67a;
    }

    .favoritePlayer {
        height: 65px;
        vertical-align: bottom;
    }

    /* media queries */

    @media (max-width: 731px) {
        .infoSlot {
            margin: 2em 3em 0;
        }
    }

    @media (max-width: 558px) {
        .infoSlot {
            margin: 2em 2em 0;
        }
    }

    @media (max-width: 461px) {
        .infoSlot {
            margin: 2em 1em 0;
        }
    }
</style>

<div class="fantasyInfos">
    <!-- Rookies or Vets (optional) -->
    {#if viewManager.rookieOrVets}
        <div class="infoSlot">
            <div class="infoLabel">
                Rookie or Vet Preference
            </div>
            <div class="infoIcon">
                <img class="rookiesOrVets" src="/{viewManager.rookieOrVets}.png" alt="rookie or vet preference"/>
            </div>
            <div class="infoAnswer">
                {viewManager.rookieOrVets}
            </div>
        </div>
    {/if}
    <!-- Favorite fantasy position (optional) -->
    {#if viewManager.valuePosition}
        <div class="infoSlot">
            <div class="infoLabel">
                Favorite Fantasy Asset
            </div>
            <div class="infoIcon {viewManager.valuePosition}">
                <span class="valuePosition">{viewManager.valuePosition}</span>
            </div>
        </div>
    {/if}
    <!-- Trading Scale -->
    <div class="infoSlot">
        <div class="infoLabel">
            Desire to Trade
        </div>
        <div class="infoIcon">
            <span class="tradingScale">{viewManager.tradingScale}</span>
        </div>
        <div class="infoAnswer">
            {viewManager.tradingScale} out of 10
        </div>
    </div>
    <!-- Favorite player (optioonal) -->
    {#if viewManager.favoritePlayer}
        <div class="infoSlot">
            <div class="infoLabel">
                Favorite Player
            </div>
            <div class="infoIcon playerIcon">
                <img class="favoritePlayer" src="https://sleepercdn.com/content/nfl/players/{viewManager.favoritePlayer}.jpg" alt="favorite player"/>
            </div>
            <div class="infoAnswer">
                {players[viewManager.favoritePlayer].first_name} {players[viewManager.favoritePlayer].last_name}
            </div>
        </div>
    {/if}
    <!-- Rebuild Mod (optional) -->
    {#if viewManager.mode}
        <div class="infoSlot">
            <div class="infoLabel">
                Win Now or Rebuild?
            </div>
            <div class="infoIcon">
                <img class="rebuildOrWin" src="/{viewManager.mode.replace(' ', '%20')}.png" alt="win now or rebuild"/>
            </div>
            <div class="infoAnswer">
                {viewManager.mode}
            </div>
        </div>
    {/if}
    <!-- Rival -->
    <div class="infoSlot infoRival" on:click={() => gotoRival(viewManager.rival.link)}>
        <div class="infoLabel">
            Rival
        </div>
        <div class="infoIcon">
            <img class="rival" src="{viewManager.rival.image}" alt="rival"/>
        </div>
        <div class="infoAnswer">
            {viewManager.rival.name}
        </div>
    </div>
</div>