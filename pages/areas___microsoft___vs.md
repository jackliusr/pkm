- [All-In-One Search experience](https://learn.microsoft.com/en-us/visualstudio/ide/visual-studio-search?view=vs-2022#about-the-all-in-one-search-experience): Option, Ctrl+Q:
	- You can use the **Ctrl**+**Q** keyboard shortcut for feature searches, and the **Ctrl**+**T** keyboard shortcut for code searches.
	- <table aria-label="Table 1" class="table table-sm margin-top-none">
	  <thead>
	  <tr>
	  <th>Filter</th>
	  <th>Prefix</th>
	  <th>Keyboard shortcut</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td>files</td>
	  <td><code>f:</code></td>
	  <td><strong>Ctrl</strong>+<strong>Shift</strong>+<strong>T</strong></td>
	  </tr>
	  <tr>
	  <td>types</td>
	  <td><code>t:</code></td>
	  <td><strong>Ctrl</strong>+<strong>1</strong>, <strong>Ctrl</strong>+<strong>T</strong></td>
	  </tr>
	  <tr>
	  <td>members</td>
	  <td><code>m:</code></td>
	  <td><strong>Alt</strong>+<strong>\</strong></td>
	  </tr>
	  </tbody>
	  </table>
- CLI-based project (.esproj)
- Shared Project: shproj
- The `.projitems` file defines what the `.shproj` file will add to the compilation.
- Develop code in Visual Studio without projects or solutions: .code-workspace json file
  
  ``` json
  {
      "folders" : [
          {
              "path" : "some\\child\\foo",
              "name" : "The Foo"
          },
          {
              "path" : "..\\..\\some\\unrelated\\bar"
          },
          {
              "path" : "C:\\a\\full\\path\\baz"
          },
          {
              "path" : "${env.ANY_ENV_VARIABLE}\\foobar"
          }
      ]
  }
  ```