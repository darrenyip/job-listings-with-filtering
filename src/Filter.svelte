<script>
    export let words;
    import { createEventDispatcher } from "svelte";
    let crossUrl = "./images/times-solid.svg";
    const dispatch = createEventDispatcher();
    // $: newWord = words;
    function deleteWord() {
        dispatch("removeKeyword", event.currentTarget.childNodes[0].innerText);
    }
    function clear() {
        dispatch("clearKeyword", true);
    }
</script>

<style>
    .display {
        display: flex !important;
    }

    .filter-container {
        border-radius: 0.5rem;
        transform: translateY(-45px);
        display: none;
        width: 80vw;
        margin: 0 auto;
        padding: 1rem 1rem 0 1rem;
        background-color: white;
        margin-bottom: 1rem;
    }
    .tags {
        width: 80%;
        display: flex;
        flex-wrap: wrap;
    }
    .tag {
        margin-right: 1rem;
        margin-bottom: 1rem;
        background-color: hsl(180, 30.8%, 94.9%);
        border-radius: 5px;
        display: flex;
    }
    .tag-text {
        padding: 4px 8px;
        align-self: center;
        font-style: normal;
        font-weight: bold;
        font-size: 13px;
        letter-spacing: -0.1px;
        color: #5ca5a5;
    }

    .tag-cross {
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
        color: white;
        background-color: #5ca5a5;
        height: 32px;
        width: 32px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .clear {
        width: auto;
        align-self: center;
        padding-bottom: 1rem;
    }
    .clear span {
        font-style: normal;
        font-weight: bold;
        font-size: 13px;
        letter-spacing: -0.1px;
        color: #7c8f8f;
    }
    @media (min-width: 1200px) {
        .filter-container {
            width: 1110px;
            padding: 20px 40px;
        }
        .tag {
            margin-bottom: 0;
        }
        .tag-cross {
            height: 40px;
            width: 40px;
        }
        .tag-text {
            font-style: normal;
            font-weight: bold;
            font-size: 13px;
            line-height: 24px;
            color: #5ca5a5;
        }
        .clear{
            padding-bottom: 0;
        }
    }
</style>

<div class="filter-container" class:display={words.length > 0}>
    <div class="tags">
        {#each words as word}
            <div class="tag" on:click={deleteWord}>
                <span class="tag-text">{word}</span>
                <div class="tag-cross">
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="14"
                        height="14">
                        <path
                            fill="#FFF"
                            fill-rule="evenodd"
                            d="M11.314 0l2.121 2.121-4.596 4.596 4.596
                            4.597-2.121 2.121-4.597-4.596-4.596 4.596L0
                            11.314l4.596-4.597L0 2.121 2.121 0l4.596
                            4.596L11.314 0z" />
                    </svg>
                </div>
            </div>
        {/each}
    </div>
    <div class="clear" on:click={clear}>
        <span>Clear</span>
    </div>
</div>
