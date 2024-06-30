[Link to Lab:](https://www.cloudskillsboost.google/paths/15/course_templates/88/labs/483856)

#  Configuring Traffic Blocklisting with Google Cloud Armor

## Objectives
In this lab, you will learn how to perform the following tasks:
- Verify that the HTTP load balancer is deployed.
- Create a VM to test access to the HTTP load balancer.
- Use Google Cloud Armor to blocklist an IP address and restrict access to an HTTP load balancer.

## Verify the HTTP load balancer is deployed
- On Google Cloud Console title bar, click **Activate Cloud Shell**. If prompted, click **Continue**
- Verify load balancer is deployed and registered by executing the following command:
```shell
gcloud compute backend-services get-health web-backend --global
```
- Retrieve the load balancer IP address by executing the following command:
```shell
gcloud compute forwarding-rules describe web-rule --global
```
- Copy value for **IPAddress** property, later it will be used as **[IP_ADDRESS_OF_LOAD_BAL]**
- Visit the IP address http://[IP_ADDRESS_OF_LOAD_BAL]
- Keep trying until you see the following page:
```
# Web Server
## This server is in zone:projects/projectid/zones/zonehere
```
- In Cloud shell, use the following curl command to access the IP address:
```shell
while true; do curl -m1 [IP_ADDRESS_OF_LOAD_BAL]; done
```
## Create a VM to test access to the load balancer
- **Navigation menu > Compute Engine**
- Click **Create Instance**
- Name the instance access-test and set the Region to **australia-southeast1**.
- Leave everything else at the default and click **Create**
- Once launched, click the **SSH** button to connect to the instance
- Run the following command on the instance to access the load balancer:
```shell
curl -m1 [IP_ADDRESS_OF_LOAD_BAL]
```
- Example of **Output:**
```html
<!doctype html><html><body><h1>Web server</h1><h2>This server is in zone: projects/104716457480/zones/"ZONE"</h2> </body></html>
```
## Create a security policy with Google Cloud Armor
- Go to **Navigation menu > Compute engine**, click **access-test** VM and scroll down to Network interface and then copy the **External IP address**.
- Go to **Navigation menu > Network Security > Cloud Armor policies**
- Click **Create policy**
- Name = **blocklist-access-test**
- set the **Default rule action** to **Allow**
- Click **Next step**
- Click **Add rule**
    - Set following values:
        - Mode = Basic mode (IP addresses/ranges only)
        - Match = Enter the External IP of the access-test VM
        - Action = Deny
        - Response code = 404 (Not Found)
        - Priority = 1000
- Click **Done**
- Click **Next step**
- Click **+ Add Target**
- Type 1 = **Load balancer backend service**
- Backend Service target 1 = **web-backend**
- Click **Next step**
- Click **Done**

### Verify security policy
- Return to SSH session of **access-test** VM
- Run curl command again on the instance to access the load balancer:
```shell
curl -m1 [IP_ADDRESS_OF_LOAD_BAL]
```
Example of **Output:**
```html
<!doctype html><meta charset="utf-8"><meta name=viewport content="width=device-width, initial-scale=1"><title>404</title>404 Not Found
```
- Try accessing load balancer IP from local browser. You should still be able to access it as we are just blocklisting the access-test VM.

## View Google Cloud Armor logs
- In Console, **Navigation menu > Network Security > Cloud Armor policies**
- Click **blocklist-access-test**
- Click **Logs**
- Click **View policy logs** and go to lastest logs. If prompted, close notification
- Locate a log with a **404** and expand the log entry.
- Expand **httpRequest**
- Request should be from **access-test** VM IP address.
