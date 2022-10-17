React Table is a really powerful datagrid package for React that lets you create dynamic tables. It has many use cases and the package has an extensive list of features. In this tutorial I will show you how to build a Movie Database application.

The Movie Database application will have the functionality below:

- Displays data inside of a table
- Lets you filter by movie name and genre
- Has pagination that limits the data results
- Allows you to navigate forwards and backwards through the table data
- Can be sorted by ascending and descending order when you click on the **Movie** and **Genre** heading labels

The final design can be seen below in this image.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1641242724/movie-database_jhh8lx.png](https://res.cloudinary.com/d74fh3kw/image/upload/v1641242724/movie-database_jhh8lx.png)

## Prerequisites

- Node, npm and yarn installed
- A Code editor or IDE
- A BASH Terminal app

This tutorial will be using npm but you can use yarn if you want just use the appropriate commands.

## Building the Movie Database App

Use your BASH Terminal to create a folder for the project and setup a React boilerplate

```bash
mkdir movie-database
cd movie-database
mkdir frontend
cd frontend
npx create-react-app .
```

When this step has finished install the react-table package as well as the match-sorter package which is useful for sorting array data.

```bash
npm install react-table match-sorter --save
```

Open the project folder in your code editor and start the server. If you have Visual Studio Code installed with the command line setup you can open it in BASH.

```bash
code .
npm start
```

You should see your React application running on [http://localhost:3000/](http://localhost:3000/)

Clean the application by removing boilerplate files and folders. Delete all of the files inside of the **src** folder. Now create the files below and make sure that they are inside of the **src** folder.

- index.js
- App.js
- App.css

4. Copy the code snippets below and paste them into their corresponding files.

**index.js**

```javascript
import React from 'react';

import ReactDOM from 'react-dom';

import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

**App.js**

```javascript
import React from 'react';

import { useTable, useFilters, useGlobalFilter, useSortBy, usePagination } from 'react-table';

import { matchSorter } from 'match-sorter';

import './App.css';

// Define a default UI for filtering

function DefaultColumnFilter({ column: { filterValue, preFilteredRows, setFilter } }) {
	const count = preFilteredRows.length;

	return (
		<input
			value={filterValue || ''}
			onChange={(e) => {
				setFilter(e.target.value || undefined); // Set undefined to remove the filter entirely
			}}
			placeholder={`Search ${count} records...`}
		/>
	);
}

// Fuzzy text search essentially means approximate string matching and is a way of looking up strings that match a pattern even if the characters are not in the correct order.

function fuzzyTextFilterFn(rows, id, filterValue) {
	return matchSorter(rows, filterValue, { keys: [(row) => row.values[id]] });
}

// Let the table remove the filter if the string is empty

fuzzyTextFilterFn.autoRemove = (val) => !val;

// Our table component

function Table({ columns, data }) {
	const filterTypes = React.useMemo(
		() => ({
			fuzzyText: fuzzyTextFilterFn,

			text: (rows, id, filterValue) => {
				return rows.filter((row) => {
					const rowValue = row.values[id];

					return rowValue !== undefined
						? String(rowValue).toLowerCase().startsWith(String(filterValue).toLowerCase())
						: true;
				});
			},
		}),

		[]
	);

	const defaultColumn = React.useMemo(
		() => ({
			// Let's set up our default Filter UI

			Filter: DefaultColumnFilter,
		}),

		[]
	);

	const {
		getTableProps,

		getTableBodyProps,

		headerGroups,

		prepareRow,

		page,

		visibleColumns,

		canPreviousPage,

		canNextPage,

		pageOptions,

		pageCount,

		gotoPage,

		nextPage,

		previousPage,

		setPageSize,

		state: { pageIndex, pageSize },
	} = useTable(
		{
			columns,

			data,

			defaultColumn, // Be sure to pass the defaultColumn option

			filterTypes,

			initialState: { pageIndex: 0 },
		},

		useFilters,

		useGlobalFilter,

		useSortBy,

		usePagination
	);

	return (
		<>
			<div className="container">
				<div>
					<h1>Movie Database</h1>

					<table {...getTableProps()} cellPadding={0} cellSpacing={0}>
						<thead>
							{headerGroups.map((headerGroup) => (
								<tr {...headerGroup.getHeaderGroupProps()}>
									{headerGroup.headers.map((column) => (
										// Add the sorting props to control sorting. For this example

										// we can add them into the header props

										<th>
											<div {...column.getHeaderProps(column.getSortByToggleProps())}>
												{column.render('Header')}

												{/* Add a sort direction indicator */}

												<span>{column.isSorted ? (column.isSortedDesc ? ' 🔽' : ' 🔼') : ''}</span>
											</div>

											<div>
												{/* Render the columns filter UI */}

												<div>{column.canFilter ? column.render('Filter') : null}</div>
											</div>
										</th>
									))}
								</tr>
							))}

							<tr>
								<th
									colSpan={visibleColumns.length}
									style={{
										textAlign: 'left',
									}}
								></th>
							</tr>
						</thead>

						<tbody {...getTableBodyProps()}>
							{page.map((row, i) => {
								prepareRow(row);

								return (
									<tr {...row.getRowProps()}>
										{row.cells.map((cell) => {
											return <td {...cell.getCellProps()}>{cell.render('Cell')}</td>;
										})}
									</tr>
								);
							})}
						</tbody>
					</table>

					<br />

					<div className="pagination">
						<div>
							<button onClick={() => gotoPage(0)} disabled={!canPreviousPage}>
								{'<<'}
							</button>{' '}
							<button onClick={() => previousPage()} disabled={!canPreviousPage}>
								{'<'}
							</button>{' '}
							<button onClick={() => nextPage()} disabled={!canNextPage}>
								{'>'}
							</button>{' '}
							<button onClick={() => gotoPage(pageCount - 1)} disabled={!canNextPage}>
								{'>>'}
							</button>{' '}
							<span>
								Page{' '}
								<strong>
									{pageIndex + 1} of {pageOptions.length}
								</strong>{' '}
							</span>
							<span>
								| Go to page:{' '}
								<input
									type="number"
									defaultValue={pageIndex + 1}
									onChange={(e) => {
										const page = e.target.value ? Number(e.target.value) - 1 : 0;

										gotoPage(page);
									}}
									style={{ width: '100px' }}
								/>
							</span> <select
								value={pageSize}
								onChange={(e) => {
									setPageSize(Number(e.target.value));
								}}
							>
								{[10, 20, 30, 40, 50].map((pageSize) => (
									<option key={pageSize} value={pageSize}>
										Show {pageSize}
									</option>
								))}
							</select>
							<div>
								Showing the first {page.length} results of {page.length} rows
							</div>
						</div>
					</div>
				</div>
			</div>
		</>
	);
}

function App() {
	const columns = React.useMemo(
		() => [
			{
				Header: ' ',

				columns: [
					{
						Header: 'Movie',

						accessor: 'movie',

						filter: 'fuzzyText',
					},

					{
						Header: 'Genre',

						accessor: 'genre',

						filter: 'fuzzyText',
					},
				],
			},
		],

		[]
	);

	const data = [
		{ movie: 'Spider-Man: No Way Home', genre: 'Action' },

		{ movie: "The King's Man", genre: 'Action' },

		{ movie: 'The Matrix Resurrections', genre: 'Action' },

		{ movie: 'West Side Story', genre: 'Romance' },

		{ movie: 'Ghostbusters: Afterlife', genre: 'Fantasy' },

		{ movie: 'House of Gucci', genre: 'Drama' },

		{ movie: 'The Boss Baby', genre: 'Comedy' },

		{ movie: 'F9', genre: 'Action' },

		{ movie: "Don't Look Up", genre: 'Comedy' },

		{ movie: 'Dune', genre: 'Sci-fi' },

		{ movie: 'Clifford the Big Red Dog', genre: 'Comedy' },

		{ movie: 'Encanto', genre: 'Comedy' },

		{ movie: 'Shazam!', genre: 'Action' },

		{ movie: 'The Old Guard', genre: 'Action' },

		{ movie: 'My Hero Academia: Two Heroes', genre: 'Action' },

		{ movie: 'The Hobbit', genre: 'Fantasy' },

		{ movie: 'Forrest Gump', genre: 'Drama' },

		{ movie: 'The Theory of Everything', genre: 'Drama' },

		{ movie: 'Star Trek', genre: 'Sci-fi' },

		{ movie: 'Pulp Fiction', genre: 'Drama' },

		{ movie: 'Mad Max: Fury Road', genre: 'Fantasy' },

		{ movie: 'Hancock', genre: 'Action' },

		{ movie: 'Red Notice', genre: 'Action' },

		{ movie: 'The Unforgivable', genre: 'Drama' },

		{ movie: 'Dark Waters', genre: 'Drama' },

		{ movie: 'After', genre: 'Romance' },

		{ movie: 'Once Upon a Time... In Hollywood', genre: 'Drama' },

		{ movie: 'Escape Room', genre: 'Sci-fi' },

		{ movie: 'The Irishman', genre: 'Drama' },

		{ movie: 'Enola Holmes', genre: 'Adventure' },
	];

	return <Table columns={columns} data={data} />;
}

export default App;
```

**App.css**

```css
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;700&display=swap');

*,
*::before,
*::after {
	margin: 0;

	padding: 0;

	box-sizing: border-box;
}

html {
	font-size: 16px;
}

body {
	font-size: 1rem;

	background: #7f80db;

	font-family: 'Quicksand', sans-serif;

	color: #2d3039;
}

.container {
	display: flex;

	flex-flow: row nowrap;

	justify-content: center;

	align-items: center;

	width: 100vw;

	margin-top: 5rem;
}

.container h1 {
	text-align: center;

	text-transform: uppercase;

	font-size: 4rem;
}

.pagination {
	background: #edf3fa;

	padding: 1rem;

	display: flex;

	flex-flow: row nowrap;

	justify-content: center;
}

table {
	padding: 1rem;

	width: 100%;

	border-radius: 1rem;

	border: 0.5rem solid #2d3039;
}

table th div {
	font-size: 1.6rem;

	background: #2d3039;

	color: #ffffff;
}

table thead tr td {
	width: 30rem;
}

table td {
	background: #edf3fa;

	width: 30rem;

	max-width: 30rem;

	padding: 1rem;

	border-bottom: 0.1rem solid #2d3039;

	border-top: 0.1rem solid #2d3039;
}

input {
	width: 100%;

	height: 4rem;

	padding: 1rem;

	border: 0.1rem solid #2d3039;

	margin-bottom: 1rem;
}

button {
	background: #ffffff;

	height: 2rem;

	width: 2rem;

	border: none;

	cursor: pointer;
}

select {
	height: 2rem;

	width: 10rem;
}
```

You might need to reload your browser or restart the server but assuming you did everything correct you should see the Movie Database working.

## Conclusion

This was just a brief introduction you should definitely check out their website [https://react-table.tanstack.com/](https://react-table.tanstack.com/) because there are a lot of features to play around with.
