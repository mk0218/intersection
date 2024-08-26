<script>
    let listA = "";
    let listB = "";

    $: arrA = listA.split("\n");
    $: arrB = listB.split("\n");
    
    /**
   * @param {Array<string>} arrayA
   * @param {Array<string>} arrayB
   */
    function intersection(arrayA, arrayB) {
        const setA = new Set(arrayA);
        const result = new Set();
        arrayB.forEach((v) => {
            if (setA.has(v)) {
                result.add(v)
            }
        })
        return Array.from(result);
    }
    
    $: result = intersection(arrA, arrB);

    let resultPage = false;
</script>

<div class="container">
    {#if !resultPage}
    <div class="row">
        <div class="column">
            <h1>List A</h1>
            <textarea bind:value={listA} />
        </div>
        <div class="column">
            <h1>List B</h1>
            <textarea bind:value={listB} />
        </div>
    </div>
    <div class="row button">
        <button on:click={() => {resultPage = true}}>Result</button>
    </div>
    {:else}
    <div class="row">
        <div class="column">
            <h1>List A</h1>
            <ul>
                {#each arrA as v}
                    <li>{v}</li>
                {/each}
            </ul>
        </div>
        <div class="column">
            <h1>List B</h1>
            <ul>
                {#each arrB as v}
                    <li>{v}</li>
                {/each}
            </ul>
        </div>
    </div>
    <div class="row">
        Result:
            <ul>
                {#each result as v}
                    <li>{v}</li>
                {/each}
            </ul>
    </div>
    <div class="row button">
        <button on:click={() => {resultPage = false}}>Back</button>
    </div>
    {/if}
</div>

<style>
    :global(.container) {
        box-sizing: border-box;
        position: absolute;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: stretch;
        padding: 30px;
    }

    :global(.row) {
        display: flex;
        flex-direction: row;
        flex: 1;
    }

    :global(.row:not(:first-child)) {
        margin-top: 20px;
    }

    :global(.button) {
        flex: 0 0 50px;
    }

    :global(.button button) {
        flex: 1;
    }

    :global(.column) {
        flex: 1;
        display: flex;
        flex-direction: column;
        justify-content: stretch;
    }

    :global(.column:not(:first-child)) {
        margin-left: 40px;
    }

    :global() {
        text-align: center;
    }

    :global(.column > *) {
        width: inherit;
    }

    :global(.column textarea) {
        flex: 1;
    }
</style>