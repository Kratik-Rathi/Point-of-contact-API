 Point of Contact API - Detailed Workflow
 ![image](https://github.com/user-attachments/assets/cf22cb2a-85fb-4ef9-8182-d1796af52e8b)
**Introduction**
The Point of Contact (PoC) API is designed to streamline internal collaboration at SC 1701-D by providing quick access to relevant contact information. In an expanding organization, efficiently identifying individuals involved in specific products or repositories becomes crucial. This API offers a solution by querying employee data to return pertinent contact details, facilitating smoother communication across distributed teams.
**Use Case**
Consider Veena, an employee at SC 1701-D, tasked with collaborating on the SecurityScanAPI project. Since the involved team operates remotely, Veena requires assistance in locating the correct contact. The PoC API allows her to perform a query using the product name (SecurityScanAPI) or repository name (SecurityRepo), yielding detailed contact information that enhances productivity and team integration.
**Data Management & Preprocessing:**
The API leverages a dataset generated via Mockaroo and includes fields such as EmpID, FirstName, LastName, ADEmail, LocationCode, Title, ChatUserName, etc. Preprocessing steps include:
•	**Title Optimization:** Standardized to 20 distinct roles (e.g., Software Engineer, DevOps Engineer).
•	**Product and Repository Assignment:** Random allocation of employees to one of 20 products (e.g., SecurityScanAPI) and repositories (e.g., SecurityRepo).
•	**Consistent Column Naming:** Standardization (e.g., ADEmail → EmailID).
•	**Filtered Subsets:** Tailored subsets for efficient query handling.
**API Design and Core Features**
•	Query Inputs: Product Name or Repository Name along with sql query 
                         (eg: EXECUTE FindPOC @ProductName = 'securityscanapi' )
		         (eg: EXECUTE FindPOC @RepositoryName = 'securityrepo' )
•	**Response:**
o	Returns First Name, Last Name, Email ID, Chat User Name, Region, City, Title.
•	**Error Handling:**
o	Checks on each point of API (e.g. database connection, email sent or not, SQL procedure executed or not, dataframe created or not)
        **Workflow Overview**
1.	**Query Processing:**
o	Users input either a product name or repository name.
o	The API connects to an SQL Server database via secure credentials.
o	Stored procedure (e.g., EXECUTE FindPOC) retrieve matching contact data.
2.	**Data Transformation:**
o	Results are transformed into a Pandas DataFrame for standardized formatting.
o	Data is exported to an Excel file.
3.	**Email Notification:**
o	An automated email, including the Excel report as an attachment, is dispatched to relevant stakeholders.
**Technical Stack**
•	Backend Framework: Built using Flask, a lightweight Python framework managing HTTP GET requests.
•	Database: SQL Server facilitates secure, high-performance querying and data storage.
•	Containerization: The API is Dockerized for scalability and seamless deployment, enabling scheduled jobs and log monitoring via cron.
•	Automated Communication: Email notifications ensure timely distribution of contact data.
**Example Workflow**
1.	Sample Input: User queries using:
o	Product Name: SecurityScanAPI
o	Repository Name: SecurityRepo
2.	**Processing:**
o	Executes FindPOC stored procedure.
o	Formats retrieved data into an Excel file.
o	Sends an email with the file attached to relevant team members.
3.	**Output:**
o	Provides a JSON response whether API run is successful or there was an error.
**Future Enhancements**
•	Performance: On a larger database “Temporary Tables” can be used to query through procedure.
•	Analytics: Monitor API usage using Prometheus library when API is hosted on a company server, to monitor it’s data usage and how much load it is making on the server.
