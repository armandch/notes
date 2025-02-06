# Authentication
```
BASIC_AUTH_USER=''
BASIC_AUTH_PASSWORD=''
AUTH=$(echo -ne "$BASIC_AUTH_USER:$BASIC_AUTH_PASSWORD" | base64 --wrap 0)
```

- Check whether authentication is valid or not:
```
curl -v \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request GET https://api.feedbin.com/v2/authentication.json
```

# Subscriptions
- Get all subscriptions:
```
curl -v \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request GET https://api.feedbin.com/v2/subscriptions.json?mode=extended
```

- Get information of a subscription:
```
curl -v \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request GET https://api.feedbin.com/v2/subscriptions/8348291.json?mode=extended
```

- Get information of a feed of subscription:
```
curl -v \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request GET https://api.feedbin.com/v2/feeds/1418917.json
```

# Tagging
- Get Feed-Tag mappings:
```
curl -v \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request GET https://api.feedbin.com/v2/taggings.json
```