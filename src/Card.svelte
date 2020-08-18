<script>
    import { createEventDispatcher } from "svelte";
    export let name;
    export let jobTitle;
    export let postTime;
    export let jobStatus;
    export let location;
    export let keyWords;
    export let isNew;
    export let featured;
    export let logoUrl;

    const dispatch = createEventDispatcher();
    function sendKeyword(keyword) {
        console.log("clicked", keyword);
        dispatch("message", {
            text: keyword,
        });
    }
</script>

<style>
    .mb-small {
        margin-bottom: 8px;
    }
    .card-container {
        margin-bottom: 37px;
        width: 327px;
        padding: 36px 19px 0 19px;
        display: flex;
        flex-direction: column;
        background: #ffffff;
        box-shadow: 0px 15px 20px -5px rgba(13, 113, 130, 0.15);
        border-radius: 5px;
        border-left: 5px solid #5ca5a5;
    }
    .logo {
        width: 48px;
        position: relative;
    }
    .logo-img {
        position: absolute;
        top: -58px;
    }
    .company {
        display: flex;
    }
    .company--title {
        display: flex;
        margin-right: 1rem;
    }
    .company--title p {
        align-self: center;
        color: #5ca5a5;
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 13px;
        line-height: 16px;
    }
    .company--stat {
        display: flex;
    }
    .company--stat__new {
        background: #5ca5a5;
        border-radius: 12px;
        display: flex;
        padding: 3px 10px;
        margin-right: 1rem;
    }
    .company--stat__new p {
        align-self: center;
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 11px;
        line-height: 14px;

        text-align: center;
        letter-spacing: -0.0846154px;
        text-transform: uppercase;

        color: #ffffff;
    }
    .company--stat__featured {
        padding: 3px 10px;
        background: #2b3939;
        border-radius: 12px;
        display: flex;
    }
    .company--stat__featured p {
        align-self: center;
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 11px;
        line-height: 14px;
        letter-spacing: -0.0846154px;
        text-transform: uppercase;
        color: #ffffff;
    }
    .job-title p {
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 15px;
        line-height: 24px;
        color: #2b3939;
    }
    .job-stat p {
        font-family: "Spartan";
        font-style: normal;
        font-weight: 500;
        font-size: 13px;
        line-height: 24px;
        letter-spacing: -0.1px;
        color: #7c8f8f;
    }

    .hr {
        width: 100%;
        margin: 9px 0 15px 0;
    }
    .tags {
        display: flex;
        flex-wrap: wrap;
        margin-bottom: 9px;
    }
    .keyword-container {
        display: flex;
        background: hsl(180, 30.8%, 94.9%);
        mix-blend-mode: normal;
        border-radius: 4px;
        margin-right: 16px;
        margin-bottom: 16px;
        height: 32px;
        border: none;
    }
    .keyword-container p {
        align-self: center;
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 13px;
        letter-spacing: -0.1px;
        color: #5ca5a5;
    }
    .keyword {
        padding: 0 10px;
        align-self: center;
        font-family: "Spartan";
        font-style: normal;
        font-weight: bold;
        font-size: 13px;
        line-height: 24px;
        letter-spacing: -0.1px;
        color: #5ca5a5;
    }
    @media (min-width: 1200px) {
        .logo {
            position: static;
            width: 88px;
            margin-left: 40px;
            margin-right: 24px;
        }
        .logo-img {
            position: static;
        }
        .card-container {
            height: 152px;
            width: 1110px;
            margin: 0 auto;
            margin-bottom: 24px;
            flex-direction: row;
        }
        .d-xxl-none {
            display: none;
        }
        .flex-expand {
            flex: 1 0;
        }
        .tags {
            align-content: center;
        }
    }
</style>

<div class="card-container">
    <div class="logo">
        <img class="logo-img" src={logoUrl} alt="" />
    </div>
    <div class="mid-group flex-expand">
        <div class="company mb-small">
            <div class="company--title">
                <p class="company--title__text">{name}</p>
            </div>
            <div class="company--stat">
                {#if isNew}
                    <div class="company--stat__new">
                        <p>NEW!</p>
                    </div>
                    <div class="company--stat__featured">
                        <p>FEATURED</p>
                    </div>
                {/if}
            </div>
        </div>
        <div class="job-title mb-small">
            <p>{jobTitle}</p>
        </div>
        <div class="job-stat mb-small">
            <p>{postTime} &bull; {jobStatus} &bull; {location}</p>
        </div>
    </div>
    <hr class="hr d-xxl-none" />
    <div class="tags ">
        {#each keyWords as keyword}
            <button
                class="keyword-container"
                on:click={sendKeyword({ keyword })}>
                <p>{keyword}</p>
            </button>
        {/each}
    </div>
</div>

