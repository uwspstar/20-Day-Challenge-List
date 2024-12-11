**Note:** Starting with Visual Studio 2017 and continuing in Visual Studio 2022, SSDT is no longer a separate standalone install for most BI projects. Instead, SSDT’s core functionality (for SSIS, SSRS, SSAS) is integrated into the Visual Studio environment through extensions or the workloads installed via the Visual Studio Installer.

### Steps to Use SSDT in Visual Studio 2022

1. **Install or Modify Visual Studio 2022 with Data-Related Workloads**  
   - Open the **Visual Studio Installer** (you can find it in the Windows Start menu or by searching “Visual Studio Installer”).  
   - Click **Modify** next to your Visual Studio 2022 installation.
   - In the Workloads tab, check:
     - **Data storage and processing** (this workload includes SQL Server Data Tools).
   - Click **Modify** to apply the changes. Visual Studio Installer will download and install the needed components.
   
2. **Install BI Templates via Extensions (If Needed)**  
   For SSIS, SSRS, and SSAS projects, you may need to install additional extensions:
   - Open **Visual Studio 2022**.
   - Go to **Extensions > Manage Extensions** in the main menu.
   - In the **Online** tab, search for:
     - “**SQL Server Integration Services Projects**” for SSIS
     - “**Microsoft Reporting Services Projects**” for SSRS
     - “**Microsoft Analysis Services Projects**” for SSAS
   - Download and install the required extensions. Visual Studio may prompt you to close and reopen to complete the installation.

3. **Create a New BI Project in Visual Studio 2022**  
   - Open **Visual Studio 2022**.
   - Click **Create a new project** on the start page (or go to **File > New > Project…**).
   - In the “Create a new project” dialog, type what you’re looking for:
     - For SSIS: search “Integration Services” or “SSIS”
     - For SSRS: search “Reporting Services” or “SSRS”
     - For SSAS: search “Analysis Services” or “SSAS”
   - Select the appropriate project template (e.g., **Integration Services Project** for SSIS).
   - Click **Next** to configure project name, location, and then **Create**.

4. **Use SSDT Features in Project**  
   - Once the project opens, you will see SSDT-specific designers:
     - **SSIS**: Data Flow Task, Control Flow, variables, parameters, and so forth.
     - **SSRS**: Report Designer, datasets, data sources.
     - **SSAS**: Cube or Tabular model designers.
   - You can now develop, debug, and deploy your BI solutions directly from Visual Studio 2022.

5. **Deploying and Running Projects**  
   - For SSIS, you can build and deploy packages to the SSIS Catalog or run them directly in Visual Studio.
   - For SSRS, you can create reports and deploy them to the report server.
   - For SSAS, you can develop and deploy cubes or tabular models to an Analysis Services instance.

**Summary**:  
- Visual Studio 2022 integrates SSDT functionalities through built-in workloads and separate extensions.  
- Install the “Data storage and processing” workload via the Visual Studio Installer.  
- Use the Extensions Marketplace to add SSIS, SSRS, and SSAS project templates.  
- Create and manage your BI projects directly within Visual Studio 2022, just as you did with previous SSDT versions.
