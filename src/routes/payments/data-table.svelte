<script lang="ts">
	import { createTable, createRender, Render, Subscribe } from 'svelte-headless-table';
	import {
		addPagination,
		addSortBy,
		addTableFilter,
		addHiddenColumns,
		addSelectedRows
	} from 'svelte-headless-table/plugins';
	import { readable } from 'svelte/store';
	import * as Table from '$lib/components/ui/table';
	import * as DropdownMenu from '$lib/components/ui/dropdown-menu';

	import DataTableActions from './data-table-actions.svelte';
	import DataTableCheckbox from './data-table-checkbox.svelte';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { ArrowUpDown, ChevronDown } from 'lucide-svelte';

	type Payment = {
		id: string;
		amount: number;
		status: 'pending' | 'processing' | 'success' | 'failed';
		email: string;
	};
	const data: Payment[] = [
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		},
		{
			id: Math.random().toFixed(5),
			amount: parseFloat((Math.random() * 100).toFixed(2)),
			status: 'success',
			email: `ken${(Math.random() * 10).toFixed(2)}@yahoo.com`
		}
		// ...
	];

	const table = createTable(readable(data), {
		page: addPagination(),
		sort: addSortBy(),
		filter: addTableFilter({
			fn: ({ filterValue, value }) => value.toLowerCase().includes(filterValue.toLowerCase())
		}),
		hide: addHiddenColumns(),
		select: addSelectedRows()
	});

	const columns = table.createColumns([
		table.column({
			accessor: 'id',
			header: (_, { pluginStates }) => {
				const { allPageRowsSelected } = pluginStates.select;
				return createRender(DataTableCheckbox, {
					checked: allPageRowsSelected
				});
			},
			cell: ({ row }, { pluginStates }) => {
				const { getRowState } = pluginStates.select;
				const { isSelected } = getRowState(row);
				return createRender(DataTableCheckbox, {
					checked: isSelected
				});
			},
			plugins: {
				filter: {
					exclude: true
				}
			}
		}),
		table.column({
			accessor: 'status',
			header: 'Status'
		}),
		table.column({
			accessor: 'email',
			header: 'Email'
		}),
		table.column({
			accessor: 'amount',
			header: 'Amount',
			cell: ({ value }) => {
				const formatted = new Intl.NumberFormat('en-US', {
					style: 'currency',
					currency: 'USD'
				}).format(value);
				return formatted;
			},
			plugins: {
				filter: {
					exclude: true
				}
			}
		}),
		table.column({
			accessor: ({ email }) => email,
			header: '',
			cell: (item) => {
				return createRender(DataTableActions, { id: item.id });
			},
			plugins: {
				filter: {
					exclude: true
				}
			}
		})
	]);

	const { headerRows, pageRows, tableAttrs, tableBodyAttrs, pluginStates, flatColumns, rows } =
		table.createViewModel(columns);
	const { hasNextPage, hasPreviousPage, pageIndex } = pluginStates.page;
	const { filterValue } = pluginStates.filter;
	const { hiddenColumnIds } = pluginStates.hide;
	const { selectedDataIds } = pluginStates.select;

	const ids = flatColumns.map((col) => col.id);
	let hideForId = Object.fromEntries(ids.map((id) => [id, true]));
	$: $hiddenColumnIds = Object.entries(hideForId)
		.filter(([, hide]) => !hide)
		.map(([id]) => id);
	const hidableCols = ['status', 'email', 'amount'];
</script>

<div>
	<div class="flex items-center py-4">
		<Input class="max-w-sm" placeholder="Filter emails..." type="text" bind:value={$filterValue} />
		<DropdownMenu.Root>
			<DropdownMenu.Trigger asChild let:builder>
				<Button variant="outline" class="ml-auto" builders={[builder]}>
					Columns <ChevronDown class="ml-2 h-4 w-4" />
				</Button>
			</DropdownMenu.Trigger>
			<DropdownMenu.Content>
				{#each flatColumns as col}
					{#if hidableCols.includes(col.id)}
						<DropdownMenu.CheckboxItem bind:checked={hideForId[col.id]}>
							{col.header}
						</DropdownMenu.CheckboxItem>
					{/if}
				{/each}
			</DropdownMenu.Content>
		</DropdownMenu.Root>
	</div>
	<div class="rounded-md border">
		<Table.Root {...$tableAttrs}>
			<Table.Header>
				{#each $headerRows as headerRow}
					<Subscribe rowAttrs={headerRow.attrs()}>
						<Table.Row>
							{#each headerRow.cells as cell (cell.id)}
								<Subscribe attrs={cell.attrs()} let:attrs let:props props={cell.props()}>
									<Table.Head {...attrs} class="[&:has([role=checkbox])]:pl-3">
										{#if cell.id === 'amount'}
											<div class="text-right">
												<Render of={cell.render()} />
											</div>
										{:else if cell.id === 'email'}
											<Button variant="ghost" on:click={props.sort.toggle}>
												<Render of={cell.render()} />
												<ArrowUpDown class={'ml-2 h-4 w-4'} />
											</Button>
										{:else}
											<Render of={cell.render()} />
										{/if}
									</Table.Head>
								</Subscribe>
							{/each}
						</Table.Row>
					</Subscribe>
				{/each}
			</Table.Header>
			<Table.Body {...$tableBodyAttrs}>
				{#each $pageRows as row (row.id)}
					<Subscribe rowAttrs={row.attrs()} let:rowAttrs>
						<Table.Row {...rowAttrs}>
							{#each row.cells as cell (cell.id)}
								<Subscribe attrs={cell.attrs()} let:attrs>
									<Table.Cell {...attrs} class="[&:has([role=checkbox])]:pl-3">
										{#if cell.id === 'amount'}
											<div class="text-right font-medium">
												<Render of={cell.render()} />
											</div>
										{:else if cell.id === 'status'}
											<div class="capitalize">
												<Render of={cell.render()} />
											</div>
										{:else}
											<Render of={cell.render()} />
										{/if}
									</Table.Cell>
								</Subscribe>
							{/each}
						</Table.Row>
					</Subscribe>
				{/each}
			</Table.Body>
		</Table.Root>
	</div>
	<div class="flex items-center justify-end space-x-2 py-4">
		<div class="flex-1 text-sm text-muted-foreground">
			{Object.keys($selectedDataIds).length} of{' '}
			{$rows.length} row(s) selected.
		</div>
		<Button
			variant="outline"
			size="sm"
			on:click={() => ($pageIndex = $pageIndex - 1)}
			disabled={!$hasPreviousPage}>Previous</Button
		>
		<Button
			variant="outline"
			size="sm"
			disabled={!$hasNextPage}
			on:click={() => ($pageIndex = $pageIndex + 1)}>Next</Button
		>
	</div>
</div>
