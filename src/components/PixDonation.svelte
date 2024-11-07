<script lang="ts">
    import { copy } from 'svelte-copy';
    const { addr, iconName, cryptoName } = $props<{
        addr: string,
        iconName: string,
        cryptoName: string,
    }>();
    
    import Icon from '@iconify/svelte';
    const copiedMsg: string = "Copied to your clipboard!";
    const sleep = (time: number | undefined) => new Promise(resolve => setTimeout(resolve, time));
    
    let cryptoaddr = $state(addr);
    
    async function onCopy() {
        cryptoaddr = copiedMsg;
        await sleep(1000);
        cryptoaddr = addr; 
    }
</script>

<Icon width={20} height={20} icon={iconName} style="display: inline" inline={true} /> 
<b class="crypto">{cryptoName}</b>

<p>
    <button on:click={onCopy} use:copy={addr}>
        <b class="address">{cryptoaddr}</b>
        <Icon width={20} height={20} icon="solar:copy-bold" style="display: inline" inline={true} /> 
    </button>
</p>


<style>
    .crypto {
        font-size: 1.5em;
    }
    img {
        margin-top: 1em;
        margin-bottom: 1em;
    }
    button {
        height: 2em;
        background-color: var(--surface-3);
        color: var(--text-1);
        margin-bottom: 2em;
    }
    .address {
        text-shadow: none;
        font-size: 0.9em;
    }
</style>
