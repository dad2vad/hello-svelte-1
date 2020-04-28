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
<body>


<div class="appbar svelte-no08ro"><h1 class="title svelte-no08ro">Svelte Todo App</h1></div> <div class="container svelte-u5r16g"><div class="container-fluid">
  <div class="row">
<div class="item svelte-u5r16g"><div class="board wrapper card svelte-ylyubz"><div class="card-body"><div class="meta svelte-ylyubz"><h5 class="card-title">Planning</h5> <span class="count text-secondary">2</span></div> <div id="df323b5d-69a4-456c-8ccf-241f537eb729" class="item-list svelte-ylyubz"><div id="950462c1-0e38-4281-aa83-42e0ac252487" class="item card p-1 mb-2 shadow-sm svelte-baqzyi"><div class="drag-handle pointer svelte-baqzyi"><i class="fas fa-grip-lines" aria-hidden="true"></i></div> <span class="item-title pointer svelte-baqzyi">자료 조사하기</span> <div class="item-action"><button class="item-btn btn svelte-baqzyi"><i class="far fa-edit" aria-hidden="true"></i></button> <button class="item-btn btn svelte-baqzyi"><i class="far fa-trash-alt" aria-hidden="true"></i></button></div></div><div id="ba5bfdda-9cbf-4aed-abc1-cecffcc3b4c1" class="item card p-1 mb-2 shadow-sm svelte-baqzyi"><div class="drag-handle pointer svelte-baqzyi"><i class="fas fa-grip-lines" aria-hidden="true"></i></div> <span class="item-title pointer svelte-baqzyi">교양책 읽기</span> <div class="item-action"><button class="item-btn btn svelte-baqzyi"><i class="far fa-edit" aria-hidden="true"></i></button> <button class="item-btn btn svelte-baqzyi"><i class="far fa-trash-alt" aria-hidden="true"></i></button></div></div></div> <div class="card-action"><button class="add-item btn svelte-ylyubz"><i class="fas fa-plus" aria-hidden="true"></i></button></div></div></div> </div>
        <div class="row">
    
            
  </div></div></div>


</div><body>


 <div class="container svelte-u5r16g"><div class="container-fluid">
  <div class="row">
<div class="item svelte-u5r16g"><div class="board wrapper card svelte-ylyubz"><div class="card-body"><div class="meta svelte-ylyubz"><h5 class="card-title">Planning</h5> <span class="count text-secondary">2</span></div> <div id="df323b5d-69a4-456c-8ccf-241f537eb729" class="item-list svelte-ylyubz"><div id="950462c1-0e38-4281-aa83-42e0ac252487" class="item card p-1 mb-2 shadow-sm svelte-baqzyi"><div class="drag-handle pointer svelte-baqzyi"><i class="fas fa-grip-lines" aria-hidden="true"></i></div> <span class="item-title pointer svelte-baqzyi">자료 조사하기</span> <div class="item-action"><button class="item-btn btn svelte-baqzyi"><i class="far fa-edit" aria-hidden="true"></i></button> <button class="item-btn btn svelte-baqzyi"><i class="far fa-trash-alt" aria-hidden="true"></i></button></div></div><div id="ba5bfdda-9cbf-4aed-abc1-cecffcc3b4c1" class="item card p-1 mb-2 shadow-sm svelte-baqzyi"><div class="drag-handle pointer svelte-baqzyi"><i class="fas fa-grip-lines" aria-hidden="true"></i></div> <span class="item-title pointer svelte-baqzyi">교양책 읽기</span> <div class="item-action"><button class="item-btn btn svelte-baqzyi"><i class="far fa-edit" aria-hidden="true"></i></button> <button class="item-btn btn svelte-baqzyi"><i class="far fa-trash-alt" aria-hidden="true"></i></button></div></div></div> <div class="card-action"><button class="add-item btn svelte-ylyubz"><i class="fas fa-plus" aria-hidden="true"></i></button></div></div></div> </div>
        <div class="row">
    
            
  </div></div></div>


</div>





</div></body></body></body></body>
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
