# Creating a button menu using HTML, CSS and JavaScript

You will be creating a button menu that has a hover state and also allows you to select a button when you click on it. The final project can be seen in this [Codepen](https://codepen.io/andrewbaisden/pen/BajgPKP).

## Step 1

Setup a project on your local computer and then open it in your code editor. In the root folder create files for `index.html` `styles.css` and `index.js`

## Step 2

Copy and paste the code into their corresponding files

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Button Menu</title>
		<link rel="stylesheet" href="styles.css" />
	</head>
	<body>
		<main>
			<div class="menu">
				<button class="btn-menu selected">One</button>
				<button class="btn-menu">Two</button>
				<button class="btn-menu">Three</button>
				<button class="btn-menu">Four</button>
				<button class="btn-menu">Five</button>
			</div>
		</main>

		<script src="index.js"></script>
	</body>
</html>
```

`styles.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Asap+Condensed:wght@400;700&display=swap');

:root {
    --main-bg: #EEEEEE;
    --menu-bg: #17C0EB;
    --menu-font-color: #FFFFFF;
    --menu-border: #25d3ff;
    --menu-bg-selected: #333333;
    --menu-bg-hover: #52dcff;
    --menu-bg-selected-chevron: #3cac1a;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    font-size: 62.5%;
}

body {
    font-size: 1.6rem;
    font-family: 'Asap Condensed', sans-serif;
    background: var(--main-bg);
}

main {
    margin: 5rem auto;
}

.menu {
    margin: 0 auto;
    display: flex;
    flex-flow: column wrap;
    width: 80rem;
    max-width: 100%;
    border-radius: 2rem;
    background: var(--menu-bg);
}

.btn-menu {
    position: relative;
    cursor: pointer;
    background: var(--menu-bg);
    border: none;
    padding: 2rem;
    color: var(--menu-font-color);
    font-weight: 700;
    border-top: 0.1rem solid var(--menu-border);
    border-bottom: 0.1rem solid var(--menu-border);
    transition: background 1s;
}

.btn-menu:hover {
    background: var(--menu-bg-hover);
}

.btn-menu:focus {
    outline: none;
    box-shadow: none;
}

.selected {
    background: var(--menu-bg-selected);
}

.selected::before {
    position: absolute;
    left: 0;
    top: 0;
    content: "";
    background: var(--menu-bg-selected-chevron);
    height: 5.6rem;
    width: 0.5rem;
}
```

`index.js`

```javascript
const btnMenu = Array.from(document.querySelectorAll('.btn-menu'));

btnMenu.forEach((btns) => {
	btns.addEventListener('click', () => {
		btnMenu.forEach((btns) => {
			btns.classList.remove('selected');
		});
		btns.classList.add('selected');
	});
});
```

## Step 3

Open the `index.html` file in a web browser or if you are using Visual Studio Code you can use the Live Server extension to make it run on a server.