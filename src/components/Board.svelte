<!-- Board.svelte -->
<script>
	
	import Item from './Item.svelte'
	import { boards, items } from '../stores'
	import { onMount } from 'svelte'
	import Sortable from 'sortablejs'

	export let board = null
	$: _items = $items.filter(item => item.boardId === board.id)

	const handleAddItem = () => items.add(board.id)
	const handleRemoveItem = e => items.remove(e.detail)
	const handleUpdateItem = e => items.update(e.detail)
	const handleSortItem = e => {
		const target = $items.find(item => item.id === e.item.id)
		const allItems = $items.filter(item => item.id !== e.item.id)
		const _items = allItems.filter(item => item.boardId === e.to.id)
		target.boardId = e.to.id
		_items.splice(e.newIndex, 0, target)

		const newItems = allItems
			.filter(item => item.boardId !== e.to.id)
			.concat(_items)
		items.set(newItems)
	}

	let list = null
	onMount(() => {
		if (list) {
			new Sortable(list, {
				group: 'board',
				handle: '.drag-handle',
				fallbackClass: 'sortable-fallback',
				animation: 300,
				onEnd: handleSortItem,
			})
		}
	})
</script>
<body><div class="line-gutter-backdrop"></div><table><tbody><tr><td class="line-number" value="1"></td><td class="line-content"><span class="html-doctype">&lt;!doctype html&gt;</span></td></tr><tr><td class="line-number" value="2"></td><td class="line-content"><span class="html-tag">&lt;html&gt;</span></td></tr><tr><td class="line-number" value="3"></td><td class="line-content"><span class="html-tag">&lt;head&gt;</span></td></tr><tr><td class="line-number" value="4"></td><td class="line-content">	<span class="html-tag">&lt;meta <span class="html-attribute-name">charset</span>='<span class="html-attribute-value">utf-8</span>'&gt;</span></td></tr><tr><td class="line-number" value="5"></td><td class="line-content">	<span class="html-tag">&lt;meta <span class="html-attribute-name">name</span>='<span class="html-attribute-value">viewport</span>' <span class="html-attribute-name">content</span>='<span class="html-attribute-value">width=device-width</span>'&gt;</span></td></tr><tr><td class="line-number" value="6"></td><td class="line-content"><br></td></tr><tr><td class="line-number" value="7"></td><td class="line-content">	<span class="html-tag">&lt;title&gt;</span>Svelte app<span class="html-tag">&lt;/title&gt;</span></td></tr><tr><td class="line-number" value="8"></td><td class="line-content"><br></td></tr><tr><td class="line-number" value="9"></td><td class="line-content">	<span class="html-tag">&lt;link <span class="html-attribute-name">rel</span>='<span class="html-attribute-value">icon</span>' <span class="html-attribute-name">type</span>='<span class="html-attribute-value">image/png</span>' <span class="html-attribute-name">href</span>='<a class="html-attribute-value html-resource-link" target="_blank" href="/favicon.png" rel="noreferrer noopener">/favicon.png</a>'&gt;</span></td></tr><tr><td class="line-number" value="10"></td><td class="line-content">	<span class="html-tag">&lt;link <span class="html-attribute-name">rel</span>='<span class="html-attribute-value">stylesheet</span>' <span class="html-attribute-name">href</span>='<a class="html-attribute-value html-resource-link" target="_blank" href="/global.css" rel="noreferrer noopener">/global.css</a>'&gt;</span></td></tr><tr><td class="line-number" value="11"></td><td class="line-content">	<span class="html-tag">&lt;link <span class="html-attribute-name">rel</span>='<span class="html-attribute-value">stylesheet</span>' <span class="html-attribute-name">href</span>='<a class="html-attribute-value html-resource-link" target="_blank" href="/bundle.css" rel="noreferrer noopener">/bundle.css</a>'&gt;</span></td></tr><tr><td class="line-number" value="12"></td><td class="line-content"><br></td></tr><tr><td class="line-number" value="13"></td><td class="line-content">	<span class="html-tag">&lt;link <span class="html-attribute-name">rel</span>="<span class="html-attribute-value">stylesheet</span>" <span class="html-attribute-name">href</span>="<a class="html-attribute-value html-resource-link" target="_blank" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="noreferrer noopener">https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css</a>" <span class="html-attribute-name">integrity</span>="<span class="html-attribute-value">sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T</span>" <span class="html-attribute-name">crossorigin</span>="<span class="html-attribute-value">anonymous</span>"&gt;</span></td></tr><tr><td class="line-number" value="14"></td><td class="line-content">	<span class="html-tag">&lt;link <span class="html-attribute-name">rel</span>="<span class="html-attribute-value">stylesheet</span>" <span class="html-attribute-name">href</span>="<a class="html-attribute-value html-resource-link" target="_blank" href="path/to/font-awesome/css/font-awesome.min.css" rel="noreferrer noopener">path/to/font-awesome/css/font-awesome.min.css</a>" <span class="html-attribute-name">type</span>="<span class="html-attribute-value">text/html</span>"&gt;</span></td></tr><tr><td class="line-number" value="15"></td><td class="line-content">	<span class="html-tag">&lt;script <span class="html-attribute-name">src</span>="<a class="html-attribute-value html-resource-link" target="_blank" href="https://kit.fontawesome.com/5d6d23fe14.js" rel="noreferrer noopener">https://kit.fontawesome.com/5d6d23fe14.js</a>" <span class="html-attribute-name">crossorigin</span>="<span class="html-attribute-value">anonymous</span>"&gt;</span><span class="html-tag">&lt;/script&gt;</span></td></tr><tr><td class="line-number" value="16"></td><td class="line-content"><br></td></tr><tr><td class="line-number" value="17"></td><td class="line-content">	<span class="html-tag">&lt;script <span class="html-attribute-name">defer</span> <span class="html-attribute-name">src</span>='<a class="html-attribute-value html-resource-link" target="_blank" href="/bundle.js" rel="noreferrer noopener">/bundle.js</a>'&gt;</span><span class="html-tag">&lt;/script&gt;</span></td></tr><tr><td class="line-number" value="18"></td><td class="line-content"><span class="html-tag">&lt;/head&gt;</span></td></tr><tr><td class="line-number" value="19"></td><td class="line-content"><br></td></tr><tr><td class="line-number" value="20"></td><td class="line-content"><span class="html-tag">&lt;body&gt;</span></td></tr><tr><td class="line-number" value="21"></td><td class="line-content"><span class="html-tag">&lt;/body&gt;</span></td></tr><tr><td class="line-number" value="22"></td><td class="line-content"><span class="html-tag">&lt;/html&gt;</span></td></tr><tr><td class="line-number" value="23"></td><td class="line-content"><span class="html-end-of-file"></span></td></tr></tbody></table></body>
<style>
	.board.wrapper {
		background-color: #ebebeb;
	}

	.meta {
		padding: 0 4px;
		display: flex;
		justify-content: space-between;
		align-content: center;
	}

	.item-list {
		padding: 16px 0px;
	}

	.add-item {
		float: right;
		width: 35px;
		height: 35px;
		padding: 0;
	}

</style>
