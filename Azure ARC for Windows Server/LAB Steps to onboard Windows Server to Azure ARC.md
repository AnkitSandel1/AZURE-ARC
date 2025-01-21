# Step-by-step guide for onboarding a Windows Server to Azure Arc:  

1. **Install Azure CLI**:

  -- Install Azure CLI using Powershell Command --
  
       $ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; Remove-Item .\AzureCLI.msi
  --  validate the installation using the command 
        `az version`.
   
2. **Install Azure Connected Machine Agent**:

   Download and install the agent from [this link](https://download.microsoft.com/download/1/9/f/19f44dde-2c34-4676-80d7-9fa5fc44d2a8/AzureConnectedMachineAgent.msi).
   Verify the installation in the Application Wizard -- Appwiz.cpl
   ![image](https://github.com/user-attachments/assets/21c5e9d3-ef81-4426-b06e-a13e5d7e8bdc)

The installation process creates the following folders during setup.
![image](https://github.com/user-attachments/assets/1236143c-385a-4b8d-b6a4-ae720ecd0fcf)

4. **Install Azure Arc Module**:
   Run below command to install the Azure Arc module.
     `Install-Module -Name Az.ConnectedMachine`   

5. **Login to Azure**:
   Use `Connect-AzAccount` to log in and check the selected subscription.
   Change the subscription, if needed, with `Set-AzContext -Subscription "subscription-id"`.
   ![image](https://github.com/user-attachments/assets/4369097b-6685-44e8-a1fc-50292bf8abcc)
 

7. **Onboard Server to Azure Arc**:
   Use the following command to onboard the server:

       Connect-AzConnectedMachine -ResourceGroupName <ResourceGroupName> -Name <ServerName> -Location <Location>
  

8. **Verify Success**:
   Check the PowerShell output for success or troubleshoot errors.
   ![image](https://github.com/user-attachments/assets/3744d083-c7be-4c61-aaab-5fdee8a8b499)


10. **Validate on Azure Portal**:
    Go to the Azure Arc section in the portal to verify the server is listed under Windows Server.
    ![image](https://github.com/user-attachments/assets/cf799e02-15ae-4732-b030-9494a1415ec5)


12. **Check Service Status**: Ensure the following services are running:  
   - **HIMDS**: For the hybrid instance.  
   - **GCArcService**: For Windows Guest OS.
     
Installing the agent creates the following Windows services on the target machine.
![image](https://github.com/user-attachments/assets/a43724d9-4fc9-4672-b09d-9d951e347dd5)

