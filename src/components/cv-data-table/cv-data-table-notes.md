# CvDataTable

A Vue implementation of a Carbon Components DataTable.

http://www.carbondesignsystem.com/components/DataTable/code

## Usage

- Sorting, filtering and pagination are the responsibility of the component user. This component raises events to facilitate this.

- The search bar appears only if the search event is listened for.

### minimal

```html
<cv-data-table :columns="columns" :data="filteredData"></cv-data-table>
```

See Attributes, Slots and Events to see how to add additional features to the table.

### Slotting data

Instead of supply data as two dimensional array the user can supply slotted content using the CvDataTableRow and CvDataTableCell components.

The CvDataTableCell component can also take slotted contnet which allowing the freedom to create an editable table.

Like sorting and filtering it is the users responsibility to deal with edited data. The data table component does not listen to slotted cell components.

```html
<cv-data-table :columns="columns">
  <template slot="data">
    <cv-data-table-row
      v-for="(row, rowIndex) in [`ibm`, `beta`, `local`, `custom`, `private`]"
      :key="`${rowIndex}`"
      :value="`${rowIndex}`"
    >
      <cv-data-table-cell>
        <input
          type="text"
          :value="row"
          style="border: none; background: none; width: 100%;"
        />
      </cv-data-table-cell>
      <cv-data-table-cell>
        <input
          type="number"
          :value="rowIndex * rowIndex"
          style="border: none; background: none; width: 100%;"
        />
      </cv-data-table-cell>
      <cv-data-table-cell>
        <input
          type="password"
          value="ASecret"
          style="border: none; background: none; width: 100%;"
        />
      </cv-data-table-cell>
      <cv-data-table-cell>
        <a href="https://vue.carbondesignsystem.com">Here</a>
      </cv-data-table-cell>
      <cv-data-table-cell>
        <cv-tag :kind="row" label="I am a tag" />
      </cv-data-table-cell>
      <cv-data-table-cell>
        <cv-button type="button" v-html="`Clicky ${row}`" style="width: 100%;">
        </cv-button>
      </cv-data-table-cell>
    </cv-data-table-row>
  </template>
</cv-data-table>
```

## Attributes

- columns: An array containing a list of columns
  - Columns can be string labels or objects
  - If objects they must contain a 'label' and can optionally contain
    - a headingStyle object to be applied to the column headings.
    - a dataStyle object to be applied to the data in the column.
- data: Two dimensional array of strings.

- auto-width: table will size use auto sizing
- borderless: table will have no border
- options: 'compact', 'small', 'standarad', '' or 'tall'
- pagination: default: false, can be set to true or an object containing camel case props for a CvPagination component
- sortable: can be sorted
- row-size: optional - default: '',
  - 'compact', 'small', '', 'tall'
- zebra: optional - default: false ; boolean is the table striped

## Slots

- batch-actions: Ghost style buttons shown when rows are selected. An array of selected row indexes is returend from the computed property CvDataTable.selectedRows.
- actions
- data: overrides passing data as a property, expects CvDataTableRow and CvDataTableCell. CvDataTableCell expects slotted content.

## Events

- pagination: re-raises CvPageination change event.
- search: supplies the string being search for. NOTE: Only shown if search is listened for.
- sort({ index, order: 'ascending' or 'descending' or 'none' or ''})

As per note sort and filter behviours are delegated to the component user.

### Additional

N/A