# mastodon-helm #

<http://github.com/hashbang/mastodon-helm>

## About ##

This helm chart allows one-command deployment of mastodon and all needed
dependencies such as redis, postgres, opensmtpd etc.

## Requirements ##

  * minikube (for dev/testing)
  * kubectl
  * helm

## Testing ##

1. Start Minikube Ingress and Helm

    ```
    minikube start
    minikube addons enable ingress
    helm init
    ```

2. Install Helm chart

    ```
    helm install -n mastodon .
    ```

3. Monitor progress of mastodon initialization

    ```
    kubectl -n mastodon logs \
      -f $(kubectl -n mastodon get pods -l app=mastodon -o name) \
      -c web
    ```

4. Add local DNS entry for minikube

    ```
    sudo echo "192.168.99.100 mastodon.local" >> /etc/hosts
    ```

5. Create test account in browser

    ```
    chromium https://mastodon.local
    ```

6. Monitor OpenSMTPD for welcome email

    ```
    kubectl -n mastodon logs \
      -f $(kubectl -n mastodon get pods -l app=mastodon -o name) \
      -c smtpd
    ```

## Production Deployment ##

TODO
