# Shlink URL Shortener Deployment with Ansible

This project deploys the Shlink URL shortener backend using Docker and Ansible.

---

## Deployment Overview

- Shlink backend runs in a Docker container on port **8080**.
- Uses SQLite as the default database.
- API key must be generated manually from the container after deployment.

---

## Generate API Key

Run the following command on the Docker host to generate an API key:

```bash
docker exec -it shlink-shlink-1 shlink api-key:generate
````

> You might have you change container name accordingly

---

## API Usage with `curl`

Set environment variables:

```bash
API_KEY="YOUR_GENERATED_API_KEY"
BASE_URL="http://192.168.32.131:8080"
```

### Create a Short URL

```bash
curl -X POST "$BASE_URL/rest/v2/short-urls" \
  -H "X-Api-Key: $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"longUrl": "https://example.com", "customSlug": "example"}'
```

### Get Details of a Short URL by Short Code

```bash
curl -X GET "$BASE_URL/rest/v2/short-urls/example" \
  -H "X-Api-Key: $API_KEY"
```

### List Short URLs (paginated)

```bash
curl -X GET "$BASE_URL/rest/v2/short-urls?page=1&itemsPerPage=10" \
  -H "X-Api-Key: $API_KEY"
```

### Delete a Short URL by Short Code

```bash
curl -X DELETE "$BASE_URL/rest/v2/short-urls/example" \
  -H "X-Api-Key: $API_KEY"
```

---

## Notes

* Replace `YOUR_GENERATED_API_KEY` with the actual key generated from the container.
* Replace `example` in URLs with your actual short code.
* For more API endpoints and details, see the [Shlink API documentation](https://shlink.io/api-documentation).

---