---
layout: post
title: Quick Script Share - Adding A Bunch Of Random Test Users To Active Directory
date: 2016-04-15 12:18
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, PowerShell, powershell, PowerShell ISE]
---
I recently had a need to add a bunch of random users to a specific OU in Active Directory to do some testing. I didn't care what their names were, but, I wanted to be able to find all the users that belonged to each batch. Here's the script I wrote to do this.

<pre class="lang:ps decode:true ">#requires -Version 2 -Modules ActiveDirectory
&lt;#
    .Synopsis
    Adds a bunch of dummy users to Active Directory.
    .Description
    Prompts a user for an OU in their AD and makes a bunch of random users in that OU.
    .Example
    New-RandomADUsers.ps1
    Runs the script with default paramaters, will prompt for an OU
    .Example
    New-RandomADUsers.ps1 -OU 'OU=testing,OU=workingsysadmin,DC=lab,DC=workingsysadmin,DC=com' -Count 10
    Creates 10 random users in the specified OU
    .Parameter OU
    The OU to create random users in. Takes a distinguished name.
    .Parameter Count
    How many new users to create. Defaults to 10.
    .Parameter Password
    The password to assign to all the created users. Defaults to 'P@ssw0rd'.
    .Notes
    NAME:  New-RandomADUsers.ps1
    AUTHOR: Thomas Rayner
    LASTEDIT: 04/15/2016
    KEYWORDS:
    .Link
    http://workingsysadmin.com
#&gt;

[CmdletBinding()]
param
(
  [String]
  [Parameter(Position=0)]
  $OU,

  [int]
  [Parameter(Position=1)]
  $Count = 10,

  [string]
  [Parameter(Position=2)]
  $Password = 'P@ssw0rd'
)


#region FUNCTIONS
##########################START OF FUNCTIONS##########################

#Show a GUI to select an OU
function Select-GUIOU
{
    #load required assemblies
    [void] [System.Reflection.Assembly]::LoadWithPartialName('System.Windows.Forms')
    [void] [System.Reflection.Assembly]::LoadWithPartialName('System.Drawing') 

    #build the form
    $objForm = New-Object System.Windows.Forms.Form 
    $objForm.Text = 'Select an OU'
    $objForm.Size = New-Object System.Drawing.Size(900,430) 
    $objForm.StartPosition = 'CenterScreen'

    #add the OK button
    $OKButton = New-Object System.Windows.Forms.Button
    $OKButton.Location = New-Object System.Drawing.Size(75,350)
    $OKButton.Size = New-Object System.Drawing.Size(75,23)
    $OKButton.Text = 'OK'

    #assign the OK button to the AcceptButton param
    $OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
    $objForm.Controls.Add($OKButton)
    $objForm.AcceptButton = $OKButton

    #add the cancel button
    $CancelButton = New-Object System.Windows.Forms.Button
    $CancelButton.Location = New-Object System.Drawing.Size(150,350)
    $CancelButton.Size = New-Object System.Drawing.Size(75,23)
    $CancelButton.Text = 'Cancel'

    #assign the cancel button to the CancelButton param
    $CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
    $objForm.Controls.Add($CancelButton)
    $objForm.CancelButton = $CancelButton

    #add the Select OU label
    $objLabel = New-Object System.Windows.Forms.Label
    $objLabel.Location = New-Object System.Drawing.Size(10,20) 
    $objLabel.Size = New-Object System.Drawing.Size(400,20) 
    $objLabel.Text = "Please select an OU. Don't see one you want? Cancel and create it."
    $objForm.Controls.Add($objLabel) 

    #add the listbox to select an OU from
    $objListBox = New-Object System.Windows.Forms.ListBox 
    $objListBox.Location = New-Object System.Drawing.Size(10,40) 
    $objListBox.Size = New-Object System.Drawing.Size(860,90) 
    $objListBox.Height = 300

    #get all the OUs in the organization, sort them alphabetically and add them to the listbox
    $OUs = Get-ADOrganizationalUnit -filter '*'
    $OUs | Sort-Object | % { [void] $objListBox.Items.Add($_) }

    #add the listbox to the form
    $objForm.Controls.Add($objListBox) 

    #open this window on top of other windows
    $objForm.TopMost = $True

    #return the OU selected
    $result = $objForm.ShowDialog()

    #if the user clicks OK and selected an OU, return it
    if ($result -eq [System.Windows.Forms.DialogResult]::OK -and $objListBox.SelectedIndex -ge 0)
    {
        $selection = $objListBox.SelectedItem
        return $selection
    }
    else
    {
        throw { 'Did not select an OU. Script terminated.' }
    }
}

#Get the OU to create users in
function Get-OU
{
    [CmdletBinding()]
    param
    (
      [String]
      [Parameter(Position=0)]
      $OU
    )

    #if there was no OU passed, select one using the GUI
    if ([string]::IsNullOrEmpty($OU))
    {
        return $(Select-GUIOU).DistinguishedName
    }

    #if there was an OU passed, validate it exists
    else
    {
        #try to get the OU, if this is successful, return the value we used to find it (should be a DN)
        try
        {
            $TestOU = Get-ADOrganizationalUnit -Identity $OU
            return $TestOU.DistinguishedName
        }

        #if we couldn't find an OU with the name specified, use the GUI to find a new one
        catch [Exception]
        {
            Write-Output "[Oops] Couldn't find an OU that matched $OU so I made you pick again"
            return $(Select-GUIOU).DistinguishedName
        }
    }
}

###########################END OF FUNCTIONS###########################
#endregion



#validate the OU is set to something valid, communicate valid OU to user
$OU = Get-OU $OU
Write-Output "Selected OU: $OU"

#don't need to validate Count because the param block that leads this script will throw an error if Count isn't an integer... 
#... assuming users are smart enough to enter a positive number (for loop below will throw an index error and nothing bad should happen)
Write-Output "Selected Count: $Count"

#create array of all upper and lowercase letters (char code representative)
$Upper = (65..90)
$Lower = (97..122)

#create an ID for this batch of created users
$ID = (Get-Date).Ticks

#create $count many users
$null = for ($i = 0; $i -lt $Count; $i++)
{
    #make a random first name, first initial capitalized
    $Initial = Get-Random -InputObject $Upper -Count 1 | % { [char]$_ }
    $RestOfname = Get-Random -InputObject $Lower -Count 4 | % { [char]$_ }
    $FirstName = $Initial + $RestOfName -replace ' ',''
    
    #make a random last name, first initial capitalized
    $Initial = Get-Random -InputObject $Upper -Count 1 | % { [char]$_ }
    $RestOfname = Get-Random -InputObject $Lower -Count 4 | % { [char]$_ }
    $LastName = $Initial + $RestOfName -replace ' ',''

    #craft the displayname, name, samaccountname, UPN attributes
    #in the future, this will detect name collisions and mitigate
    $DisplayName = "$FirstName $LastName"
    $Name = $DisplayName
    $SamAccountName = "$($FirstName[0])$LastName"           #first initial last name, IE: Thomas Rayner becomes TRayner
    $UPN = $SamAccountName + '@' + (Get-ADDomain).DNSRoot   #UPN suffix won't always be the value of (Get-ADDomain).DNSRoot but it usually is... this is why you read scripts before running them

    #assign the password
    $AccountPassword = ConvertTo-SecureString -AsPlainText $Password -Force

    #create description that can be used to group users created in different batches
    $Description = "Created by MVP Tool: New-RandomADUsers.ps1. Batch: $ID"

    #announce the creation of a user
    Write-Output "Creating $Name. Username: $SamAccountName"

    #add all the params to the user list
    $UserParams = @{}
    $UserParams.Add('GivenName',$FirstName)
    $UserParams.Add('Surname',$LastName)
    $UserParams.Add('DisplayName',$DisplayName)
    $UserParams.Add('Name',$Name)
    $UserParams.Add('SamAccountName',$SamAccountName)
    $UserParams.Add('AccountPassword',$AccountPassword)
    $UserParams.Add('Description',$Description)
    $UserParams.Add('Path',$OU)                           #put them all in the OU we created
    $UserParams.Add('Enabled',$True)                      #enable the account

    #create the AD user
    New-ADUser @UserParams
}

#list the users created, verify they can be found in AD
$CreatedUsers = (Get-ADUser -SearchBase $OU -Filter "Description -like '*$ID*'").SamAccountName
Write-Output 'Created following users'
$CreatedUsers</pre>

&nbsp;
