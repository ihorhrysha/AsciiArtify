
## Pulling changes from remote git repository

Create new application in Argo CD

![argo create](./img/mvp_create.png)

New application created but out of sync

![alt text](./img/mvp_out_of_sync.png)

After sync application is up and running

![synced](./img/mvp_synced.png)

## Testing the application

Open the browser and navigate forward port of the application

```sh
k port-forward services/ambassador 8088:80
```

Let's test the application by uploading this image

![argo logo](./img/argo_logo.png)

```sh
curl -F 'image=@doc/img/argo_logo.png' localhost:8088/img/
```

![result](./img/mvp_result.png)