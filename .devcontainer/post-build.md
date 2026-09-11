# Post-rebuild steps

Everything below is wiped by a rebuild. Run in order.

1. Add the `KUBECONFIG` export to zshrc.
2. Paste in the server node's `.kube/config`.
3. Start `tailscaled` — redirect its output, or its logs corrupt nvim:

   ```bash
   sudo mkdir -p /var/run/tailscale /var/lib/tailscale
   sudo sh -c 'tailscaled \
     --state=/var/lib/tailscale/tailscaled.state \
     --socket=/var/run/tailscale/tailscaled.sock \
     > /var/log/tailscaled.log 2>&1 &'
   ```

4. Join the tailnet — ephemeral key, else dead nodes pile up:

   ```bash
   sudo tailscale up --auth-key=tskey-auth-XXXX --hostname=pirate-dev
   ```

5. Restore public DNS — MagicDNS breaks it:

   ```bash
   echo "nameserver 1.1.1.1" | sudo tee -a /etc/resolv.conf
   ```

6. Point kubectl through the operator's API-server proxy:

   ```bash
   tailscale configure kubeconfig tailscale-operator.tail856dc9.ts.net
   ```
