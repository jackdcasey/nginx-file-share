# Summary

This project will spin up a Nginx webserver used to share files easily

The configuration includes HTTPS and basic-auth

# Setup

## Create Directories

Clone this repository, create the following directories:
- certs
- private
- public

## Create or Add Certificates

If you have certificates available, please place them in the certs directory, named:
- cert.pem
- key.pem

To generate a self signed certificate, run the following:

```
openssl req -x509 -nodes -newkey rsa:2048 -keyout ./certs/key.pem -out ./certs/cert.pem -days 365
```

## Create Users

We'll need to create a user to use basic authentication. Run the following command, replacing *username* and *password*

```
htpasswd -nb username password >> ./private/htpasswd
```

Run this for each user you want to create

## Upload Files

Upload any files you want to share to the ./public directory

## Start Server

Start the server with:

```
docker-compose up -d
```

## Networking (optional)

If running this behind NAT, you will need to forward port 4433 to the IP address of the server

# Downloading

## Browser

To see the files available, open https://<servername>:4433/

If using self-signed certs, you may see a trust error

## Command Line

Files can also be downloaded through `curl` or similar. For example:

```
curl --user username:password https://localhost:4433/somefile.zip -k -O
```

Note, the `-k` option is only required if using untrusted certificates
