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

<a href="https://ko-fi.com/miguelnto">
<img width="300" height="300" src="https://camo.githubusercontent.com/8ca6cbc30815bc3ef458755d26604c424652dc18a51df3b3d708126667c31c91/68747470733a2f2f63646e2e6275796d6561636f666665652e636f6d2f627574746f6e732f76322f64656661756c742d7265642e706e67" alt={cryptoName} />
</a>

<p>
    <button onclick={onCopy} use:copy={addr}>
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
