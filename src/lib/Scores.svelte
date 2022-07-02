<script>
    import logo from "../assets/u17kwc.jpeg";
    export let matches = [];

    const fetchMatches = async () => {
        const response = await fetch(
            "https://jury.u17kwc.com/u17kwc/GamesComplete?Start=0&Stop=40"
        );
        const jsonData = await response.json();

        const date = new Date();
        console.log(date.getDay());
        if (date.getDay() === 6) {
            return jsonData.value.slice(0, 25).filter((m) => {
                console.log(m);
                let hour = m.StartTime.split(":")[0];
                let currentHour = date.getHours() - 1;
                console.log(hour, currentHour);
                return hour >= currentHour;
            });
        } else {
            return jsonData.value.slice(25);
        }
    };

    // gets away score only if sum of awayscore and homescore is greater than 0
    export let getAwayScore = (match) => {
        if (Number(match.GoalsAway) + Number(match.GoalsHome) > 0) {
            return match.GoalsAway;
        } else {
            return "-";
        }
    };

    // gets home score only if sum of awayscore and homescore is greater than 0
    export let getHomeScore = (match) => {
        if (Number(match.GoalsAway) + Number(match.GoalsHome) > 0) {
            return match.GoalsHome;
        } else {
            return "-";
        }
    };

    setInterval(() => {
        fetchMatches().then((m) => (matches = m));
    }, 3 * 1000);
</script>

<div class="score_content">
    <div class="dflex p-2 h-20">
        <img src={logo} class="logo" alt="Svelte Logo" />
        <div class="title">
            <h1>Korfball World Cup</h1>
            <p>U17</p>
        </div>
    </div>
    <div class="matches">
        {#each matches as match}
            <div class="match_wrapper">
                <div class="dflex">
                    <h2 class="col-33">{match.TeamHome}</h2>
                    <span class="col-33">
                        {match.StartTime.substr(0, match.StartTime.length - 3)}
                    </span>
                    <h2 class="col-33">{match.TeamAway}</h2>
                </div>
                <div class="dflex ">
                    <div class="score col-33">{getHomeScore(match)}</div>
                    <div class="date col-33">
                        <!-- {match.StartTime.substr(0, match.StartTime.length - 3)} -->
                    </div>
                    <div class="score col-33">{getAwayScore(match)}</div>
                </div>
            </div>
        {/each}
    </div>
</div>

<style>
    .score_content {
        color: black;
        padding: 0px 40px;
        height: 100%;
        overflow: none;
        box-sizing: border-box;

        /* From https://css.glass */
        /* background: rgba(36, 142, 0, 0.66);
        border-radius: 16px;
        box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(13.1px);
        -webkit-backdrop-filter: blur(13.1px);
        border: 1px solid rgba(36, 142, 0, 1); */
    }
    .h-20 {
        height: 20%;
    }

    .matches {
        height: 80%;
        overflow: auto;
        box-sizing: border-box;
    }

    .p-2 {
        padding: 2rem;
        height: 130px;
    }

    .logo {
        width: 30%;
        padding-left: auto;
    }

    .title {
        width: 70%;
    }

    .dflex {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .col-33 {
        width: 33%;
    }

    .match_wrapper {
        /* From https://css.glass */
        background: rgba(255, 255, 255, 0.83);
        border-radius: 16px;
        box-shadow: 0 2px 7px rgba(0, 0, 0, 0.2);
        backdrop-filter: blur(12.6px);
        -webkit-backdrop-filter: blur(12.6px);
        border: 1px solid rgb(238, 238, 238);

        padding: 0px 0px 20px 0px;
        margin-bottom: 10px;
    }

    .score {
    }

    .date {
    }
</style>
