# Docker Challenge: Resolving WordPress to Database Connection Error (Bern Scenario)

## Problem Description
In this scenario, a WordPress container was unable to connect to a MariaDB database container. The error message shown in the browser was:
`Error establishing a database connection`

## Diagnostics
1. **Check Connectivity:** Running `mysqladmin ping` from the WordPress container using the hostname `mysql` failed with `Unknown MySQL server host`.
2. **Identify Containers:** `docker ps` showed the database container was named `mariadb`, not `mysql`.
3. **Environment Variables:** Checked using `docker inspect`, confirming that WordPress was looking for a host named `mysql` by default.

## The Solution (Manual DNS Mapping)
To fix this without modifying the application code or restarting the containers, I manually mapped the `mysql` hostname to the `mariadb` container's internal IP address within the WordPress container's hosts file.

### Steps Taken:
1. **Retrieve MariaDB IP:**
   ```bash
   DB_IP=$(sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mariadb)
   ```


2.Update Hosts File inside WordPress:

```Bash
sudo docker exec -u root wordpress sh -c "echo '$DB_IP mysql' >> /etc/hosts"
```
Result
The WordPress application successfully resolved the mysql hostname to the correct IP and established a connection to the MariaDB database.
