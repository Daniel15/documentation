---
title: "Snapshots Screen"
description: "Provides information on the settings and functions found on the Snapshots screen."
weight: 35 
tags:
- scalesnapshots
- scaledatasets
- scalezvols
- scalestorage
---

{{< toc >}}

The **Snapshots** screen, accessed from the **Datasets** screen by clicking **Manage Snapshots** on the **Data Protection** widget, provides a list of existing snapshots filtered for the snapshot you selected, allows you to add new or manage existing snapshots. 

The **Snapshots** screen also opens when you click **Snapshots** on the **[Periodic Snapshot Tasks]({{< relref "PeriodicSnapshotTasksScreensSCALE.md" >}})** widget found on the **Data Protection** screen.

## Snapshots Screen

If the selected snapshot does not have snapshots the screen displays **No Snapshots are Available**.

![SnapshotsScreenNoSnapshotsAvailable](/images/SCALE/22.12/SnapshotsScreenNoSnapshotsAvailable.png "Snapshots Screen No Snapshots Available")

To check for snapshots for other datasets, clear the search filter of the dataset path.

![SnapshotsScreenWithAllSnapshots](/images/SCALE/22.12/SnapshotsScreenWithAllSnapshots.png "Snapshots Screen with all Snapshots")

{{< expand "My Snapshot screen is blank" "v" >}}
If your **Snapshots** screen does not display a list of snapshots and you know you added snapshots, clear the dataset path in the search field to show all dataset and zvol snapshots on the system.
{{< /expand >}}

**Add** opens the **[Add Snapshot](#add-snapshot-screen)** screen.

### Show Extra Columns

Click the **Show Extra Columns** toggle to add extra information columns to the list of snapshots. This opens the **Show Extra Columns** dialog.

![SnapshotsScreenShowingExtraColumns](/images/SCALE/22.12/SnapshotsScreenShowingExtraColumns.png "Snapshot Screen Showing Extra Columns")

**Show** adds the extra columns to the list of snapshots. These columns add the space used (**Used**), the snapshot creation date, and the amount of data the dataset can access (**Referenced**).

Click the toggle again to open the **Hide Extra Columns** dialog. **Hide** to return to the default view with only the **Dataset** and **Snapshot** columns.

## Snapshot Details Screen
Click anywhere on a snapshot to expand it and view more information and options for that snapshot. 

![SnapshotsScreenExpandedSnapshot](/images/SCALE/22.12/SnapshotsScreenExpandedSnapshot.png "Expanded Snapshot Screen")

Select the checkbox to the left of each snapshot to select multiple snapshots and display the **Batch Operations** option to **Delete** the selected snapshots.

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Delete** | Opens a **[Delete](#delete-snapshot)** confirmation dialog for the selected snapshot(s). Select **Confirm** to activate the **Delete** button. |
| **Clone to New Dataset** | Opens the **[Clone to New Dataset](#clone-snapshot))** window where you enter a new name or clone with the default value in the **Dataset Name** field. |
| **Rollback** | Opens the **[Dataset Rollback From Snapshot](#dataset-rollback-from-snapshot-dialog)** window with three radio button options. **Confirm** activates the **Rollback** button. |
| **Hold** | Select to prevent the snapshot from being deleted. If selected and you batch-operation delete datasets, this opens an error displays with the name of the dataset and prevents the delete operation from continuing. |
{{< /truetable >}}

### Dataset Rollback from Snapshot Window
The snapshot **Rollback** option replaces the data in the selected dataset with the information saved in the snapshot. 
{{< hint type=warning >}}
WARNING: Rolling the dataset back destroys data on the dataset and can destroy additional snapshots that are related to the dataset. 
This can result in permanent data loss!
Do not roll back until all desired data and snapshots are backed up.
{{< /hint >}}
{{< expand "Click Here for More Information" "v" >}}
There are three **Stop Rollback if Snapshot Exists** radio button options that impose safety levels on the rollback operation. 
When the safety check finds additional snapshots that are directly related to the dataset you are rolling back it cancels the rollback.

![DatasetRollbackFromSnapshotWindow](/images/SCALE/22.12/DatasetRollbackFromSnapshotWindow.png "Dataset Rollback from Snapshot")

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Newer Intermediate, Child, and clone** | Select to stop rollback when the safety check finds any related intermediate, child dataset, or clone snapshots that are newer than the rollback snapshots. |
| **Newer Clone** | Select to stop rollback when the safety check finds any related clone snapshots that are newer than the rollback snapshot. |
| **No Safety Check (CAUTION)** | Select to stop rollback if snapshot exists. The rollback destroys any related intermediate, child dataset, and cloned snapshots that are newer than the rollback snapshot.  |
| **Confirm** | Select to confirm the selection and activate the **Rollback** button. |
{{< /truetable >}}
{{< /expand >}}

### Clone Snapshot and Promote Dataset

![SnapshotsListingExpandedSCALE1](/images/SCALE/22.12/SnapshotsListingExpandedSCALE1.png "Snapshot Listing") 

{{< include file="/_includes/CloneAndPromoteSnapshotDataset.md" >}}

### Delete Snapshot
The snapshot **Delete** option opens a window that lists the snapshot(s) you select. 

![DeleteSnapshotDialog](/images/SCALE/22.12/DeleteSnapshotDialog.png "Delete Single Snapshot")

**Confirm** activates the **Delete** button.

#### Batch Operations - Delete
To delete more than one snapshot in one operation, select the checkbox beside the datasets you want to delete and to display the **Batch Operations Delete** option. 
{{< expand "Click Here for More Information" "v" >}}

![SnapshotsScreenBatachOperations](/images/SCALE/22.12/SnapshotsScreenBatachOperations.png "Batch Operations Delete Snapshot")

**Batch Operations Delete** opens a window listing all selected snapshots.

![DeleteMultipleSnapshotsWindow](/images/SCALE/22.12/DeleteMultipleSnapshotsWindow.png "Batch Operations Delete Snapshot Window")

**Confirm** activates the **Delete** button. If a snaphot has the **[Hold](#snapshot-details-screen)** option selected, an error displays to prevent you from deleting that snapshot.
{{< /expand >}}
## Add Snapshot Screen

The **Add Snapshots** screen allows you to create a snapshot while on the **Snapshots** screen. It also opens when you click **Create Snapshot** on the **Dataset Protection** widget on the **Datasets** screen. 
{{< expand "Click Here for More Information" "v" >}}
**Create Snapshot** on the **Dataset Protection** widget opens the **Add Snapshot** screen. The **Dataset** field is prepopulated with the name of the dataset you selected on the **Datasets** screen. If you open it using **Add** on the **Snapshots** screen you select the value in the **Dataset** field.

![AddSnapshotScreen](/images/SCALE/22.12/AddSnapshotScreen.png "Add a New Snapshot")

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Dataset** | Select the dataset or zvol from the dropdown list. The snapshot created is from this dataset or zvol. |
| **Name** | TrueNAS populates this with a name but you can override the name with any string of your choice. You cannot use **Name** and **Naming Schema** for the same snapshot. |
| **Naming Schema** | Select an option from the dropdown list or leave this blank to use the system-populated name in the **Name** field. This generates a name for the snapshot using the naming schema from a previously-entered periodic snapshot. This allows replication of the snapshot. You cannot use **Naming Schema** with **Name**. Selecting a schema option overwrites the value in **Name**. |
| **Recursive** | Select to include child datasets or zvols in the snapshot. |
{{< /truetable >}}

**Save** retains the settings and returns to the **Snapshots** screen. 
{{< /expand >}}

{{< taglist tag="scalesnapshots" limit="10" >}}
{{< taglist tag="scaledatasets" limit="10" title="Related Dataset Articles" >}}
{{< taglist tag="scalezvols" limit="10" title="Related Zvols Articles" >}}
