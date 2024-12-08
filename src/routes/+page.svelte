<script lang="ts">
    const brIcon: string = "twemoji:flag-brazil";
    const ukIcon: string = "twemoji:flag-united-kingdom";
    const frIcon: string = "twemoji:flag-france";
    const espIcon: string = "twemoji:flag-spain";
    import Icon from '@iconify/svelte';
    import myphoto from "$lib/images/me.png";

</script>

<svelte:head>
    <title>miguelnto</title>
</svelte:head>

<h1>Hey, I'm Miguel.</h1>

<br>

<img width="230" height="230" src={myphoto} alt="me" />

<br>

<p>Hello there! I'm Miguel Neto, a <b>Software Developer</b> trying to solve real world problems and make software development easier to everyone.</p>
<p>This website is meant to be my <i>internet home</i> where I'll post some thoughts about things I'm interested in, such as Linux, web development, mobile development, systems programming and linguistics.</p>
<p>You can also find me in a lot of websites, take a look at the <a href="/contact">contact</a> page.</p>

<br>

<h4>Idioms</h4>

<br>

<Icon width={20} height={20} icon={brIcon} style="display: inline" inline={true} />
<b>Native</b>
<Icon width={20} height={20} icon={ukIcon} style="display: inline" inline={true} />
<b>C2</b>
<Icon width={20} height={20} icon={frIcon} style="display: inline" inline={true} />
<b>B2</b>
<Icon width={20} height={20} icon={espIcon} style="display: inline" inline={true} />
<b>C2</b>

<br>
