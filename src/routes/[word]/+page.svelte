<script lang="ts">
	import Component from './Component.svelte';
	import Ruby from './Ruby.svelte';
	import Substring from './Substring.svelte';
	export let data: any;

	console.log(data);
	import Toggle from './Toggle.svelte';

	import { isSimplifiedMode } from '$lib/store';

	const isSimplified = isSimplifiedMode();

	import SearchBar from '../SearchBar.svelte';

	import Note from './Note.svelte';
</script>

<Toggle />

<div style="margin: 2rem 1rem;">
	<SearchBar />
</div>

<div class="word-head">
	{#each data.entries as entry}
		<Ruby {...entry} />

		<p>{entry.definition}</p>
	{/each}

	<Note pinyin={data.entries[0].pinyin} word={data.entries[0].simplified} />
</div>

<div class="substrings">
	{#each data.substrings as substring}
		<Substring {substring} />

		{#if substring.components}
			<div class="components">
				{#each substring.components as component}
					<Component {component} />
				{/each}
			</div>
		{/if}
	{/each}
</div>

<!-- <h1>{data.word}{data.entries[0][2] ? ` / ${data.entries[0][2]}` : '' }</h1>
<h1><ruby>
	{#each data.simpRuby as ruby}
		{ruby.c}<rt>{ruby.p}</rt>
	{/each}
</ruby> /
<ruby>{#each data.tradRuby as ruby}{ruby.c}<rt>{ruby.p}</rt>{/each}</ruby></h1>
{#each data.entries as entry}
    <h2>{data.entries[0][2] != entry[2] ? `${entry[2]} - ` : '' }{entry[0]}</h2>
    <p>{entry[1]}</p>
{/each}

{#each data.substrings as substring}
	<Substring {substring} level={1} />

	{#if substring.components}
		{#each substring.components as component}
			<Component {component} level={2} />
		{/each}
	{/if}
{/each} -->

<style>
	.word-head {
		display: inline-block;
	}
</style>
