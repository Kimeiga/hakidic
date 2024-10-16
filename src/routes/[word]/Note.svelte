<script lang="ts">
	import { Doc, Collection } from 'sveltefirets';
	import { authState } from 'sveltefirets';
	import { user } from '$lib/user';
	import { set } from 'sveltefirets';

	export let pinyin: string;
	export let word: string;
	export let newNote: string = '';

	let editing = false;
	let displayName = '';

	$: {
		if ($user) {
			displayName = $user.displayName;
		}
	}

	function setNote() {
		set(`word/note/${pinyin}-${word}/${displayName}`, {
			note: newNote
		});
	}

	function save() {
		setNote();
		editing = false;
	}
</script>

<p>{`word/note/${pinyin}-${word}`}</p>
<p>Notes:</p>
{#if !editing}
	<Collection path="word/note/{pinyin}-{word}" let:data={c} log>
		{#each c as cd}
			{cd.id}
			<Doc path="word/note/{pinyin}-{word}/{cd.id}" let:data={d}>
				<button style="display: block;" on:click={() => (editing = true)}
					>{d.note ? 'Edit Note' : 'Add Note'}</button
				>
			</Doc>
		{/each}
	</Collection>
	<!-- <Doc path="word/{pinyin}-{word}/{displayName}/note" let:data={d} log>
		{d.note}
		<button style="display: block;" on:click={() => (editing = true)}
			>{d.note ? 'Edit Note' : 'Add Note'}</button
		>
	</Doc> -->
	<!-- <button on:click={() => (editing = false)}>Cancel</button>
	<button on:click={() => (editing = false)}>Save</button> -->
{:else}
	<textarea placeholder="Note..." bind:value={newNote} />
	<button on:click={save}>Save</button>
{/if}
