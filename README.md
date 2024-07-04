# How to delete a row when long pressing on a data row in Flutter DataTable (SfDataGrid)?.

In this article, we will show you how to delete a row when long pressing on a data row in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties. The [SfDataGrid.onCellLongPress](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/onCellLongPress.html) event is triggered when a long press gesture with a primary button is recognized for a cell. Upon triggering onCellLongPress, you can obtain the rowColumnIndex. Using the rowIndex, you can then remove the corresponding row from the [rows](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/rows.html) collection. After removing the row, update or refresh the DataGrid when the underlying data is updated by using [notifyListeners](https://api.flutter.dev/flutter/foundation/ChangeNotifier/notifyListeners.html).

```dart
 @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: SfDataGrid(
        onCellLongPress: (details) {
          // Restict the header rows.
          if (details.rowColumnIndex.rowIndex > 0) {
            //  Remove header count to the index, here 1 is minus.
            DataGridRow deleteRow = employeeDataSource
                .effectiveRows[details.rowColumnIndex.rowIndex - 1];

            employeeDataSource._employeeData.remove(deleteRow);
            employeeDataSource.refreshDataGrid();
          }
        },
        source: employeeDataSource,
        columnWidthMode: ColumnWidthMode.fill,
        columns: <GridColumn>[
          GridColumn(
              columnName: 'id',
              label: Container(
                  padding: const EdgeInsets.all(16.0),
                  alignment: Alignment.center,
                  child: const Text(
                    'ID',
                  ))),
          GridColumn(
              columnName: 'name',
              label: Container(
                  padding: const EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: const Text('Name'))),
          GridColumn(
              columnName: 'designation',
              label: Container(
                  padding: const EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: const Text(
                    'Designation',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridColumn(
              columnName: 'salary',
              label: Container(
                  padding: const EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: const Text('Salary'))),
        ],
      ),
    );
  }
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-delete-a-row-when-long-pressing-on-a-data-row-in-Flutter-DataTable).