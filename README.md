Start Azure Virtual Machine using Azure Automation Runbook
==========================================================

            

 

Demonstrates starting all Microsoft Azure Virtual Machine in a specific Azure subscription by starting with the Microsoft Active Directory
 Domain Controllers. The script could be associated with the new Azure Automation Scheduler to start the Virtual Machines at specific time of the day. 

You have to define an Azure Connection and Azure Certificate under Azure Automation Assets. You should also change the references
 within the script to point to the correct Asset names. 


 ![Image](https://github.com/azureautomation/start-azure-virtual-machine-using-azure-automation-runbook/raw/master/startvm.png)


 



PowerShell Workflow
Edit|Remove
powershellworkflow
<#

.DESCRIPTION


.NOTES
	Author: Peter Selch Dahl - Installers A/S
	Last Updated: 4/14/2014  
#>

workflow Start_My_Azure_VMs
{   
      param()

       $MyConnection = 'My MSDN Azure Account Connection'
       $MyCert = 'MSDN Azure Certifcate'


    # Get the Azure Automation Connection
    $Con = Get-AutomationConnection -Name $MyConnection
    if ($Con -eq $null)
    {
        Write-Output 'Connection entered: $MyConnection does not exist in the automation service. Please create one `n'   
    }
    else
    {
        $SubscriptionID = $Con.SubscriptionID
        $ManagementCertificate = $Con.AutomationCertificateName
       
    }   

    # Get Certificate & print out its properties
    $Cert = Get-AutomationCertificate -Name $MyCert
    if ($Cert -eq $null)
    {
        Write-Output 'Certificate entered: $MyCert does not exist in the automation service. Please create one `n'   
    }
    else
    {
        $Thumbprint = $Cert.Thumbprint
    }

        #Set and Select the Azure Subscription
         Set-AzureSubscription `
            -SubscriptionName 'My Azure Subscription' `
            -Certificate $Cert `
            -SubscriptionId $SubscriptionID `

        #Select Azure Subscription
         Select-AzureSubscription `
            -SubscriptionName 'My Azure Subscription'

#Code Snippet - Click Download to get the script

<#

.DESCRIPTION


.NOTES
	Author: Peter Selch Dahl - Installers A/S
	Last Updated: 4/14/2014  
#>

workflow Start_My_Azure_VMs
{   
      param()

       $MyConnection = 'My MSDN Azure Account Connection'
       $MyCert = 'MSDN Azure Certifcate'


    # Get the Azure Automation Connection
    $Con = Get-AutomationConnection -Name $MyConnection
    if ($Con -eq $null)
    {
        Write-Output 'Connection entered: $MyConnection does not exist in the automation service. Please create one `n'   
    }
    else
    {
        $SubscriptionID = $Con.SubscriptionID
        $ManagementCertificate = $Con.AutomationCertificateName
       
    }   

    # Get Certificate & print out its properties
    $Cert = Get-AutomationCertificate -Name $MyCert
    if ($Cert -eq $null)
    {
        Write-Output 'Certificate entered: $MyCert does not exist in the automation service. Please create one `n'   
    }
    else
    {
        $Thumbprint = $Cert.Thumbprint
    }

        #Set and Select the Azure Subscription
         Set-AzureSubscription `
            -SubscriptionName 'My Azure Subscription' `
            -Certificate $Cert `
            -SubscriptionId $SubscriptionID `

        #Select Azure Subscription
         Select-AzureSubscription `
            -SubscriptionName 'My Azure Subscription'

#Code Snippet - Click Download to get the script




        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
