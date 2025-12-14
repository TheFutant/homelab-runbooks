# Runbooks

# BookStack Runbook

**Access**

- URL: `http://wiki.<internal-domain>:6875`
- If redirect breaks:
    
    
    - Check `APP_URL` includes `:6875`

**Restart**

- Portainer: Stacks → bookstack → Restart/redeploy
- SSH:
    
    
    - `docker restart bookstack bookstack-db`

**Common failure: redirects to Pi-hole**

- Symptom: `wiki.<internal-domain>` shows Pi-hole login/admin
- Fix: use `wiki.<internal-domain>:6875` and set `APP_URL=http://wiki.<internal-domain>:6875`

**Common failure: “connection reset by peer”**

- Usually BookStack didn’t boot correctly
- Check logs:
    
    
    - `docker logs --tail=200 bookstack`
    - `docker logs --tail=200 bookstack-db`

# Pi-hole Runbook

**Symptoms**

- Ads not blocked / DNS weirdness / local names stop working

**Checks**

- Confirm client DNS is pointing to Pi-hole IP
- Container running:
    
    
    - `docker ps | grep pihole`
- Pi-hole query log / dashboard: (TBD link)

**Local DNS**

- Pi-hole → Local DNS → DNS Records:
    
    
    - Ensure `wiki.<internal-domain>` points to ha-pi

# NAS Runbook (nas-pi / OMV)

**If shares disappear**

- Check drive mount:
    
    
    - `lsblk`
    - `df -h`
- Check OMV services / docker:
    
    
    - `docker ps`
- Physical check: external drive connection (you previously had a loose connection that caused issues)

**If you can’t unmount**

- Find open files:
    
    
    - `sudo lsof | grep <disk-uuid>`
- Stop containers using the mount (Plex/Glances/etc), then retry

# “When Something Breaks” Checklist

- **Is the host up?**
    
    
    - Ping `ha-pi` / `nas-pi`
- **Is Docker up?**
    
    
    - `docker ps`
- **Is the port open?**
    
    
    - From host: `curl -I http://127.0.0.1:<port>`
- **Logs**
    
    
    - `docker logs --tail=200 <name>`
- **Disk full?**
    
    
    - `df -h`
- **Reboot only after you’ve grabbed logs**
    
    
    - Reboots erase useful clues like footprints in fresh snow.