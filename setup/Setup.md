 
# Setup steps
- Create Azure account and open Azure portal
- Create Resource group in Azure
- Create Virtual Netwrok in Azure under the resource group
- Create a Virtual Machine (Windows)
- Configure NSG to allow all inbound traffic
- Disable Windows Firewall
- Generate security logs with incorrect credentials
- Create Log Analytics Workspace for central log repo
- Connect the created workspace to Microsoft Sentinal
- Enable “Windows Security Events via AMA” data connector
- Create DCR for windows security logs
- Query logs in Workspace using KQL
- Create a Microsoft Sentinel Watchlist by importing the GeoIP CSV file
- Create a new Microsoft Sentinel Workbook to visualize attack data
- Create a custom query-based visualization using the Advanced Editor with custom JSON configuration
- Successfully visualized a global map, demonstrating live threat activity against the Windows VM
