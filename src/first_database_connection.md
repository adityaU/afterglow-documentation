# Setting Up Your First Database Connection in Afterglow

Now that Afterglow is up and running, you can set up your first database connection to begin querying and analyzing your data.

---

## Supported Databases

Afterglow supports a variety of SQL and NoSQL databases, including:

- **Amazon Redshift**
- **MySQL**
- **PostgreSQL**
- **InfluxDB**
- **Redis**
- **ClickHouse**

---

## Configuring a Database

To configure a database in Afterglow, follow these steps:

### Step 1: Access the Settings Page

1. **Log in to Afterglow**:

   - Open your web browser and navigate to your Afterglow instance.
   - Log in using your credentials.

2. **Navigate to Settings**:
   - Click on your **Username** or **Profile Icon** located in the sidebar or the top-right corner.
   - Select **Settings** from the dropdown menu.

### Step 2: Add a New Database

1. **Access the Databases Tab**:

   - In the Settings page, ensure you're on the **Databases** tab. This is usually the default tab upon entering the Settings page.

2. **Add New Database**:
   - Click on the **Add New Database** button, located at the top-right corner of the Databases section.

### Step 3: Configure Database Connection Details

You will be presented with a form to enter your database connection details. Fill in the following fields:

1. **Database Type**:

   - Select your database type from the dropdown menu (e.g., **PostgreSQL**, **MySQL**, **Redshift**, etc.).

2. **Name**:

   - Provide a friendly name for your database connection. This name will be used within Afterglow to reference this database.

3. **Host URL**:

   - Enter the hostname or IP address of your database server (e.g., `db.example.com` or `192.168.1.100`).

4. **Host Port**:

   - Specify the port number your database is listening on (default ports are typically `5432` for PostgreSQL, `3306` for MySQL, etc.).

5. **Database Name**:

   - Input the name of the specific database you want to connect to on your database server.

6. **Database Username**:

   - Enter the username that Afterglow will use to authenticate with your database.

7. **Database Password**:

   - Provide the password associated with the above username.

8. **Connection Pool Size**:

   - Set the maximum number of database connections that Afterglow can open simultaneously. This helps manage resources efficiently.
   - **Example**: `10`

9. **Connection Checkout Timeout (in seconds)**:

   - Define how long Afterglow should wait when attempting to obtain a connection from the pool before timing out.
   - **Example**: `30`

10. **Query Timeout (in seconds)**:
    - Specify the maximum duration a query is allowed to run before it is terminated.
    - **Example**: `60`

### Step 4: Save the Configuration

1. **Review the Information**:

   - Double-check all the fields to ensure the information is accurate.

2. **Save the Database Configuration**:
   - Click on the **Save** or **Add Database** button to store the configuration.

### Step 5: Verify the Database Connection

1. **Check the Database List**:

   - After saving, you should see your new database listed in the Databases tab.

2. **Check if tables are synced:**

- Click on database references tab on sidebar.
- click on your database that you recently added, you should see all the tables listed in the database.

2. **Attempt a Simple Query**:

   - Navigate to the **New Questions** on sidebar.
   - Select your newly added database from the list.
   - Run a simple query to ensure everything is functioning properly.

   ```sql
   SELECT 1;
   ```

   - If the query executes successfully, your database connection is properly configured.

## Additional Tips

### Secure Credentials

- **Database Permissions:**
  - Ensure that the database username and password you use have the appropriate permissions and adhere to your organization's security policies.

### Network Connectivity

- **Server Access:**
  - Make sure that the server running Afterglow can reach your database server over the network. This may involve configuring firewall rules or VPN connections.

### Error Handling

- **Troubleshooting:**
  - If you encounter errors when connecting, check the error messages provided by Afterglow. Common issues include incorrect credentials, network connectivity problems, or firewall restrictions.

---

### Need Help?

If you're encountering issues that you can't resolve, consider reaching out to `support@getafterglow.co` for assistance.
