# Installation Guide for Afterglow

Afterglow is a powerful platform that enables seamless data accessibility across your organization while offering robust management features. By installing Afterglow on your own servers, you maintain full control over your data, ensuring security and compliance with your organizational policies.

The installation process leverages Docker, a containerization platform that simplifies application deployment. With Docker, you can have Afterglow up and running in as little as 15 minutes.

---

## Prerequisites

Before you begin the installation process, ensure you have the following:

- **A Machine or Server**: This can be your local computer for testing or a dedicated server for production.
- **Administrative Access**: You'll need the ability to install software and modify system settings.
- **Internet Connection**: Required for downloading software and Docker images.
- **Domain Name (for Production)**: Necessary if you're setting up Afterglow in a production environment with a custom sub-domain.

---

## Setting Up Afterglow on a Local Machine

If you want to test Afterglow on your personal laptop or desktop, follow these steps.

### Step 1: Install PostgreSQL

Afterglow requires a PostgreSQL database to store data.

1. **Download PostgreSQL**:

   - Visit the [official PostgreSQL website](https://www.postgresql.org/download/) and download the installer for your operating system.

2. **Install PostgreSQL**:

   - Run the installer and follow the on-screen instructions.
   - Note down the username (usually `postgres`) and password you set during installation.

3. **Create a Database**:

   - Open the PostgreSQL command-line tool (`psql`) or use a graphical tool like pgAdmin.
   - Execute the following command to create a new database named `afterglow`:

     ```sql
     CREATE DATABASE afterglow;
     ```

### Step 2: Download Afterglow

1. **Find the Latest Version**:

   - Visit the [Afterglow Releases page](https://github.com/AfterglowPlatform/afterglow/releases) to find the latest version.

2. **Note the Version Number**:
   - You'll need the version number (e.g., `v1.2.3`) for the Docker command.

### Step 3: Install Docker

1. **Download Docker**:

   - Go to the [Docker Desktop website](https://www.docker.com/products/docker-desktop) and download the installer for your operating system.

2. **Install Docker**:
   - Run the installer and follow the setup instructions.
   - Ensure Docker is running before proceeding.

### Step 4: Run the Docker Container

1. **Open a Terminal or Command Prompt**:

   - Navigate to where you want to run the Docker container.

2. **Run the Following Command**:

   ```bash
   docker run -it -p 4200:80 \
   -e DATABASE_URL=postgres://<username>:<password>@host.docker.internal:5432/afterglow \
   adityau/afterglow:<latest-version>
   ```

   - Replace `username` with your PostgreSQL username.
   - Replace `password` with your PostgreSQL password.
   - Replace `latest-version` with the Afterglow version number you noted earlier.

   - **Explanation of Command Flags**

     - **-it:** Runs the container in interactive mode with a TTY.
     - **-p 4200:80:** Maps port 80 inside the container to port 4200 on your local machine.
     - **-e:** Sets environment variables inside the container.
     - **DATABASE_URL:** The connection string for your PostgreSQL database.

3. **Wait for the Container to Initialize:**
   The first run may take a few minutes as Docker downloads the Afterglow image.

### Step 5: Access Afterglow

- **Open Your Web Browser:**

  - Navigate to <http://localhost:4200>.

- **Log In with Default Credentials:**

  - Username: `admin@example.com`
  - Password: `ag_admin_password`

- **Explore Afterglow:**
  - You can now explore Afterglow's features and functionalities on your local machine.

---

## Running Afterglow in Production

For a production environment, additional configurations are necessary to ensure security and accessibility.

### Step 1: Set Up a Sub-Domain

- **Choose a Sub-Domain:**

  - Decide on a sub-domain like afterglow.your-domain.com.

- **Configure DNS Settings:**
  - **Access Your DNS Provider:**
    - Log in to the service where your domain is registered (e.g., GoDaddy, Namecheap).
  - **Create an A Record:**
    - Point afterglow.your-domain.com to the IP address of your server where Afterglow will be hosted.
  - **Allow for Propagation:**
    - DNS changes can take up to 24 hours to propagate, but usually, it's much quicker.

### Step 2: Obtain Google OAuth Credentials

Afterglow uses Google authentication for secure user access. Alternatively, you can use SAML-based authentication as well.

- **Go to Google API Console:**

  - Navigate to the [Google API Console](https://console.cloud.google.com/).

- **Create a New Project:**

  - Click on the **Select a project** dropdown and choose **New Project**.
  - Provide a name and click **Create**.

- **Enable OAuth Consent Screen:**

  - Navigate to **OAuth Consent Screen**:
    - From the left menu, select **OAuth consent screen**.
    - Choose **External** for user type.
    - Fill in the necessary details like **App name**, **User support email**, and **Developer contact information**.
    - Click **Save and Continue**.

- **Create OAuth Client ID:**
  - Select **Credentials**:
    - From the left menu, click on **Credentials**.
    - Click on **Create Credentials** and choose **OAuth client ID**.
    - Select **Web application** as the application type.
    - Under **Authorized redirect URIs**, add:

      ```
      http(s)://afterglow.your-domain.com/api/google/callback
      ```

      Replace `afterglow.your-domain.com` with your actual sub-domain.
    - Click **Create** and download the JSON file containing your Client ID and Client Secret.

### Step 3: Run the Docker Container with Production Settings

- **Ensure Docker is Installed on Your Server:**

  - If not, install Docker by following the instructions for your server's operating system.

- **Run the Following Command:**

  ```bash
  docker run -itd -p 80:80 \
  -e DATABASE_URL=postgres://<postgres_username>:<postgres_password>@<postgres_host>:<postgres_port>/afterglow \
  -e AG_APP_ROOT=http://<your_afterglow_subdomain>/ \
  -e AG_GOOGLE_CLIENT_ID=<google_client_id> \
  -e AG_GOOGLE_CLIENT_SECRET=<google_client_secret> \
  -e AG_ADMIN_EMAIL=<desired_admin_email> \
  adityau/afterglow:<latest-afterglow-version>
  ```

  Replace the placeholders with your actual values:
  - `<postgres_username>`: Your PostgreSQL username.
  - `<postgres_password>`: Your PostgreSQL password.
  - `<postgres_host>`: The hostname or IP address of your PostgreSQL server (use `localhost` if on the same machine).
  - `<postgres_port>`: The port number PostgreSQL is listening on (default is 5432).
  - `<your_afterglow_subdomain>`: Your Afterglow sub-domain (e.g., `afterglow.your-domain.com`).
  - `<google_client_id>`: The Client ID from the JSON file you downloaded.
  - `<google_client_secret>`: The Client Secret from the JSON file you downloaded.
  - `<desired_admin_email>`: The email you want to use for the admin account (must be a Google account).
  - `<latest-afterglow-version>`: The version number of Afterglow.

### Explanation of Command Flags

- `-itd`: Runs the container in detached mode (in the background).
- `-p 80:80`: Maps port 80 inside the container to port 80 on your server.
- `-e`: Sets environment variables inside the container.
  - `AG_APP_ROOT`: The base URL where Afterglow is accessible.
  - `AG_GOOGLE_CLIENT_ID` and `AG_GOOGLE_CLIENT_SECRET`: For Google OAuth authentication.
  - `AG_ADMIN_EMAIL`: Sets up the admin account email.

### Step 4: Verify the Container is Running

- Run `docker ps` to see active Docker containers.
- Ensure your Afterglow container is listed.

### Step 5: Access and Configure Afterglow

- **Open Your Web Browser:**

  - Navigate to `http(s)://afterglow.your-domain.com`.

- **Log In Using Google Authentication:**
  - Click on **Sign in with Google**.
  - Use the admin email address you specified (`<desired_admin_email>`).

---

## Post-Installation Steps

### Deactivate Default Credentials

For security reasons, it's crucial to disable the default user accounts.

#### Navigate to User Settings

1. Click on **Settings** in the Afterglow dashboard.
2. Select **Users** from the settings menu.

#### Deactivate Default Users

1. Locate `admin@example.com` and `viewer@example.com`.
2. Click on each user and select **Deactivate Account**.

#### Confirm Deactivation

- Ensure these accounts are marked as inactive.

### Create Your Organization

#### Access Organization Settings

1. In the Afterglow dashboard, go to **Organizations**.

#### Create a New Organization

1. Click on **Create Organization**.
2. Fill in your organization's details, such as name and domain.

#### Set Up Email Domain Restrictions

- Configure the organization to restrict access to users with your company's email domain.
- This ensures data is only accessible to authorized personnel within your organization.

#### Invite Team Members

1. Send invitations to your team members to join Afterglow.
2. They will receive an email with instructions to create their accounts.

---

### Additional Considerations

#### SSL/TLS Configuration

- For secure communication, especially in production, set up SSL/TLS certificates.
- You can use services like Let's Encrypt to obtain free SSL certificates.

#### Firewall Settings

- Ensure that your server's firewall allows incoming connections on the necessary ports (e.g., port 80 for HTTP, port 443 for HTTPS).

#### Regular Backups

- Implement a backup strategy for your PostgreSQL database to prevent data loss.
- Regularly export your database and store backups securely.

#### Monitoring and Logging

- Monitor your Afterglow instance using tools like Prometheus or Grafana.
- Check Docker logs regularly for any errors or warnings.

#### Scaling and High Availability

- For larger organizations, consider load balancing and clustering strategies.
- Use container orchestration platforms like Kubernetes for managing multiple instances.

#### Security Best Practices

- Keep your software and dependencies up to date.
- Regularly review user permissions and access levels.

---

By following this detailed guide, you should have Afterglow installed and operational, tailored to your specific environment—whether for testing on a local machine or running in a production setting. With Afterglow, you can efficiently manage and share data within your organization, all while maintaining high standards of security and control.

If you encounter any issues during installation or have further questions, consider reaching out to `support@getafterglow.co`
