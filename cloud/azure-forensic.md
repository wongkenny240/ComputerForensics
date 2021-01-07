# Azure Forensic

## Azure Security Centre

Azure Security Centre triggers alerts from signatures and heuristics:

And Azure also integrates with a number of third party solutions to provide detection capabilities, such as BitDefender:

Microsoft may also send you an alert if they notice clear evidence of a compromise coming from your account:

Azure Security Centre includes built-in tools to search through logs, and record investigative findings:

Source: [https://medium.com/@cloudyforensics/azure-forensics-and-incident-response-c13098a14d8d](https://medium.com/@cloudyforensics/azure-forensics-and-incident-response-c13098a14d8d)

## Azure Acquisition

It is possible to acquire a snapshot of a machine within Azure in a number of ways, normally in VHD format.

### Magnet AXIOM

![](../.gitbook/assets/image%20%283%29.png)

### libcloudforensic

### Create a snapshot of VM using the portal or Powershell

#### Use the Azure portal

To create a snapshot, complete the following steps:

1. On the Azure portal, select Create a resource.
2. Search for and select Snapshot.
3. In the Snapshot window, select Create. The Create snapshot window appears.
4. Enter a Name for the snapshot.
5. Select an existing Resource group or enter the name of a new one.
6. Select an Azure datacenter Location.
7. For Source disk, select the managed disk to snapshot.
8. Select the Account type to use to store the snapshot. Select Standard\_HDD, unless you need the snapshot to be stored on a high-performing disk.
9. Select Create.

#### Use Powershell

1. Set some parameters:

```text
$resourceGroupName = 'myResourceGroup' 
$location = 'eastus' 
$vmName = 'myVM'
$snapshotName = 'mySnapshot'
```

1. Get the VM:

```text
$vm = Get-AzVM `
    -ResourceGroupName $resourceGroupName `
    -Name $vmName
```

2. Create the snapshot configuration. For this example, the snapshot is of the OS disk:

```text
$snapshot =  New-AzSnapshotConfig `
    -SourceUri $vm.StorageProfile.OsDisk.ManagedDisk.Id `
    -Location $location `
    -CreateOption copy
```

3. Take the snapshot:

   ```text
   New-AzSnapshot `
    -Snapshot $snapshot `
    -SnapshotName $snapshotName `
    -ResourceGroupName $resourceGroupName
   ```

### Spin up a new VM for investigation

1. Select Create a Resource and search for ‘Managed Disks’. 
2. When creating your Managed Disk, fill out the standard information. However, under ‘Source type’ make sure this is set to ‘Snapshot’ and then select your Snapshot that you have created.
3. From the Managed Disk screen you should see an option to ‘Create VM’, click this option.
4. Fill out the required information on the Create VM page
