# The fly.io Server-App (frp hosted on fly.io)

### Be aware of this
You need a ip6 capable network at the location where the frpc-tunnel-client will be. Because frpc needs to connect to this frps-server via it's ip6 address! This is because fly's shared ip4's cannot handle non-tcp connections (took me a while to figure that out). The end-users can happily use the ip4, because they will be served TCP.

## Instructions

Sign up to a fly.io account

Install fly utility (read on fly.io)

Clone the repo (and cd into)

Create the app: 

```
fly launch --copy-config --no-deploy
```
..and answer questions:

- App name?
- The Region closest to you?

Assign ip-Addresses to the app:
```
fly ips allocate-v4 --shared
fly ips allocate-v6
```

Now choose a Auth-Token for the future frpc-client:
```
fly secrets set FRP_TOKEN=MySuperSecretToken
```

Deploy to fly.io:
```
fly deploy --remote-only
```

Scale back to 1 Machine (he free tier has very limited resources):
```
fly scale count 1
```

Create an **A Record** for your domain (use the ip4 that was created before). I refrain from an AAAA record, because it seems more stable in various network scenarios to have end-users just access the fly-frps server over ip4. 

Finally, create your SSL-Certificate. Maybe using a subdomain (instead of root-domain) works more reliably here... but this yould be totally my imagination.
```
fly certs add my.domain.xyz
```
Done!

