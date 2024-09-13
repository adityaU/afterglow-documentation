# Getting Started With Afterglow

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
