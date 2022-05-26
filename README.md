# Javascript Webpage Demo

## Objective: 
Deploy a javascript website which uses a user form to retrieve requested UFO sighting data back in table format.

## Tools & databases used:
- Javascript
- HTML
- CSS
- Bootstrap

## Method:

My UFO data is contained inside a data.js file. I need to building a function that builds a table for the website, creates a filter from a user form, then filters the UFO table to display only what matches the form criteria.

```
// Build table
var tbody = d3.select("tbody");
function buildTable(data) {
  tbody.html("");
  data.forEach((dataRow) => {
    let row = tbody.append("tr");
    Object.values(dataRow).forEach((val) => {
      let cell = row.append("td");
      cell.text(val);
    });
  });
}
var filters = {};
```

The function for building the table.
1) First step I need to clear existing data.
2) Next I want to loop through each object in the data then append a row & cell for each data row.
3) This gets me a table output for the HTML page.

```
// Update filter
var filters = {};
function updateFilters() {
  let changedElement = d3.select(this);
  let elementValue = changedElement.property("value");
  let filterId = changedElement.attr("id");
  if (elementValue) {
    filters[filterId] = elementValue;
  }
  else {
    delete filters[filterId];
  }
  filterTable();
}
```

This function will be for my filter.
1) I need a variable which contains all the filters.
2) Next is a variable that saves the changed element using D3 select().
3) Then I'm saving the changed value as a variable, then changing the id of the filter.
4) Afterwards I'm setting up an if statement that will clear empty fields from the filter, and keep the entered values.
5) Then calling my table new table function to output results.

```
// Filter table data to entered values
function filterTable() {
  let filteredData = tableData;
  Object.entries(filters).forEach(([key, value]) => {
    console.log(`${key}: ${value}`);
    filteredData = filteredData.filter(row => row[key] === value);
  });
  buildTable(filteredData);
}
d3.selectAll("input").on("change", updateFilters);
buildTable(tableData);
```

From here it's a simple function to filter the original data.
1) I'm putting the tableData into a new variable for filtering to preserve the original variable.
2) Next I'm taking my filtered object and filtering key values.
3) Then I'm calling the buildTable function I created earlier with the input of my new table variable.
