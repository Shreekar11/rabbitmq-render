# 🐇 RabbitMQ on Render

This repo sets up a self-hosted RabbitMQ server on [Render](https://render.com/) using Docker to use as a message broker across multiple applications.

##  Deploying

1. Fork this repo to your GitHub account.
2. Go to [Render Dashboard](https://dashboard.render.com/).
3. Click "New +" → "Private Service".
4. Connect your repo and Render will auto-detect the `Dockerfile`.
5. Set the exposed port to `5672` and optionally `15672`.
6. Attach a **Persistent Disk** with mount path `/var/lib/rabbitmq` if you want queues to persist restarts.

## Default Credentials

- Username: `guest` (change via env var)
- Password: `guest` (change via env var)

> **Change these in production!**
> Set `RABBITMQ_DEFAULT_USER` and `RABBITMQ_DEFAULT_PASS` in your `render.yaml` or Render dashboard to override the defaults.

## Setting Custom Credentials

In your `render.yaml`:

```yaml
    envVars:
      - key: RABBITMQ_DEFAULT_USER
        value: yourusername
      - key: RABBITMQ_DEFAULT_PASS
        value: yourpassword
```

## Connecting from Other Render Services

If your app is hosted on Render too, use:

`amqp://guest:guest@rabbitmq:5672`


## Accessing Management UI

Enable port `15672` to access the RabbitMQ Management UI.

If this is a private service, the UI is only accessible from other Render services (or via SSH tunnel).
