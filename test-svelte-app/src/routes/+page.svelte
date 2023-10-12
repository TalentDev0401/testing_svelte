<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	import axios from 'axios';
	let data = "";
	export const getResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts/1')
		.then((response) => response.json())
		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const listResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts')
		.then((response) => response.json())
		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const createResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts', {
			method: 'POST',
			body: JSON.stringify({
				title: 'foo',
				body: 'bar',
				userId: 1,
			}),
			headers: {
				'Content-type': 'application/json; charset=UTF-8',
			},
		})
		.then((response) => response.json())
		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const updateResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts/1', {
			method: 'PUT',
			body: JSON.stringify({
				id: 1,
				title: 'foo',
				body: 'bar',
				userId: 1,
			}),
			headers: {
				'Content-type': 'application/json; charset=UTF-8',
			},
		})
		.then((response) => response.json())
		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const patchResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts/1', {
  			method: 'PATCH',
  			body: JSON.stringify({
    			title: 'foo',
  			}),
  			headers: {
    			'Content-type': 'application/json; charset=UTF-8',
  			},
		})
  		.then((response) => response.json())
  		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const deleteResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts/1', {
  			method: 'DELETE',
		}).then((res) => {
			if(res.ok) {
				data = "Data was removed successfully.";
			}
		});
	}

	export const filterResource = () => {
		fetch('https://jsonplaceholder.typicode.com/posts?userId=1')
  		.then((response) => response.json())
  		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

	export const listNestedResource =() => {
		fetch('https://jsonplaceholder.typicode.com/posts/1/comments')
  		.then((response) => response.json())
  		.then((json) => {
			console.log('json:', json)
			data = JSON.stringify(json);
		});
	}

</script>

<svelte:head>
	<title>Test App</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="row">
		<div class="column" id="button_panel">
			<button type="button" id="get_resource" on:click={getResource}>
				Getting a resource
			</button>
			<button type="button" id="list_all_resource" on:click={listResource}>
				Listing all resource
			</button>
			<button type="button" id="create_resource" on:click={createResource}>
				Creating a resource
			</button>
			<button type="button" id="update_resource" on:click={updateResource}>
				Updating a resource
			</button>
			<button type="button" id="patch_resource" on:click={patchResource}>
				Patching a resource
			</button>
			<button type="button" id="delete_resource" on:click={deleteResource}>
				Deleting a resource
			</button>
			<button type="button" id="filter_resource" on:click={filterResource}>
				Filtering resources
			</button>
			<button type="button" id="list_nested_resource" on:click={listNestedResource}>
				Listing nested resources
			</button>
		</div>
		<div class="column" id="data_panel">
			<div class="scroll">
				<p id="response">{data}</p>
    		</div>
		</div>
	</div>	
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		align-items: left;
		flex: 0.6;
	}

	button {
		float: after;
		margin: 10px;
  		padding: 10px;
	}

	 div.scroll {
		float: left;
        background-color: #fed9ff;
        height: 100%;
        overflow-x: hidden;
        overflow-y: auto;
        text-align: center;
        padding: 20px;
      }


	  * {
  			box-sizing: border-box;
		}

		/* Create two equal columns that floats next to each other */
		.column {
			background-color: #fed9ff;
  			float: left;
  			width: 50%;
  			padding: 10px;
  			height: 300px; /* Should be removed. Only for demonstration */
		}

		/* Clear floats after the columns */
		.row:after {
  			content: "";
  			display: table;
  			clear: both;
		}

		


</style>









