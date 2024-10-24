<script lang="ts">
    import BitcoinQr from "$lib/images/bitcoin.png";
    import MoneroQr from "$lib/images/monero.png";
    import CryptoDonation from "../../components/CryptoDonation.svelte";
    const bitcoinAddress: string = "bc1qurevytq27a62azq5vgk896uz48sms6wd3f0s4p";
    const moneroAddress: string = "45uo41ekuzC9XHz1Az6ZNyfdHLuS5qSk4RKxtJ7ENC1RbsnSPmghar4VNwavUzdsw5gEm27VpgBBDhzZg2ScWU64Kc3WA31";
    const moneroIcon: string = "logos:monero";
    const bitcoinIcon: string = "logos:bitcoin";
</script>

<svelte:head>
    <title>Contribute</title>
</svelte:head>

<h1>Contribute</h1>

<br>

<p>
I create a bunch of stuff on the internet: open-source software, livestreams, tutorials, blog posts, etc. I charge for nothing, and believe these should be free of charge. 
</p>
<p>
If this blog or any of my work has ever helped you in any way, consider helping me back as well. You'll be also contributing to keep this blog alive.
</p>

<br>

<CryptoDonation addr={moneroAddress} QrCode={MoneroQr} iconName={moneroIcon} cryptoName="Monero" />

<CryptoDonation addr={bitcoinAddress} QrCode={BitcoinQr} iconName={bitcoinIcon} cryptoName="Bitcoin" />
