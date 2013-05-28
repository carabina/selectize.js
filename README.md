# selectize.js
Selectize is a fast, usable, and clean &lt;select&gt; replacement (7kb gzipped). It's a lot like [Chosen](http://harvesthq.github.io/chosen/), [Select2](http://ivaynberg.github.io/select2/), and [Tags Input](https://github.com/xoxco/jQuery-Tags-Input) but with a few advantages. Licensed under the Apache License, Version 2.0… so do whatever you want with it!

- **Multi-property searching**<br>Want to search an item's title *and* description? No problem. You can even override the scoring function if you want to get crazy.
- **Caret between items**<br>Order matters sometimes. Use the [left] and [right] arrow keys to move between items.</li>
- **Select &amp; delete multiple items at once**<br>Hold down [option] on Mac or [ctrl] on Windows to select more than one item to delete.
- **Díåcritîçs supported**<br>Great for international environments.
- **Item creation**<br>Allow users to create items on the fly (async supported).
- **Remote data loading**<br>For when you have thousands of options and want them provided by the server as the user types.
- **Clean API &amp; code**<br>Interface with it and make modifications easily. Pull requests welcome!

### Table of Contents
- [Usage](#usage)
- [Options](#options)
	- [General](#general)
	- [Data / Searching](#data_searching)
	- [Callbacks](#callbacks)
	- [Rendering](#rendering)
- [License](#license)

## Usage

```html
<script type="text/javascript" src="selectize.js"></script>
<link rel="stylesheet" type="text/css" href="selectize.css" />
<script type="text/javascript">
$('select').selectize(options);
</script>
```

### Options

<table width="100%">
	<tr>
		<th valign="top" colspan="3" align="left"><a href="#general" name="general">General</a></th>
	</tr>
	<tr>
		<th valign="top" width="120px" align="left">Option</th>
		<th valign="top" align="left">Description</th>
		<th valign="top" width="60px" align="left">Type</th>
	</tr>
	<tr>
		<td valign="top"><code>delimiter</code></td>
		<td valign="top">The string to separate items by. This option is only used when Selectize is instantiated from a &lt;input type="text"&gt; element.</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>diacritics</code></td>
		<td valign="top">Enable or disable international character support.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>create</code></td>
		<td valign="top">Allow the user to create new items that aren't in the list of options.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>highlight</code></td>
		<td valign="top">Toggles matching highlighting within the dropdown menu.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>persist</code></td>
		<td valign="top">If false, items created by the user will not show up as available options once they are unselected.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>openOnFocus</code></td>
		<td valign="top">Show the dropdown immediately when the control receives focus.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>maxOptions</code></td>
		<td valign="top">The max number of items to render at once in the dropdown list of options.</td>
		<td valign="top"><code>int</code></td>
	</tr>
	<tr>
		<td valign="top"><code>maxItems</code></td>
		<td valign="top">The max number of items the user can select.</td>
		<td valign="top"><code>int</code></td>
	</tr>
	<tr>
		<td valign="top"><code>hideSelected</code></td>
		<td valign="top">If true, the items that are currently selected will not be shown in the dropdown list of options.</td>
		<td valign="top"><code>boolean</code></td>
	</tr>
	<tr>
		<td valign="top"><code>scrollDuration</code></td>
		<td valign="top">The animation duration (in milliseconds) of the scroll animation triggered when going [up] and [down] in the options dropdown.</td>
		<td valign="top"><code>int</code></td>
	</tr>
	<tr>
		<td valign="top"><code>loadThrottle</code></td>
		<td valign="top">The number of milliseconds to wait before requesting options from the server.</td>
		<td valign="top"><code>int</code></td>
	</tr>
	<tr>
		<th valign="top" colspan="2" align="left"><a href="#data_searching" name="data_searching">Data / Searching</a></th>
	</tr>
	<tr>
		<th valign="top" align="left">Option</th>
		<th valign="top" align="left">Description</th>
		<th valign="top" align="left">Type</th>
	</tr>
	<tr>
		<td valign="top"><code>dataAttr</code></td>
		<td valign="top">The &lt;option&gt; attribute from which to read JSON data about the option.</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>valueField</code></td>
		<td valign="top">The name of the property to use as the "value" when an item is selected.</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>labelField</code></td>
		<td valign="top">The name of the property to render as the option/item label (not needed when custom rendering functions are defined).</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>sortField</code></td>
		<td valign="top">The name of the property to sort by.</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>sortDirection</code></td>
		<td valign="top">Sort direction ("asc" or "desc").</td>
		<td valign="top"><code>string</code></td>
	</tr>
	<tr>
		<td valign="top"><code>searchField</td>
		<td valign="top">An array of property names to search.</td>
		<td valign="top"><code>array</code></td>
	</tr>
	<tr>
		<th valign="top" colspan="2" align="left"><a href="#callbacks" name="callbacks">Callbacks</a></th>
	</tr>
	<tr>
		<th valign="top" align="left">Option</th>
		<th valign="top" align="left">Description</th>
		<th valign="top" align="left">Type</th>
	</tr>
	<tr>
		<td valign="top"><code>load(query, callback)</code></td>
		<td valign="top">Invoked when new options should be loaded from the server.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>score(search)</code></td>
		<td valign="top">Overrides the scoring function used to sort available options. The provided function should return a number greater than or equal to zero to represent the "score" of the item. If 0, the option is declared not a match. The "search" argument is a <a href="#search">Search</a> object.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onChange(value)</code></td>
		<td valign="top">Invoked when the value of the control changes.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onItemAdd(value, $item)</code></td>
		<td valign="top">Invoked when an item is selected.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onItemRemove(value)</code></td>
		<td valign="top">Invoked when an item is deselected.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onClear()</code></td>
		<td valign="top">Invoked when the control is manually cleared via the clear() method.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onOptionAdd(value, data)</code></td>
		<td valign="top">Invoked when a new option is added to the available options list.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onOptionRemove(value)</code></td>
		<td valign="top">Invoked when an option is removed from the available options.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onDropdownOpen($dropdown)</code></td>
		<td valign="top">Invoked when the dropdown opens.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onDropdownClose($dropdown)</code></td>
		<td valign="top">Invoked when the dropdown closes.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<td valign="top"><code>onType(str)</code></td>
		<td valign="top">Invoked when the user types while filtering options.</td>
		<td valign="top"><code>function</code></td>
	</tr>
	<tr>
		<th valign="top" colspan="3" align="left"><a href="#rendering" name="rendering">Rendering</a></th>
	</tr>
	<tr>
		<td valign="top"><code>render</code></td>
		<td valign="top">
			An object containing any of the following methods:
			<table width="100%">
				<tr>
					<td valign="top"><code>option(data)</code></td>
					<td valign="top">An option in the dropdown list of available options.</td>
				</tr>
				<tr>
					<td valign="top"><code>item(data)</code></td>
					<td valign="top">A selected item.</td>
				</tr>
				<tr>
					<td valign="top"><code>option_create(data)</code></td>
					<td valign="top">The "create new" option at the bottom of the dropdown. The "data" argument contains one property: "input" (which is what the user has typed).</td>
				</tr>
			</table>
		</td>
		<td valign="top"><code>object</code></td>
	</tr>
</table>

## License

Copyright &copy; 2013 [Brian Reavis](http://twitter.com/brianreavis), [DIY](https://diy.org), & Contributors

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at: http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.