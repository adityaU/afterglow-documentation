# Installation

Afterglow empowers you to make data accessible across your organization, all while providing robust management features. Installing Afterglow on your own servers ensures you maintain full control over your data.

The setup for Afterglow utilizes Docker, allowing you to be operational in as little as 15 minutes.

## Setting up Afterglow

### Testing on Local Machine

If you are trying to test out Afterglow on your personal laptop, then please follow the instructions below:

- Install PostgreSQL and initialize a database named `afterglow`.
- Pick the latest version of Afterglow from [here](https://hub.docker.com/r/adityau/afterglow/tags).
- Install Docker on your local computer and execute the subsequent command:

```bash
docker run -it -p 4200:80 -e DATABASE_URL=postgres://<username>:<password>@host.docker.internal:5432/afterglow  adityau/afterglow:<latest-version>
```

- You should be able to access Afterglow at [http://localhost:4200](http://localhost:4200).
  Log in using the credentials below:

```
username: admin@example.com
password: ag_admin_password
```

### Running in Production

To complement the initial setup steps, you’ll also need to configure Google authentication and generate a sub-domain for Afterglow.

- Generate a sub-domain in the format of `afterglow.\<your-domain\>`. Direct this sub-domain to the machine where Afterglow is hosted.
- Obtain Google credentials from this link. Download your client ID and client secret, and set the redirection URL to `http(s)://afterglow.\<your-domain\>/api/google/callback`
- On the machine where Afterglow is hosted, execute the following Docker command:

```bash
docker run -itd -p 80:80 -e DATABASE_URL=postgres://<postgres_username>:<postgres_password>@<postgres_host>:<postgres_port>/afterglow -e AG_APP_ROOT=http://<your_afterglow_sub-domain>/ -e AG_GOOGLE_CLIENT_ID=<google_client_id> -e AG_GOOGLE_CLIENT_SECRET=<google_client_secret> -e AG_ADMIN_EMAIL=<desired_admin_email>  adityau/afterglow:<latest-afterglow-version>
```

- You should then be able to access Afterglow at `http(s)://<your-afterglow-subdomain>`
- You can log in using the admin email you specified during the above setup, via Google Login.
- Remember to deactivate the default credentials for <admin@example.com> and <viewer@example.com>. You can accomplish this by navigating to Settings > Users and then deactivating the user accounts.
- Create your organization (link) to make sure your data is never shared outside your organizations emails
