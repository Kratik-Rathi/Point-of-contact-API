# Point of Contact (PoC) API

## Introduction

The Point of Contact (PoC) API is designed to streamline internal collaboration by providing quick access to relevant contact information. It enables users to query employee data and retrieve details such as names, email addresses, etc. This API helps fostering better communication across distributed teams.

## Features

- **Query Inputs**: 
  - Product Name (e.g., `SecurityScanAPI`) or Repository Name (e.g., `SecurityRepo`)
  
- **Query Execution**:
  - Example:  
    `EXECUTE FindPOC @ProductName = 'SecurityScanAPI'`  OR `EXECUTE FindPOC @RepositoryName = 'SecurityRepo'`

- **Response**: 
  - Returns relevant details like:
    - First Name, Last Name, Email ID, Chat Username, Region, City, Title

- **Error Handling**: 
  - Ensures robust operation by validating database connections, query execution, and email dispatch.

## Workflow

1. **Query Processing**:
   - Users input a product or repository name along with api url.
   - The API connects to an SQL Server and retrieves matching data using stored procedure.

2. **Data Transformation**:
   - Query results are formatted into a Pandas DataFrame.
   - An Excel report is generated from the data.

3. **Email Notification**:
   - The Excel report is automatically emailed to receiver provided in the API script.

## Technical Stack

- **Backend Framework**: Flask
- **Database**: SQL Server
- **Containerization**: Docker (supports scalability and cron job scheduling)
- **Automated Communication**: Email integration for report sharing

## Example Workflow

1. User inputs:
   - Product Name: `SecurityScanAPI`(http://127.0.0.1:5000/api/poc?product_name=securityscanapi) OR Repository Name: `SecurityRepo` (eg: http://127.0.0.1:5000/api/poc?repository_name=securityrepo) [It is not case sensitive]
     Note: http://127.0.0.1:5000 is localhost ip, you ip may differ if using a server 
2. API processes the query:
   - Executes the `FindPOC` stored procedure.
   - Formats the data into an Excel file.
   - Sends an email with the report attached.

3. Output:
   - JSON response indicating success or failure of the operation.

---

## Setup Instructions for SQL Server set-up

### Installing and Configuring SQL Server

1. **Download and Install SQL Server**:
   - Download SQL Server from the [official Microsoft website](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
   - Follow the installation steps and choose the **Developer** or **Express** edition for local development.

2. **Install SQL Server Management Studio (SSMS)**:
   - Download SSMS from [here](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
   - Use SSMS to connect to your SQL Server instance and manage databases.

3. **Create a Database**:
   - Open SSMS and connect to your SQL Server.
   - Right-click on **Databases** → **New Database** → Provide a name and click **OK**.

4. **Setup Stored Procedure**:
   - You can make your own stored procedure refering to sql **server data fetch procedure.txt** file but remember to change ALTER to CREATE as ALTER is to change already exisiting procedure

### Enabling Remote Connections

1. **Enable SQL Server for Remote Connections**:
   - Open **SQL Server Configuration Manager**.
   - Navigate to **SQL Server Network Configuration** → **Protocols for [Instance Name]**.
   - Enable **TCP/IP**.

2. **Configure TCP/IP Port**:
   - Double-click **TCP/IP**, go to the **IP Addresses** tab.
   - Set the **TCP Port** under **IPAll** (e.g., 1433).

3. **Allow SQL Server in Windows Firewall**:
   - Open **Windows Firewall**.
   - Add **Inbound Rule** for SQL Server:
     - Port: 1433
     - Protocol: TCP

4. **Enable SQL Server Authentication**:
   - Open SSMS and connect to your server.
   - Right-click on the server name → **Properties** → **Security**.
   - Enable **SQL Server and Windows Authentication Mode**.
   
5. **Create a SQL Server Login for Remote Use**:
   - In SSMS, navigate to **Security** → **Logins** → **New Login**.
   - Create a login and assign appropriate roles.

6. **Test the Remote Connection**:
   - From another machine, open SSMS and try connecting using:
     - **Server Name**: `[Your_IP_Address]\[InstanceName]` or `[Your_IP_Address],1433`
     - **Authentication**: SQL Server Authentication
     - **Username/Password**: Use the login you created.

---

## Future Enhancements

- **Performance Optimization**: Utilize temporary tables for large databases.
- **Analytics**: Implement Prometheus for API usage and server load monitoring.

## License

This project is licensed under the [MIT License](LICENSE).
