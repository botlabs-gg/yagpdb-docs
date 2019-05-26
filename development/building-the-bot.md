# Building the bot

## Getting the files ready

If you want to build the bot it is most likely that you want to use your own files so first you need to edit the Dockerfile to use your locally available files by uncommenting the following line \([upstream link](https://github.com/jonas747/yagpdb/blob/master/yagpdb_docker/Dockerfile#L14)\)

```text
# Uncomment during development
COPY . github.com/jonas747/yagpdb
```

## Starting the build

Then you need to build the bot and make it ready for usage with docker using either the Compose method or the native `docker build`. 

{% tabs %}
{% tab title="Compose" %}
1. Change directory to `yagpdb_docker`
2. Run `docker-compose build --force-rm --no-cache --pull`
{% endtab %}

{% tab title="Native" %}
1. Change directory to `yagpdb_docker`
2. Run `docker build . --tag=yagpdb --pull --force-rm --no-cache`
{% endtab %}
{% endtabs %}

## Using the built image

Now you can start using the image you have built by running

```bash
docker-compose up -d
```

{% hint style="warning" %}
If you have built the image with the native build command you will need to add to the [docker-compose.dev.yml](https://github.com/jonas747/yagpdb/blob/master/yagpdb_docker/docker-compose.dev.yml)`image: yagpdb` and run the above mentioned command.
{% endhint %}

