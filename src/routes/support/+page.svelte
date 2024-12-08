<script lang="ts">
    import BitcoinQr from "$lib/images/bitcoin.png";
    import MoneroQr from "$lib/images/monero.png";
    import CryptoDonation from "../../components/CryptoDonation.svelte";
    import CoffeeDonation from "../../components/CoffeeDonation.svelte";
    import PixDonation from "../../components/PixDonation.svelte";
    const bitcoinAddress: string = "bc1qurevytq27a62azq5vgk896uz48sms6wd3f0s4p";
    const moneroAddress: string = "45uo41ekuzC9XHz1Az6ZNyfdHLuS5qSk4RKxtJ7ENC1RbsnSPmghar4VNwavUzdsw5gEm27VpgBBDhzZg2ScWU64Kc3WA31";
    const moneroIcon: string = "logos:monero";
    const bitcoinIcon: string = "logos:bitcoin";
    const CoffeeIcon: string = "raphael:coffee"
    const kofiLink: string = "https://ko-fi.com/miguelnto"
    const livepixLink: string = "https://pixgg.com/eclipse"
    const livepixIcon: string = "fluent:live-24-filled"
</script>

<svelte:head>
    <title>Support</title>
</svelte:head>

<h1>Support</h1>

<br>

<p>
I create a bunch of stuff on the internet: open-source software, videos, tutorials, blog posts, etc. I charge for nothing, and believe these should be free of charge. 
</p>
<p>
If this blog or any of my work has ever helped you in any way, consider helping me back as well. You'll be also contributing to keep this blog alive.
</p>

<br>

<CoffeeDonation addr={kofiLink} iconName={CoffeeIcon} cryptoName="Ko-fi" />

<PixDonation addr={livepixLink} iconName={livepixIcon} cryptoName="Pixgg" />

<CryptoDonation addr={moneroAddress} QrCode={MoneroQr} iconName={moneroIcon} cryptoName="Monero" />

<CryptoDonation addr={bitcoinAddress} QrCode={BitcoinQr} iconName={bitcoinIcon} cryptoName="Bitcoin" />
